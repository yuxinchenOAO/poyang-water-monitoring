# Multitemporal Surface Water Monitoring of Poyang Lake with Sentinel-2

This repository contains the code for the Earth Observation Advanced final project: mapping the seasonal surface-water extent of Poyang Lake, China, from Sentinel-2 imagery in Google Earth Engine, and comparing three water-extraction methods — NDWI (Otsu) thresholding, Random Forest and Support Vector Machine — through accuracy assessment and water-area change detection over 2016–2020.

## Requirements

- A Google account with access to Google Earth Engine.
- A Google Cloud project with the Earth Engine API enabled (non-commercial / academic use).
- The notebook is intended to run in Google Colab; the required Python packages (`earthengine-api`, `geemap`, `geopandas`) are installed in the first cell.

## Usage

1. Open `poyang_lake_water_monitoring.ipynb` in Google Colab.
2. In the initialisation cell (Section 0), set `ee.Initialize(project="...")` to a Google Cloud project id with the Earth Engine API enabled.
3. Run the cells in order. All tunable parameters (area of interest, years, season months, spectral indices, classifier hyperparameters) are centralised in the `CONFIG` block in Section 1.

## Outputs

- `accuracy_assessment.csv` — per year/season/method accuracy metrics (OA, precision, recall, F1, Cohen's kappa).
- `water_area_timeseries.csv` — open-water area (km²) per year and season for the three methods.
- `seasonal_expansion.csv` — wet-minus-dry area per year.
- `accuracy_comparison.png`, `water_extent_timeseries.png` — summary figures.

## Method notes

- Cloud masking uses the Sentinel-2 `s2cloudless` cloud-probability product.
- Optical bands are rescaled to [0, 1] before classification, which is required for the SVM to perform comparably to Random Forest.
- Reference labels are derived from the JRC Global Surface Water Yearly History product, using permanent water only as the positive class to keep the training target stable across seasons.
- The 2018 wet-season composite is affected by heavy cloud cover and is excluded from the area-based trend and seasonal-expansion analysis.

## Study period

The study uses 2016–2020, within the temporal coverage of the JRC yearly reference product.

## Repository contents

- `poyang_lake_water_monitoring.ipynb` — the full Google Earth Engine / Python pipeline.
- `results/` — output figures and tables produced by the notebook (accuracy comparison, water-area time series, study area, per-method water maps, and the CSV metrics).
