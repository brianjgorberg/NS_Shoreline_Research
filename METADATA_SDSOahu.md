# Title: Satellite-Derived Shorelines for O‘ahu, Hawai‘i (1990–2022) from Landsat, Sentinel-2, and PlanetScope Imagery

Dataset Identifier: XXX

Version: v1.0

**Creators:**
Anna Mikkelsen, Joel Nicolow, Richelle Moskvichev
Coastal Research Collaborative, University of Hawai‘i at Mānoa

Date of Creation: June 2024  
Date Range of Observations: 1990–2022

**Geographic Coverage:**

- Region: Island of O‘ahu, Hawai‘i
- Spatial Coverage: Full coastline, divided into 112 littoral cells based on transects generated for CoSMoS-COAST (version 2023-11-27)

**Dataset Description:** 

This dataset contains satellite-derived shoreline (SDS) transect intersections for the island of O‘ahu, Hawai‘i, spanning 1990–2022. Shorelines were extracted from three satellite sources - Landsat 5–9, Sentinel-2, and PlanetScope - using two satellite shoreline frameworks: CoastSat and CoastVision. Each shoreline is represented by its intersection with a shore-normal transect. There are 5689 transects within 112 littoral cells - this transect grid was developed for the CoSMoS-COAST modeling framework.

Each shoreline position is corrected for tidal variability using the global AVISO FES2014 tide model and filtered for outliers with a site-specific median filter (typically 30 m).

**Publications with these data:**

- Moskvichev, Richelle U., Anna B. Mikkelsen, Tiffany R. Anderson, Sean F. Vitousek, Joel C. Nicolow, and Charles H. Fletcher. “Wave Driven Cross Shore and Alongshore Transport Reveal More Extreme Projections of Shoreline Change in Island Environments.” *Scientific Reports* 15, no. 1 (March 28, 2025): 10794. <https://doi.org/10.1038/s41598-025-95074-y>. 

**Folder Structure and Data Sources:** 

The dataset is organized into three folders, each containing shoreline intersection data for 112 littoral cells. All files are in CSV format.

