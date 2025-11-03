---
layout: page
title: "Sample Location Webmap"
permalink: /webmap/
author_profile: true
---

## Interactive Map of Environmental Sample Locations

Explore the stormwater sampling locations collected in 2023 with this interactive webmap.  
Click the button below to open the map in a new tab:

<div style="margin: 20px 0;">
  <a href="/assets/webmap/index.html" target="_blank" style="
     display:inline-block;
     padding:10px 20px;
     background-color:#007ACC;
     color:white;
     text-decoration:none;
     border-radius:5px;
     font-weight:bold;
  ">Open Interactive Map</a>
</div>

---

### Map Preview

<img src="/assets/webmap/lib/sample_map_preview.png" 
     alt="Sample Location Map Preview" 
     style="max-width:600px; width:100%; border:1px solid #ddd; border-radius:5px; box-shadow:2px 2px 6px rgba(0,0,0,0.1);">

---

### About This Map

This webmap was generated using **R** with the `leaflet` and `sf` packages.  
It shows all stormwater sampling locations for the year 2023 and allows you to explore by site, date, and program type (MSGP, Gage, IP).  

**Data Source:** [Intellus New Mexico](https://www.intellusnm.com/index.cfm) — provided by Los Alamos National Laboratory (LANL) and the New Mexico Environment Department (NMED DOE OB).  

**Author:** Russ Lyon — Environmental Scientist | GIS & Data Visualization