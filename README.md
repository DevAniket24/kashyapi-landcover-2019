# Land cover at the Kashyapi Dam reservoir edge, Nashik (2019)

Assignment Q1: a reproducible land-cover classification of a 3 km² area (12 cells of 500 m), compared with Dynamic World and Copernicus CGLS-LC100 (2019).
Author: Aniket Sawargaonkar · October 2026

## Files, in the order they are used

| No. | File | What it is |
|-----|------|------------|
| 00 | `00_training_polygons_v3.geojson` | Input: 120 training squares (20 per class), all outside the study grid |
| 01 | `01_landcover_classification.ipynb` | Notebook 1: grid, Sentinel-2 composites (two seasons), image chips, random forest classification |
| 02 | `02_classification_stage1_outputs.zip` | Output of notebook 1, cell 10: grid, chips, composites, valid-data counts (a subset of file 03) |
| 03 | `03_classification_outputs.zip` | Output of notebook 1, cell 18: everything in 02 plus the random forest results. Input to notebook 04 |
| 04 | `04_comparison_and_sensitivity.ipynb` | Notebook 2: Dynamic World and CGLS comparison, agreement statistics, diagnosis cells, sensitivity test |
| 05 | `05_final_outputs.zip` | Output of notebook 2: all results (contents of 03 plus every comparison output) |
| 06 | `06_presentation.pptx` | Presentation slides |

## How to reproduce the results

You need a Google account with access to Google Earth Engine (a Cloud project registered for Earth Engine).

1. Open `01_landcover_classification.ipynb` in Google Colab.
2. In cell 2, set `EE_PROJECT` to your own Earth Engine project. Change nothing else.
3. Upload `00_training_polygons_v3.geojson` to the Colab file panel (or upload it when cell 13 asks).
4. Run all cells in order. Sign in to Earth Engine when cell 3 asks. The notebook downloads `02_classification_stage1_outputs.zip` (cell 10) and `03_classification_outputs.zip` (cell 18).
5. Open `04_comparison_and_sensitivity.ipynb` in Colab. Set `EE_PROJECT` in cell 2.
6. Upload `03_classification_outputs.zip` (or upload it when cell 4 asks).
7. Run cells in this order: 1–8, then 8c, 8d, 8e, 8f, then 8b, then 9 and 10. The notebook downloads `05_final_outputs.zip`.

All settings are in cell 2 of each notebook. Random seed: 2019. Library versions: Python 3.13, earthengine-api 1.7.39, scikit-learn 1.6.1, rasterio 1.5.2, numpy 2.1.3.

## Key files inside `05_final_outputs.zip`

| File | Contents |
|------|----------|
| `comparison_cell_labels.csv` | One row per cell: visual label, random forest, Dynamic World and CGLS labels, class shares, valid pixels, uncertainty, agreement flags |
| `comparison_agreement_summary.csv`, `agreement_summary_extended.csv` | Agreement counts with denominators and 95% Wilson intervals |
| `grid_cells.geojson`, `aoi_boundary.geojson` | The 12 cells (C01–C12) and the study-area boundary |
| `chips/`, `chips_febmar/` | One RGB image per cell for Oct–Dec 2019 and Feb–Mar 2019 |
| `comparison_figure.png`, `diagnosis_C02.png`, `diagnosis_C10.png` | Main figure and the two diagnosis panels |
| `sensitivity_before_after.csv`, `sensitivity_summary.json` | Sensitivity test (Oct–Dec only), with the original results kept |
| `run_log.json`, `comparison_log.json` | Every setting, Sentinel-2 image ID and software version |


