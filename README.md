---

# NDVILand: A Dataset of NDVI-Enhanced EuroSAT Satellite Images for Land Use

## Project Overview

The NDVILand dataset is a structured, multi-class geospatial dataset designed for satellite imagery-based surface characterization, vegetation index tracking, and multi-terrain analysis. The dataset addresses traditional computational processing bottlenecks by organizing multi-spectral data into a structure optimized for parallel, distributed cluster environments like Apache Spark. It serves as a reproducible foundation for precision land use/cover classification, distributed big data benchmarking, and downstream machine learning segmentation tasks.

## Dataset Specifications

 * **Total Image Count:** 27,000+ geo-referenced image patches.


* **Resolution Layout:** Uniform 64 × 64 pixels per image patch.


* **Spatial Grid Sampling:** 10 meters per pixel ground sampling distance.


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

NDVI_LAND_DATASET/                                       # Main dataset parent directory
│
├── Real Satellite Images/                               # Source multispectral satellite image files
│     ├── AnnualCrop/
│     ├── Forest/
│     ├── Highway/
│     └── ...
│
├── NDVI images/                                         # Processed output maps rendered in RdYlGn spectrum
│     ├── AnnualCrop/
│     ├── Forest/
│     ├── Highway/
│     └── ...
│
README.md                                                # Project documentation file
metadata.csv                                             # Metadata file
notebook.ipynb                                           # Main pipeline deployment logic script

```

## Technical Features

The images in this repository are pre-configured to target specific electromagnetic spectral windows essential for biophysical evaluations:

* **Band 04 (Visible Red, 665 nm):** 10m resolution channel used to capture peak chlorophyll absorption.


* **Band 08 (Near-Infrared, 842 nm):** 10m resolution channel used to capture terrain and leaf mesophyll back-scattering.
  

These target bands allow for the automated calculations of the Normalized Difference Vegetation Index (NDVI):

$$\text{NDVI} = \frac{\rho_{\text{B08}} - \rho_{\text{B04}}}{\rho_{\text{B08}} + \rho_{\text{B04}}}$$

Where:

$\rho_{\text{B04}}$ denotes Red reflectance.

$\rho_{\text{B08}}$ denotes Near-Infrared reflectance.

Note: Digital numbers (DN) are converted to Bottom-of-Atmosphere (BOA) reflectance by dividing by 10,000.

The theoretical NDVI range is: $-1 \le \text{NDVI} \le 1$

For visualization purposes, NDVI images are rendered using the RdYlGn colormap with the following constraints to improve contrast and highlight non-vegetated regions:

vmin = -0.26

vmax = 1.0

## Dataset Metadata

The repository includes a comprehensive metadata file (`metadata.csv`) to facilitate data filtering and analysis. It contains the following fields:

* **Image path:** The relative path to the stored image.
* **Land use class:** The categorized land cover type.
* **Mean NDVI:** The average Normalized Difference Vegetation Index value for the image.
* **Standard deviation of NDVI:** The spatial variability of vegetation health within the image.
* **Minimum NDVI:** The lowest recorded NDVI value.
* **Maximum NDVI:** The highest recorded NDVI value.

## Processing Pipeline

The dataset generation pipeline is fully implemented in `notebook.ipynb` utilizing a robust geospatial and big data stack:

* **Core Languages & Libraries:** Python, NumPy, Rasterio, Matplotlib
* **Distributed Computing:** Apache Spark (PySpark)

### Workflow Steps
1. **Data Loading:** Ingesting raw Sentinel-2 satellite imagery.
2. **Band Extraction:** Isolating Band 4 (Red) and Band 8 (Near-Infrared).
3. **NDVI Computation:** Calculating vegetation indices at the pixel level.
4. **Visualization Generation:** Producing both standard RGB satellite images and false-color NDVI visualizations.
5. **Statistical Analysis:** Computing image-level statistics (Mean, SD, Min, Max).
6. **Data Export:** Generating the `metadata.csv` file and organizing the processed images into structured, class-wise directories.

## Getting Started

The dataset processing scripts are built using Python 3.10+. Key developer software tool dependencies include:

  * `pyspark` (For distributed data mapping over RDD structures).


 
  * `rasterio` (For native uncompressed 16-bit GeoTIFF raster I/O handling).


  * `numpy` (For vectorized pixel matrix equations and validation filtering).



## Citation

If you utilize this dataset layout or the accompanying PySpark processing code within your research, please cite this repository:

```text
Chauhan, Sanjay & Kumar M, Dhinesh. (2026). NDVILand: A Dataset of NDVI-Enhanced EuroSAT Satellite Images for Land Use. Zenodo. https://doi.org/10.5281/zenodo.20777578

```
