# Command-Line GIS Final Project  
## Airbnbs & Gentrification in New Orleans  

**Author:** Sina-Marie Mayer
**Course:** Command-Line GIS (Bloustein School of Planning and Public Policy, Rutgers University, Fall 2025)

---

## 1. Overview
This project visualizes Airbnb affordability, rental housing gaps, and flood risk in New Orleans. It includes:  

- **Static Map 1:** Airbnb Affordability Ratio per census tract & Airbnb Density 
- **Static Map 2:** Rental Housing Unit Gap & Flood Zones  
- **Interactive Webmap:** Combines Airbnb listings, affordability choropleth, flood zones, and transit buffers  

---

## 2. Static Maps

### Static Map 1: Airbnb Affordability Ratio & Airbnb Density
Shows the **median nightly Airbnb price relative to median daily income**, overlayed with **circles proportional to Airbnb density**.

<img src="airbnb_affordability_map.png" alt="Airbnb Affordability Ratio" width="95%">

---

### Static Map 2: Rental Housing Unit Gap & Flood Zones
Overlays the **rental housing unit gap** with **FEMA Special Flood Hazard Areas (SFHA)**.

<img src="airbnb_housinggap_map.png" alt="Airbnb Rental Housing Gap" width="95%">

---

## 3. Interactive Webmap
This interactive map includes:  

- **Affordability Ratio Choropleth**  
- **Airbnb Listings** (marker cluster)  
- **Airbnb Heat Map**  
- **Flood Zones (SFHA)**  
- **Quarter-mile Transit Buffers**  
- **RTA Transit Routes & Stops**  

<iframe src="nola_Airbnbs.html" height="855" width="95%"></iframe>  

Or view it as a **separate web page**: [nola_Airbnbs.html](nola_Airbnbs.html)

---

## 4. Data Description

### Datasets Used

#### Airbnb Data
- **Source:** [Inside Airbnb](https://insideairbnb.com/get-the-data/)
- **Prepared by:** Inside Airbnb (independent project)
- **Last updated:** 09/11/2025  
- **Original format:** CSV, with latitude/longitude coordinates  
- **Processing:** Spatial join with tract geometries; aggregated listings to census tracts to compute Airbnb count; calculated affordability ratio (median nightly price / median daily income).

#### Tract Geometries
- **Source:** [NHGIS](https://www.nhgis.org/)
- **Prepared by:** National Historical Geographic Information System (NHGIS), University of Minnesota
- **Original format:** Shapefiles 
- **Processing:** Filtered to Orleans Parish.

#### Census Data (Median Household Income (yearly))
- **Source:** American Community Survey (ACS) 2023 5-year estimates, accessed by API
- **Prepared by:** U.S. Census Bureau
- **Original format:** CSV 
- **Processing:** Joined median household income data to census tract geometries & Airbnb data; calculated median daily hosuehold income for affordability ratios; handled missing estimates; calculate CVs for income to flag low-confidence estimates (CV > 40).  

#### Rental Housing Unit Gap
- **Source:** [Moody’s Analytics, Reinvestment Fund, PolicyMap](https://www.policymap.com/data/moodys-housing-shortfall), based on ACS 2023 5-year estimates
- **Prepared by:** Moody's Analytics, Reinvestment Fund, PolicyMap
- **Original format:** CSV with tract identifiers 
- **Processing:** Joined table to tract geometries. 

#### Flood Zones (SFHA)
- **Source:** [FEMA National Flood Hazard Layer (NFHL)](https://msc.fema.gov/portal/home)
- **Prepared by:** Federal Emergency Management Agency (FEMA)
- **Last updated:** 09/30/2016
- **Original format:** Shapefiles 
- **Processing:** Filtered for high-risk flood zones (V/VE) and 100-year zones (A/AE/AO/AH); simplified for webmap display.

#### Transit Routes & Stops
- **Source:** [US Open Data](https://catalog.data.gov/dataset/truck-routes-fcf7e) & [City of New Orleans Open Data](https://data.nola.gov/Transportation-and-Infrastructure/RTA-Stops/hp2r-gr3h/about_data)
- **Prepared by:** City of New Orleans
- **Last updated:** 07/12/2025 & 02/24/2025
- **Original format:** CSV  
- **Processing:** Converted coordinates to shapely geometry; created quarter-mile buffers around stops; simplified geometries for web display.  

### Data Quality Issues
- Missing or low-confidence data in income or rental gap datasets (handled with hatching or “No estimate” coloring).  
- Some shapefiles needed projection adjustment and simplification to display correctly on webmap.  
- Airbnb data required aggregation to tract level to avoid overcrowding on static maps.
