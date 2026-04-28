# 🛰️ Automated Sentinel-2 Geospatial ETL Pipeline

An automated Extract, Transform, Load (ETL) pipeline designed for continuous environmental monitoring. This project programmatically fetches Copernicus Sentinel-2 satellite imagery, calculates water indices via raster math, and vectorizes the data into standard geographic formats to track riverbank geomorphology and water extents over time.

## 📋 Architecture & Overview

This pipeline operates entirely in the cloud via GitHub Actions, eliminating the need for manual satellite data retrieval. Currently targeted at a highly dynamic bounding box of the Padma River (near the Hardinge Bridge, Bangladesh), it builds a time-series archive of vector data ready for GIS overlay analysis.

### ✨ Core Features
* **Cloud-Native Automation:** Runs on a scheduled `cron` job (every 3 days) via GitHub Actions CI/CD.
* **API Integration:** Authenticates and interfaces with the Sentinel Hub / CDSE API to pull Level-2A atmospherically corrected imagery.
* **On-the-Fly Raster Math:** Utilizes a custom JavaScript Evalscript to calculate the Normalized Difference Water Index (NDWI) during the API request, minimizing bandwidth.
* **Geospatial Vectorization:** Transforms pixel-based water masks into clean, projected `.geojson` feature classes using `rasterio`, `shapely`, and `geopandas`.
* **Dynamic Archiving:** Automatically stamps outputs with the current datetime (e.g., `padma_water_YYYY-MM-DD.geojson`) and commits them back to the repository.
* **Alert System:** Calculates total water pixel area and dispatches an automated SMTP email alert upon successful execution.

## 🛠️ Technology Stack
* **Language:** Python 3.10
* **Geospatial Libraries:** `sentinelhub`, `rasterio`, `geopandas`, `numpy`, `shapely`
* **Infrastructure:** GitHub Actions
* **Data Source:** Copernicus Sentinel-2 (Level-2A)

## 🗺️ GIS Integration (ArcGIS Pro / QGIS)

The primary outputs are time-stamped `.geojson` files, designed for immediate cartographic use and change-detection analysis:
1. Clone or download the raw `.geojson` files from this repository.
2. Import via the **JSON To Features** tool (ArcGIS Pro) or drag-and-drop (QGIS).
3. Project to a local coordinate system (e.g., UTM Zone 46N).
4. Perform Symmetrical Difference overlay analysis between historical and current layers to calculate exact square meters of land lost to riverbank erosion.

## Screenshots
<img width="1920" height="1032" alt="Screenshot 2026-04-29 032212" src="https://github.com/user-attachments/assets/6fc0c03f-f70d-4e22-9fe0-d2b4c47a1276" />
<img width="1920" height="1032" alt="Screenshot 2026-04-29 032235" src="https://github.com/user-attachments/assets/54df512f-ed49-4e37-ab52-0d8984ed8a4b" />
<img width="1920" height="1040" alt="Screenshot 2026-04-29 032628" src="https://github.com/user-attachments/assets/72a718fe-046c-4418-94fb-3bb7626e6c1e" />


---
**Author:** Mustaq Hasnat Tamim  
**Academic Focus:** Environmental Science and Geography  
