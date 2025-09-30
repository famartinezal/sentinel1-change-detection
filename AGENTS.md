# AGENTS.md - Development Guidelines

## Build/Test Commands
- **No formal test suite**: This is a Jupyter notebook-based geospatial analysis project
- **Sequential execution required**: Run notebooks in order: `01_preparacion_datos.ipynb` → `02_preprocesamiento_sentinel1.ipynb` → `03_deteccion_cambios.ipynb` → `04_visualizacion_interpretacion.ipynb`
- **Dependencies**: `pip install earthengine-api geemap geopandas fiona matplotlib seaborn pandas numpy plotly jupyter`
- **Google Earth Engine auth required**: Run `ee.Authenticate()` then `ee.Initialize()` before any notebook execution

## Code Style Guidelines

### Imports
- **Order**: Standard library → Scientific (numpy, pandas) → Geospatial (ee, geemap, geopandas) → Visualization (matplotlib, plotly)
- **Standard aliases**: `import numpy as np`, `import pandas as pd`, `import geopandas as gpd`, `import matplotlib.pyplot as plt`
- **Earth Engine pattern**: Always use `import ee` and handle auth with try/except block

### Naming Conventions
- **Variables**: snake_case with descriptive names (`municipios_seleccionados`, `change_params`)
- **Functions**: snake_case with clear purpose (`extract_change_stats`, `process_sentinel1_collection`)
- **Mixed language**: Spanish for domain concepts (municipios, departamento), English for technical terms (collection, geometry)

### Error Handling
- **Earth Engine auth pattern**: Use try/except for `ee.Initialize()` with fallback to `ee.Authenticate()`
- **Minimal explicit error handling**: Rely on library defaults, use print statements for status feedback
- **Data validation**: Check shapes, sizes, and summary statistics rather than formal exception handling