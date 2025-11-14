---
layout: single
title: "Hardness-Dependent Metal Screening"
permalink: /projects/hardness-screening/
---

## Hardness-Dependent Metal Screening

This R script screens surface water samples for hardness-dependent metals against both **acute** and **chronic aquatic life criteria** using New Mexico Environment Department (NMED) surface water quality standards ([20.6.4.900 NMAC](https://www.env.nm.gov/surface-water-quality/wp-content/uploads/sites/18/2025/04/20.006.0004-NMAC-22May25.pdf)).

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
 