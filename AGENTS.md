# Agent Guidelines

## Project Structure
- The workflow consists of four sequential Jupyter notebooks in the root directory.
- Execute them in order: `01_...` to `04_...`.
- The `data/` directory is used for all intermediate and final data.
- New notebooks must maintain the zero-padded prefix for clear execution order.

## Development Commands
- **Setup:** `python -m venv .venv && source .venv/bin/activate`
- **Install:** `pip install earthengine-api geemap geopandas fiona matplotlib seaborn pandas numpy plotly jupyter ruff`
- **Run:** `jupyter lab` or `jupyter notebook`
- **Lint:** `ruff check .` or `ruff format .` to check and format code within notebooks.
- **Test:** Notebook execution serves as the test suite. Validate outputs (e.g., dataframe shapes, stats) after major processing steps.

## Coding Style
- **Formatting:** Follow PEP 8 with 4-space indentation.
- **Imports:** Organize in groups: standard library, scientific (`numpy as np`), geospatial (`geopandas as gpd`), and visualization.
- **Naming:** Use snake_case. Mix Spanish geography terms with English processing tokens (e.g., `municipios_objetivo`, `change_collection`).
- **Error Handling:** Use try-except blocks for I/O and API calls.
- **Types:** Use type hints for function signatures where possible.

## Authentication
- Authenticate Google Earth Engine at the start of each session:
  ```python
  import ee
  try:
      ee.Initialize()
  except Exception:
      ee.Authenticate()
      ee.Initialize()
  ```
