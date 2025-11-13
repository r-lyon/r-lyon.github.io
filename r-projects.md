---
layout: archive
title: "R Projects"
permalink: /r-projects/
author_profile: true
---

# Featured R Workflows

This page highlights selected R scripts and reproducible workflows for environmental and hydrologic data analysis.

###  PFAS Stacked Bar Plot – Sandia Wetland
This R script creates a stacked bar chart showing the concentrations of PFAS chemicals detected at different sampling sites in Upper Sandia Canyon. It combines data from alluvial wells and surface water gaging stations, focusing on results collected from 2024 stormflow, baseflow, and groundwater sampling events. All data are publicly available at intellusnm.com

- **Script location:** [`PFAS/code/pfas_analysis.R`](https://github.com/r-lyon/Environmental-R-Scripts/tree/master/PFAS/code)  
- **Example output:**  
![PFAS Summary](https://github.com/r-lyon/Environmental-R-Scripts/blob/master/PFAS/output/stacked_bar/PFAS_Upper_Sandia_Stacked_Bar_Plot_2024.png?raw=true)

<small>Figure: Stacked bar plot of PFAS concentrations in Upper Sandia Canyon. This visualization compares detected PFAS compounds across monitoring locations, grouped by hydrologic condition: stormflow (6/20/2024), baseflow (7/30/2024), and shallow alluvial groundwater (10/24/2024). Sampling dates were chosen close in time to help assess potential PFAS sources within the Sandia wetland system. The stacked format highlights both the relative contribution of individual PFAS chemicals and the overall concentration profile at each site...</small>
---

## Hardness Metal Screening – Surface Water
This R script screens surface water samples for hardness-dependent metals against both **acute** and **chronic aquatic life criteria** using New Mexico Environment Department (NMED) surface water quality standards (20.6.4.900 NMAC).  https://www.env.nm.gov/surface-water-quality/wp-content/uploads/sites/18/2025/04/20.006.0004-NMAC-22May25.pdf

The criteria are expressed as a function of **hardness (mg CaCO₃/L)** and apply within specific hardness ranges:  

- **0–400 mg/L** for most metals (criteria for 400 mg/L applied above range)  
- **0–220 mg/L** for Aluminum (criteria for 220 mg/L applied above range)  

Acute and chronic criteria (in µg/L) are calculated using:  

Acute: exp(`mA` * ln(hardness) + `bA`) * `CF`

Chronic: exp(`mC` * ln(hardness) + `bC`) * `CF`

Where:  
- `mA` / `bA` and `mC` / `bC` are metal-specific constants  
- `CF` is the conversion factor  
- Special adjustments are applied for Cadmium and Lead  
- Aluminum is treated separately based on if sample is from base flow (WS) or storm flow (WT)
- **Note:** The script excludes the 2025 site-specific copper criteria for the Pajarito Plateau (Rio Grande Basin).

- **Script location:** [`HardnessScreening/code/MetalsHardnessBasedScreening.R`](https://github.com/r-lyon/Environmental-R-Scripts/tree/master/HardnessScreening/code)  
 
**Notes:**
- All scripts are hosted in the [Environmental-R-Scripts repo](https://github.com/r-lyon/Environmental-R-Scripts).  
- Screenshots above show example outputs — click the links to see full scripts and data.  