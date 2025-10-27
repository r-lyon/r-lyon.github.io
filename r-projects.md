---
layout: archive
title: "R Projects"
permalink: /r-projects/
author_profile: true
---

## Featured R Workflows

This page highlights selected R scripts and reproducible workflows for environmental and hydrologic data analysis.

###  PFAS Stacked Bar Plot – Sandia Wetland
This R script processes and visualizes PFAS (Per- and Polyfluoroalkyl Substances) concentration data collected from monitoring sites aassociated with the Sandia Wetland. The workflow demonstrates data wrangling, integration, and visualization skills using the tidyverse ecosystem.

Data Import & Cleaning

Reads PFAS monitoring data from CSV and Excel files.

Standardizes column names with janitor::clean_names().

Filters for regulatory samples analyzed with EPA Method 1633.

Data Integration

Combines alluvial and gage datasets.

Filters only detected PFAS compounds.

Joins with a reference table of PFAS parameter codes and short names.

Selects sampling dates close in time to allow comparison of PFAS sources under different hydrologic conditions.

Visualization

Creates a stacked bar chart of PFAS concentrations (ggplot2).

Groups results by sampling location and sample type (stormflow, baseflow, and shallow alluvial groundwater within the Sandia wetland).

Uses faceting to compare across sample types and custom color palettes for clarity.

Adds descriptive labels, legends, and rotated axis text for readability.

Output

Saves the final plot as a high-resolution PNG for reporting or presentations.

Skills Demonstrated
Data wrangling with dplyr

Date handling with lubridate

Custom plotting with ggplot2

Color scaling with viridisLite

Reproducible workflows for environmental data analysis

- **Script location:** [`PFAS/code/pfas_analysis.R`](https://github.com/r-lyon/Environmental-R-Scripts/tree/master/PFAS/code)  
- **Example output:**  
![PFAS Summary](https://github.com/r-lyon/Environmental-R-Scripts/blob/master/PFAS/output/stacked_bar/PFAS_Upper_Sandia_Stacked_Bar_Plot_2024.png?raw=true)

Figure: Stacked bar plot of PFAS concentrations at Sandia. This visualization compares detected PFAS compounds across monitoring locations, grouped by hydrologic condition: stormflow (6/20/2024), baseflow (7/30/2024), and shallow alluvial groundwater (10/24/2024). Sampling dates were chosen close in time to help assess potential PFAS sources within the Sandia wetland system. The stacked format highlights both the relative contribution of individual PFAS chemicals and the overall concentration profile at each site.
---

 **Notes:**
- All scripts are hosted in the [Environmental-R-Scripts repo](https://github.com/r-lyon/Environmental-R-Scripts).  
- Screenshots above show example outputs — click the links to see full scripts and data.  