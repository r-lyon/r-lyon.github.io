---
layout: page
title: "Hyperspectral Dimensionality Reduction via PCA"
subtitle: "Compressing Multi-Band Raster Datasets using the terra Package"
permalink: /projects/pca-hyperspectral/
---

> **View the Complete Code & Data:** You can view the full R script, raw dataset, and processing workflow for this project in my [Environmental-R-Scripts Repository](https://github.com/r-lyon/Environmental-R-Scripts/tree/master/HyperspectralPCA).

## Executive Summary
Hyperspectral sensors record hundreds of narrow, contiguous spectral bands, capturing incredibly detailed surface signatures. However, these adjacent bands are often highly correlated, leading to significant data redundancy and immense computational overhead. 

This project demonstrates an optimized pipeline for compressing a multi-band hyperspectral mosaic into its top three principal components (PCs). By utilizing a randomized pixel sampling technique for statistical efficiency, the process minimizes computational strain while preserving maximum environmental variance for downstream remote sensing workflows.

---

## Methodology & Implementation

### 1. Library Initialization & Spatial Data Ingestion
To handle memory-intensive airborne hyperspectral data efficiently, the workflow utilizes the `terra` package's pointer system alongside the data-wrangling capabilities of the `tidyverse`.

```r
# Load core packages
library(terra)
library(tidyverse)

# Define paths (anonymized for public portfolio distribution)
# The multi-band raster (.dat) requires its matching header (.hdr) file in the same directory
raster_path <- "data/hyperspectral/Hyperspectral_2025_Geof.dat" 
hs_data     <- rast(raster_path)

print(hs_data)
```

### 2. Efficiency Optimization: Pixel Sampling
Running a Principal Component Analysis (PCA) directly on millions of pixels across dozens of flight lines is computationally prohibitive. To build an accurate statistical model efficiently, a reproducible random sample of 10,000 pixels is drawn across the spatial extent of the image grid.

```r
# Establish seed for reproducibility 
set.seed(42)

# Extract a random spatial sample of 10,000 pixels as a data frame
sampled_data <- spatSample(hs_data, size = 10000, method = "random", as.df = TRUE)

# Drop missing values to clean the statistical matrix
sampled_data <- na.omit(sampled_data)
```

### 3. PCA Model Fitting & Eigenvalue Evaluation
The PCA is fitted using R’s native `prcomp()` function. Centering and scaling are explicitly set to true (`scale. = TRUE`) to standardize individual band variances, preventing bands with wider dynamic ranges from skewing the principal components.

```r
# Compute PCA on standard-scaled pixel data
pca_model <- prcomp(sampled_data, scale. = TRUE)
summary(pca_model)

# Calculate the proportion of variance explained by each eigenvalue
variance_explained <- (pca_model$sdev^2) / sum(pca_model$sdev^2)
```
### 4. Scree Plot
To determine how many principal components are necessary to capture meaningful variance, we isolate the top 10 components and construct a **Scree Plot** to identify the inflection point ("elbow").

```r
# Generate the Scree Plot via ggplot2
data.frame(PC = 1:length(variance_explained), Variance = variance_explained) %>%
  slice(1:10) %>% 
  ggplot(aes(x = PC, y = Variance)) +
  geom_line(color = "darkgreen", linewidth = 1) +
  geom_point(size = 3) +
  labs(title = "Scree Plot: Explained Variance by PC",
       x = "Principal Component", 
       y = "Proportion of Variance") +
  theme_minimal()
```

<img src="https://github.com/r-lyon/Environmental-R-Scripts/blob/master/HyperspectralPCA/img/sandia_pca_scree_plot.png?raw=true" alt="Scree Plot Analysis" width="450">

> **Key Finding:** Looking at the elbow of the plot above, the vast majority of spectral variance is captured within the first few components. Adding components beyond PC3 yields diminishing information returns.

---

### 5. Spatial Prediction & GeoTIFF Export
Once the statistical weights are generated, the model coefficients are predicted back across every single pixel in the original, full-resolution hyperspectral raster grid. By defining `index = 1:3`, we strictly output a lightweight, three-layered spatial image representing PC1, PC2, and PC3.

```r
# Project the PCA model back onto the original full-extent raster layer
hs_pca_raster <- predict(hs_data, pca_model, index = 1:3)
names(hs_pca_raster) <- c("PC1", "PC2", "PC3")

# Export the compressed principal components as an analysis-ready GeoTIFF
writeRaster(hs_pca_raster, 
            filename = "Output/hyperspectral_pca_compressed.tif",
            overwrite = TRUE)
```

#### Spatial Analysis Results
![Compressed PCA Spatial Layer](../../images/projects/pca_raster_output.png)

---

## Technical Takeaways
1. **Dimensionality Reduction:** Compressed hundreds of highly collinear hyperspectral bands into just 3 distinct, high-contrast layers.
2. **Computational Optimization:** Avoided local machine crashes by subsampling the data matrix ($N=10,000$) to train the model weights before mapping it back spatially.
3. **Application:** The final 3-band GeoTIFF functions as an optimized, lightweight base layer ideal for land cover classification, anomaly detection, or high-contrast visual RGB color interpretation.