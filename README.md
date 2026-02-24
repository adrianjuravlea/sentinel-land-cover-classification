# Sentinel-2 Land Cover Classification using Random Forest

This project implements a complete machine learning pipeline to classify land cover types in the **Petris-Hunedoara region** of Romania.
It utilizes **Sentinel-2 satellite imagery** processed via the **Google Earth Engine (GEE)** API and a **Random Forest** classifier to automate terrain mapping.



## 🚀 Overview
The project automates the transition from raw satellite data to a localized, classified GeoTIFF map. By combining spectral bands with calculated indices, 
the model distinguishes between natural and man-made features with high accuracy.

### **Classes Identified:**
* 🌾 **Agriculture** & 🐑 **Pastures**
* 🌲 **Forest**
* 🏘️ **Village** (Built-up areas)
* 🏗️ **Stone Quarry**
* 🛣️ **Roads** & 🚂 **Rails**
* 💧 **Water**

## 🛠️ Tech Stack
* **Cloud Infrastructure:** Google Earth Engine (Sentinel-2 Harmonized Dataset)
* **Language:** Python 3.x
* **Machine Learning:** `scikit-learn` (Random Forest)
* **Geospatial Tools:** `geopandas`, `rasterio`, `folium`
* **Visualization:** `matplotlib`, `seaborn`

## 📊 Methodology
1. **Data Acquisition:** Filtering Sentinel-2 collections for cloud-free summer imagery (2023).
2. **Feature Engineering:** Calculation of spectral indices:
   - **NDVI** (Vegetation Index)
   - **NDWI** (Water Index) - *Recommended for accuracy*
   - **NDBI** (Built-up Index) - *Recommended for urban/road separation*
3. **Training Strategy:**
   - Supervised classification using ~460 manually labeled points.
   - **Stratified Train/Test Split (80/20)** to handle class imbalance.
   - **Balanced Class Weights** to improve detection of minority classes like roads and rails.
4. **Validation:** Evaluated via a classification report and confusion matrix, currently achieving an accuracy of **~81%**.



## 📈 Area Statistics
The script calculates the physical footprint of each land cover class. Since each Sentinel-2 pixel is $10m \times 10m$ ($100m^2$), the area is derived as:

$$\text{Area (ha)} = \frac{\text{Pixel Count} \times 100}{10,000}$$

| Class | Pixel Count | Approx. Area (ha) |
| :--- | :--- | :--- |
| Forest | ~976,144 | ~9761.4 |
| Agriculture | ~248,816 | ~2488.2 |
| Village | ~38,328 | ~383.3 |

## 📂 Project Structure
```text
├── sentinel-land-cover-classification.ipynb  # Main processing pipeline
├── geojson/                                  # Training labels (point data)
├── sampled_data/                             # Extracted spectral values
├── raster/                                   # Output GeoTIFF classification
└── README.md                                 # Project documentation