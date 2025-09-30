# Repository Guidelines

## Project Structure & Module Organization
The analysis is driven by four sequential notebooks in the repository root: `01_preparacion_datos.ipynb`, `02_preprocesamiento_sentinel1.ipynb`, `03_deteccion_cambios.ipynb`, and `04_visualizacion_interpretacion.ipynb`. Each notebook writes intermediate artifacts into `data/`, which is the hand-off location for parameters, statistics, and exported GeoPackages. Supplementary one-off studies live alongside the main notebooks (`sentinel1_cambios_completo.ipynb`, `sentinel1_change_detection_complete.ipynb`). Keep new notebooks prefixed with a zero-padded order number to preserve execution order.

## Build, Test & Notebook Execution
Create an isolated environment and install dependencies with:
```bash
python -m venv .venv && source .venv/bin/activate
pip install earthengine-api geemap geopandas fiona matplotlib seaborn pandas numpy plotly jupyter
```
Before opening any notebook, authenticate Google Earth Engine once per session:
```python
import ee
try:
    ee.Initialize()
except Exception:
    ee.Authenticate()
    ee.Initialize()
```
Execute the notebooks sequentially using either JupyterLab or `jupyter notebook`, verifying that each run completes before advancing.

## Coding Style & Naming Conventions
Follow PEP 8 defaults with 4-space indentation. Imports must appear in the order: standard library, scientific (`numpy as np`, `pandas as pd`), geospatial (`ee`, `geemap`, `geopandas as gpd`), then visualization (`matplotlib.pyplot as plt`, plotly modules). Use snake_case for variables and functions, mixing Spanish terms for geographic concepts (`municipios_objetivo`) with English for processing terminology (`change_collection`). Keep notebooks concise by modularizing repetitive logic into functions or helper cells.

## Testing & Validation
There is no automated test suite; treat validation as part of notebook execution. After each major processing step, log key dataframe shapes, descriptive statistics for backscatter values, and sample map outputs to confirm spatial alignment. Regenerate summary CSVs in `data/` and compare row counts or key metrics against prior runs before publishing updates.

## Commit & Pull Request Guidelines
Existing history uses short, imperative commit subjects (e.g., "Add consolidated notebook"). Continue this tone, referencing affected notebooks or data products when relevant. When opening a pull request, add a succinct summary of methodological changes, list the notebooks executed, note any updates to input datasets, and attach representative plots or maps if visuals changed. Link issues or research notes when available so reviewers can trace decisions.