**COASTSAT/**
Satellite source: Landsat 5–9 and Sentinel-2
Tool: CoastSat
Resolution: 30 m pansharpened to 15 m for Landsat; 10 m for Sentinel-2 (with the 20 m SWIR pansharpened to 10 m)
Description: Includes shoreline positions derived using the CoastSat algorithm, with waterline detection based on the Modified Normalized Difference Water Index (MNDWI) and a classifier trained on images of Hawaiian beaches.

**PLANET_RAW/**
Satellite source: PlanetScope (PS2, PS2.SD)
Tool: CoastVision
Resolution: 3.7–4.1 m (resampled to 3 m by provider)
Description: Contains shoreline positions derived from  PlanetScope imagery using a logistic regression classifier and direct land-water contour extraction. No bias correction applied.

**PLANET_BIASCORRECTED/**   
Satellite source: PlanetScope   
Tool: CoastVision   
Resolution: 3.7–4.1 m (resampled to 3 m by provider)   
Description: Contains the same shoreline data as PLANET_RAW, but corrected for mean bias relative to CoastSat. For the overlapping period (2017-2021/2022, depending on site), the difference in mean shoreline position for each transect was calculated and removed from the PLANET_RAW values. (e.g. if CoastVision detected 5m further seaward than CoastSat for transect 1, then 5 m was subtracted from all transect 1 CoastVision values). This enables a continuous time-series of the data between CoastSat and CoastVision.

**Files:** Each folder contains a CSV file for each of the 112 littoral cells. Each csv file has a shoreline position (transect intersection) for each date (rows), and transect (columns).

**Method Summary:**  
See *Moskvichev et al. 2025* for further details on methodology

**CoastSat:** A Python-based tool used to extract instantaneous waterlines from Landsat and Sentinel-2 imagery. Images are pansharpened (Landsat 7–9) or bilinearly resampled (Landsat 5). The shoreline is detected using a threshold on the Modified Normalized Difference Water Index (MNDWI) and refined using the marching squares algorithm. A Hawai‘i-specific classifier was trained using labeled data from carbonate beaches on O‘ahu.

**CoastVision:** A custom Python tool for extracting shorelines from PlanetScope imagery. Classifies pixels as 'land' or 'water' using logistic regression based on band values, spectral indices (e.g., NDVI, MNDWI), and local texture metrics. The shoreline is directly delineated from the binary classification map using marching squares. Morphological filtering is used to reduce misclassifications. See framework on github (https://github.com/Coastal-Research-Collaborative/CoastVision) and further details in *Moskvichev et al. 2025.*

**Auxiliary files:** 

**Transect file:** oahu_20231127_transects_epsg3750.geojson contains all transect positions. The transect starting point is the landward transect point which approximately represents the vegetation line delineated on NRCS/NAIP 2022 satellite imagery. Transects are spaced \~20 m apart alongshore at all sandy/rubbly beaches. Transects are not placed at rocky shores. Attributes: 

- id: transect id consistent with the column names of each CSV
- site_id: littoral cell name 
- geometry: start and end coordinates of each transect in NAD83 HARN UTM Zone 4N (EPSG 3750)

**Polygon file:** oahu_20231127_polygon_epsg3750.geojson contains the bounding boxes for each littoral cell. id denotes the littoral cell id. Projection: NAD83 HARN UTM Zone 4N (EPSG 3750)

**Intended Use:** 

Primarily developed for coastal change and hazard modeling using the CoSMoS-COAST framework. This dataset can support shoreline change analysis, coastal vulnerability assessments, and remote sensing studies on O‘ahu. 

**Data Format:**

- CSV (Comma-Separated Values)
- UTF-8 encoding
- Each CSV file includes:
  - date (row)
  - transect number (column) in the format oahu<cellnumber>\_<transectnumber>. i.e.: *oahu0004_0001*
  - and shoreline position (distance from the on-shore transect endpoint to the intersection, in meters).
- For CSVs within the COASTSAT folder, the final column labeled "satname", which indicates the satellite source, "L" for LandSat or "S" for Sentinel. Satellites one of the following: \[L5, L7, L8, L9, S2\].

**Data Type:**

- Observational
- Numeric (shoreline distance along transect)

Temporal Resolution:

- Landsat: 16-day revisit
- Sentinel-2: 5-day revisit
- PlanetScope: Near-daily (depending on site and cloud cover)

Spatial Resolution:

- CoastSat (Landsat): 30 m. pansharpened to 15 m (L5 is biliniarly resampled)
- CoastSat (Sentinel-2): 10 m (20 m SWIR band resampled to 10 m)
- CoastVision (PlanetScope): 3.7–4.1 m (resampled to 3 m by provider) 

Data Quality:

- Outlier removal via median filtering
- Tidal correction applied
- PlanetScope bias correction applied for PLANET_BIASCORRECTED

**Data Stability:**

- Version 1 of this project is complete.
- Updates may occur with improved shoreline detection or to extend the observation timeline

**Licensing:**

- Dataset released under Creative Commons Attribution 4.0 International (CC 4.0)

**Citation:** XXX

**Funding:**
Office of Naval Research (ONR), Coastal Research Collaborative (CRC)

**Software/Code:**

- **CoastSat**: <https://github.com/kvos/CoastSat>
  - CoastSat version 2.3 was used, for the specific version see link: <https://github.com/kvos/CoastSat/releases/tag/v2.3> 
- **CoastVision**: <https://github.com/Coastal-Research-Collaborative/CoastVision>  

**Contact:**  
Anna Mikkelsen  
abm20@hawaii.edu  
Coastal Research Collaborative, University of Hawai‘i at Mānoa

<https://www.soest.hawaii.edu/crc/>