# 🧊 Mendenhall Glacier Retreat Analysis (2014 – 2023)

### Author: *Jinal Vyas (ASU ID 1233053785)*

This project investigates **glacial retreat patterns of the Mendenhall Glacier, Alaska**, using **10 years of Landsat-8 OLI/TIRS Collection 2 Tier-1 data**.
Data were processed and analyzed using **Google Earth Engine (GEE)** for large-scale imagery access, and **Python** for visualization, segmentation, and quantitative change assessment.

---

## 📁 Repository Structure

```
📦 Glacier-Retreat-Analysis
├── glacierAnalysis_DataPreparationReport_JinalVyas.ipynb - Colab.pdf
├── glacierAnalysisModelFinalAnalysisAndDeployment_JinalVyas_1233053785.ipynb - Colab.pdf
├── animation_RGB_GlacierChange.gif
└── README.md
```

> ⚠️ **Note:**
> If the Colab notebooks do not open due to GEE authentication or rendering issues, please refer to the **PDF versions** above — they contain all code cells, outputs, plots, and visualizations.

---

## 🛰️ Project Overview

### **Objective**

To quantify the *decline in glacier area* over a decade by:

* Building a time series of satellite images (2014 – 2023)
* Extracting spectral bands and generating RGB composites
* Performing binary segmentation to identify glacier regions
* Measuring changes in glacier coverage over time

---

## ⚙️ Data and Tools Used

| Component               | Description                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------- |
| **Satellite Data**      | Landsat-8 OLI/TIRS Collection 2 (Level 2 Surface Reflectance, Tier-1)                 |
| **Data Source**         | Google Earth Engine (GEE)                                                             |
| **Bands Used**          | SR_B3 (Green), SR_B4 (Red), SR_B5 (NIR), SR_B6–7 (SWIR)                               |
| **Software/Frameworks** | Python (Colab), GEE API, Rasterio, GDAL, OpenCV, PyTorch, segmentation_models_pytorch |
| **Model**               | UNet with ResNet34/ResNet50/EfficientNet-B4 backbones                                 |
| **Loss Function**       | Dice Loss                                                                             |
| **Evaluation Metric**   | Intersection over Union (IoU) — approaching benchmark standard                        |
| **Visualization**       | Matplotlib, Seaborn, Geemap (GEE maps)                                                |

---

## 🔬 Workflow Summary

1. **Data Acquisition & Pre-Processing**

   * Landsat-8 data fetched via GEE for each month between 2014 – 2023.
   * Applied *cloud & shadow masking* using QA_PIXEL bands.
   * Generated median composites per month to minimize cloud artifacts.
   * Clipped imagery to **Mendenhall Glacier region of interest (ROI)**.

2. **Exploratory Data Analysis (EDA)**

   * Visualized RGB (4-3-2) composites and computed correlation matrices across spectral bands.
   * Evaluated NDSI (Normalized Difference Snow Index) to isolate snow and ice regions.

3. **Segmentation Model Training**

   * Created glacier / non-glacier binary masks using OpenCV.
   * Built a custom dataset loader with torchvision transforms (224×224 resized inputs).
   * Trained UNet models with ResNet34, ResNet50, and EfficientNet-B4 encoders to compare performance.
   * Chose ResNet34 backbone as optimal based on IoU and Dice Loss scores.

4. **Post-Processing & Results**

   * Generated glacier masks for each year and measured glacier area in km².
   * Produced an animated GIF (`animation.gif`) visualizing RGB imagery changes over time.
   * The animation highlights a *progressive reduction in glacier coverage*, visually confirming retreat.

---

## 📊 Results Overview

* **Best Model:** UNet + ResNet34 (backbone)
* **IoU:** Close to benchmark standards for binary segmentation (~0.85 – 0.9)
* **Observation:** Glacier area has consistently decreased across the decade (2014–2023).
* **Visualization:** Year-wise RGB frames and animated GIF depict the spatial retreat pattern.

---

## 🖼️ Visualization Highlights

* **RGB Animation:** `animation.gif` shows glacier color and texture variation over 10 years, offering a realistic temporal progression.
* **Segmentation Comparisons:** Each frame includes the original RGB image, ground-truth mask, and predicted mask for clarity.
* **Matplotlib Plots:** Display year-wise area decline and IoU trend.

---

## 💡 Key Takeaways

* **Segmentation > Thresholding:** Even for binary masks, deep segmentation models capture context and spectral nuances that grayscale thresholds miss.
* **Consistent Monitoring:** Using GEE and UNet provides a scalable pipeline for tracking glacier retreat worldwide.
* **Visualization Matters:** Animations and realistic RGB renders improve public understanding of climate change impacts.

---

## 🧭 How to Run (Notebooks)

1. Open in **Google Colab**:
   [Data Preparation Notebook](https://colab.research.google.com/drive/19hFVgRjUXIXgkYUXt1844N56K4XTRrqx)
   [Model and Deployment Notebook](https://colab.research.google.com/drive/1VpTLL5Rf48ebgJcqKQxDMNw_PCotOqg2)

2. Authenticate Google Earth Engine when prompted.

3. Ensure `segmentation_models_pytorch`, `rasterio`, `geemap`, and `GDAL` are installed.

4. Run each cell sequentially to reproduce the workflow.

---

## 📚 References

* [USGS Landsat-8 Collection 2 Surface Reflectance Guide](https://www.usgs.gov/landsat-missions/landsat-collection-2-level-2-science-products)
* [Google Earth Engine Python API Docs](https://developers.google.com/earth-engine/python_install)

---

**Prepared by:** *Jinal Vyas*
**Course:** Glacier Change Analysis & Remote Sensing Applications
**Date:** November 2024
