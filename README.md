---

# NDVILand: A Dataset of NDVI-Enhanced EuroSAT Satellite Images for Land Use

## Project Overview

The NDVILand dataset is a structured, multi-class geospatial dataset designed for satellite imagery-based surface characterization, vegetation index tracking, and multi-terrain analysis. The dataset addresses traditional computational processing bottlenecks by organizing multi-spectral data into a structure optimized for parallel, distributed cluster environments like Apache Spark. It serves as a reproducible foundation for precision land use/cover classification, distributed big data benchmarking, and downstream machine learning segmentation tasks.

## Dataset Specifications

 
* **Total Image Count:** 27,000+ geo-referenced image patches.


* **Resolution Layout:** Uniform 64 × 64 pixels per image patch.


* **Spatial Grid Sampling:** 10 meters per pixel ground sampling distance.

* **Data Format:** Raw, uncompressed 16-bit GeoTIFF format to preserve complete sensor radiometric precision.

* **Total Data Volume:** Approximately 1.93 GB.


* **Data Source Origin:** Derived from the European Space Agency's (ESA) Sentinel-2 multi-spectral satellite instrument collection (*EuroSATallBands* variant).


## Target Land Use Categories

The dataset features a balanced representation across 10 distinct terrain types, evaluating 500 unique ground locations per image class:

* **Forest (3,000 samples):** Dense tree canopies showcasing peak chlorophyll reflection.


* **Annual Crop (3,000 samples):** Active, seasonal agricultural crop fields.


* **Residential (3,000 samples):** Suburban housing areas mixing built concrete infrastructure with green plots.


* **Industrial (2,500 samples):** High-density commercial footprints, manufacturing warehouses, and factories.


* **Highway (2,500 samples):** Impervious asphalt transit corridors and major roadways.

* **Sea Lake (2,500 samples):** Open inland/coastal water bodies showcasing high near-infrared absorption.


* **Remaining Categories:** Includes balanced selections for *Permanent Crops*, *Herbaceous Vegetation*, *Pastures*, and *Rivers* to capture comprehensive landscape heterogeneity.



## Repository Architecture

The repository coordinates data handling through the following file layout:

```text
├── data/
│   └── EuroSATallBands/             # Class-based image subdirectories
│       ├── Forest/                  # 16-bit GeoTIFF files (64x64 pixels)
│       ├── Industrial/              # 16-bit GeoTIFF files (64x64 pixels)
│       ├── Highway/                 # 16-bit GeoTIFF files (64x64 pixels)
│       └── [Remaining Classes]/     # Additional target terrain categories
├── notebooks/
│   └── PySpark_NDVI_Pipeline.ipynb # Code deployment logic for distributed band extraction
└── validation_plots/                # Sample visualization maps rendered in RdYlGn spectrum

```

## Technical Features

The images in this repository are pre-configured to target specific electromagnetic spectral windows essential for biophysical evaluations:

* **Band 04 (Visible Red, 665 nm):** 10m resolution channel used to capture peak chlorophyll absorption.


* **Band 08 (Near-Infrared, 842 nm):** 10m resolution channel used to capture terrain and leaf mesophyll back-scattering.
* 

These target bands allow for the automated calculations of the Normalized Difference Vegetation Index (NDVI):

$$\text{NDVI} = \frac{\rho_{\text{B08}} - \rho_{\text{B04}}}{\rho_{\text{B08}} + \rho_{\text{B04}}}$$

Where $\rho$ scales raw sensor Digital Numbers ($\text{DN}$) to normalized Bottom-Of-Atmosphere (BOA) reflectance values decimal spaces ranging between 0.0 and 1.0.

## Getting Started

The dataset processing scripts are built using Python 3.10+. Key developer software tool dependencies include:

* 
`pyspark` (For distributed data mapping over RDD structures).


* 
`rasterio` (For native uncompressed 16-bit GeoTIFF raster I/O handling).


* 
`numpy` (For vectorized pixel matrix equations and validation filtering).



## Citation

If you utilize this dataset layout or the accompanying PySpark processing code within your research, please cite this repository:

```text
Chauhan, S., & Dhinesh Kumar, M. (2026). Satellite-Based Geospatial Characterization using NDVI. GitHub. https://github.com/Sanjay-Chauhan52/Satellite-Based-Geospatial-Characterization-using-NDVI

```
