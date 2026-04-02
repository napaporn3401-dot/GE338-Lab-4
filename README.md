# Flood Risk Modeling using Multi-Criteria Analysis (MCA) in Google Earth Engine

## Overview
This project develops a spatial flood risk model for Tak Province, Thailand using Multi-Criteria Analysis (MCA) implemented in Google Earth Engine (GEE).

The model integrates multiple environmental factors to generate a flood susceptibility map.

---

## Research Question
Which areas in Tak Province are most vulnerable to flooding based on physical and environmental factors?

---

## Methodology

### 1. Data Sources
- DEM: USGS SRTM
- Rainfall: ERA5 Daily Aggregated
- Land Cover: MODIS MCD12Q1
- Rivers: WWF HydroSHEDS

---

### 2. Data Preprocessing
All input layers were clipped to the study area (Tak Province) and prepared in raster format.

---

### 3. Normalization
Each factor was normalized using Min-Max scaling:

\[
X' = \frac{X - X_{min}}{X_{max} - X_{min}}
\]

This ensures all variables are on a comparable scale (0–1).

---

### 4. Weighted Overlay Model

Flood risk was calculated using the weighted linear combination:

\[
FloodRisk = (0.30 \cdot Rain) + (0.25 \cdot Slope) + (0.20 \cdot Elevation) + (0.15 \cdot River) + (0.10 \cdot Landcover)
\]

---

### 5. Classification
Flood risk values were classified into three categories:

- Low Risk: < 0.25
- Medium Risk: 0.25 – 0.45
- High Risk: > 0.45

---

## Sensitivity Analysis
A sensitivity analysis was conducted by varying the weight of rainfall by ±20%.

The results indicate that the model is highly sensitive to rainfall and slope, confirming their dominant influence on flood risk.

---

## Validation
Due to the lack of ground truth data, validation was performed qualitatively by comparing model outputs with known flood-prone regions and satellite-based datasets.

---

## Results
The model successfully identifies flood-prone areas, particularly low-lying regions near rivers and areas with low slope.

---

## Limitations
- Lack of ground truth data for quantitative validation
- Simplified weighting scheme
- Static model without temporal variation
- Differences in spatial resolution among datasets

---

## Conclusion
The MCA approach provides a useful framework for flood risk assessment. However, the accuracy of the model depends heavily on the quality of input data and the weighting scheme.

---
## Sensitivity Analysis

The model was tested by adjusting the weight of the rainfall factor by ±20%.

Two scenarios were evaluated:
- Increased rainfall weight (0.30 → 0.36)
- Decreased rainfall weight (0.30 → 0.24)

### Observations:
- Areas near rivers showed consistent high risk across scenarios.
- Low-lying regions remained sensitive to weight changes.
- Some boundary areas changed classification, indicating model uncertainty.

### Conclusion:
The model is most sensitive to rainfall and slope, suggesting these are the dominant drivers of flood risk in the study area.
## Repository Structure
GE338-Lab-4/
├── lab4_modeling.ipynb  
├── conceptual_framework.md  
├── README.md  
├── figures/  
