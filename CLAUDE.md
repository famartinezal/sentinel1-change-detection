# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Sentinel-1 SAR change detection project for agricultural monitoring in 9 municipalities across Casanare and Meta departments in Colombia's Orinoquía region. The workflow is implemented as 4 sequential Jupyter notebooks that process satellite imagery through Google Earth Engine to detect and interpret land surface changes potentially related to agricultural activities.

## Critical Dependencies

### Google Earth Engine Authentication
Before running any notebook, authenticate with GEE:
```python
import ee
ee.Authenticate()  # First time only
ee.Initialize()
```

### External Data Source
The project uses Earth Engine assets directly:
- **Municipality FeatureCollection**: `users/geoia/MapasBase/ColMuni`
  - Contains all Colombian municipalities
  - Properties: DPTO_CCDGO, DPTO_CNMBR, MPIO_CCDGO, MPIO_CNMBR, MPIO_NAREA
  - No local GPKG file needed - all data accessed through Earth Engine API

## Workflow Architecture

### Sequential Processing Pipeline
The notebooks MUST be executed in order as each depends on outputs from the previous:

1. **01_preparacion_datos.ipynb** → Generates `data/municipios_seleccionados.gpkg` and `data/parametros.json`
2. **02_preprocesamiento_sentinel1.ipynb** → Generates `data/procesamiento_info.json` and temporal statistics
3. **03_deteccion_cambios.ipynb** → Generates `data/change_analysis_params.json` and change statistics
4. **04_visualizacion_interpretacion.ipynb** → Generates final outputs and reports

### Key Data Flow
```
EE Asset (users/geoia/MapasBase/ColMuni) → Notebook 01 → data/parametros.json
                                                       (includes ee_asset and codigos_municipios)

parametros.json → Notebook 02 → data/procesamiento_info.json
EE municipios                → Sentinel-1 collection (recreated in memory)

parametros.json → Notebook 03 → data/change_analysis_params.json
EE municipios                → data/estadisticas_cambio_municipios.csv

All previous files → Notebook 04 → Final visualizations & reports
```

### In-Memory vs Persisted Collections
**Important**: Sentinel-1 image collections are NOT exported to disk. They are recreated from scratch in notebooks 02, 03, and 04 using identical filtering logic. The processing pipeline functions (`process_sentinel1_collection`, `to_dB`, `apply_speckle_filter`) must be replicated across notebooks that need the collection.

## Municipality Selection

The project analyzes exactly 9 municipalities using MPIO_CCDGO codes from Earth Engine:
- **Meta**: Puerto López (50573), Castilla La Nueva (50150), San Carlos DE Guaroa (50680), Cabuyaro (50124)
- **Casanare**: Tauramena (85410), Yopal (85001), Aguazul (85010), Nunchía (85225), Villanueva (85440)

**Implementation**:
```python
codigos_municipios = ['50573', '50150', '50680', '50124', '85410', '85001', '85010', '85225', '85440']
municipios_filtrados = ee.FeatureCollection('users/geoia/MapasBase/ColMuni').filter(
    ee.Filter.inList('MPIO_CCDGO', codigos_municipios)
)
```

## Change Detection Methodology

The project implements 3 complementary change detection methods:

1. **Temporal Differences**: Direct subtraction between reference and target periods
   - Outputs: `diff_VV`, `diff_VH` in dB
   - Thresholds: Strong change >3dB, moderate >1.5dB

2. **Anomaly Detection**: Z-score analysis against time series mean/std
   - Threshold: |Z| > 2 (95% confidence)
   - Outputs: `z_score_VV`, `z_score_VH`, binary anomaly masks

3. **NDCV (Normalized Difference Change Vector)**:
   - Formula: |target - reference| / (target + reference) in linear scale
   - Threshold: NDCV > 0.3 indicates significant change
   - Outputs: `NDCV_VV`, `NDCV_VH`, `NDCV_combined`

### Change Classification
5 classes based on VV backscatter difference:
- 0: No change (|ΔVV| < 1.5 dB)
- 1: Strong increase (ΔVV > 3 dB) → Possible vegetation growth, flooding
- 2: Strong decrease (ΔVV < -3 dB) → Possible harvest, soil preparation
- 3: Moderate increase (1.5-3 dB)
- 4: Moderate decrease (-3 to -1.5 dB)

## SAR Processing Details

### Sentinel-1 Filtering Criteria
```python
.filter(ee.Filter.eq('instrumentMode', 'IW'))  # Interferometric Wide swath only
.filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VV'))
.filter(ee.Filter.listContains('transmitterReceiverPolarisation', 'VH'))
.filter(ee.Filter.eq('orbitProperties_pass', orbit_type))  # Either ASCENDING or DESCENDING
```

**Critical**: The code automatically selects the orbit direction (ascending/descending) with more available images for consistency in geometry.

### Speckle Filtering
Uses focal median with 7×7 kernel (radius=3 pixels):
```python
kernel = ee.Kernel.square(radius=3, units='pixels')
image.select('VV').focal_median(kernel=kernel)
```

### dB Conversion
Always applied to both VV and VH polarizations:
```python
vv_db = ee.Image(10).multiply(vv_linear.log10())
```

## Common Development Commands

### Running Notebooks
```bash
# Sequential execution
jupyter notebook 01_preparacion_datos.ipynb
jupyter notebook 02_preprocesamiento_sentinel1.ipynb
jupyter notebook 03_deteccion_cambios.ipynb
jupyter notebook 04_visualizacion_interpretacion.ipynb
```

### Checking Data Directory
```bash
ls -lh data/  # All outputs stored here
```

## Output Files Reference

### Intermediate Files (in `data/`)
- `municipios_seleccionados.gpkg`: Selected municipalities in WGS84
- `parametros.json`: Date ranges, AOI centroid, bounding box
- `procesamiento_info.json`: Orbit type, image count, processing parameters
- `change_analysis_params.json`: Reference/target periods, thresholds

### Final Outputs (in `data/`)
- `estadisticas_cambio_municipios.csv`: Per-municipality change statistics
- `resultados_finales_con_interpretacion.csv`: With agricultural interpretation
- `municipios_con_resultados.gpkg`: Spatial layer with change metrics
- `resumen_ejecutivo.json`: Executive summary in JSON format
- `*.png`: Visualization outputs (temporal distribution, change maps, etc.)

## Modifying Analysis Parameters

### Changing Date Ranges
**Current analysis period: Second semester 2025**

Edit in notebook 01:
```python
fecha_inicio = '2025-01-01'
fecha_fin = '2025-09-30'
```

Then in notebook 03, define reference and target periods:
```python
reference_start = '2025-01-01'  # First semester 2025 (reference)
reference_end = '2025-06-30'
target_start = '2025-07-01'     # Second semester 2025 (analysis)
target_end = '2025-09-30'
```

### Adjusting Change Detection Thresholds
In notebook 03:
```python
strong_threshold = 3      # Strong change in dB
moderate_threshold = 1.5  # Moderate change in dB
ndcv_threshold = 0.3      # NDCV significance threshold
```

## Agricultural Context

The Orinoquía region has:
- **Main crops**: Rice (with flooding), maize, oil palm, soy, pastures
- **Rainfall seasons**: April-May and October-November
- **Crop cycles**: Short (3-4 months) and permanent crops

### SAR Backscatter Interpretation for Agriculture
- **VV increase + VH increase**: Vegetation growth, crop emergence
- **VV strong increase, VH stable**: Field flooding (typical rice preparation)
- **VV decrease + VH decrease**: Harvest, senescence, soil preparation
- **High temporal variability**: Crop rotation, active management

## Working with Earth Engine FeatureCollections

The project uses Earth Engine FeatureCollections directly - no GeoPandas conversion needed:

```python
# Load and filter municipalities
municipios_col = ee.FeatureCollection('users/geoia/MapasBase/ColMuni')
municipios_filtrados = municipios_col.filter(
    ee.Filter.inList('MPIO_CCDGO', codigos_municipios)
)

# Create unified AOI
aoi = municipios_filtrados.geometry()

# Extract statistics by municipality
features_list = municipios_filtrados.toList(municipios_filtrados.size())
for i in range(n_municipios):
    feature = ee.Feature(features_list.get(i))
    geom = feature.geometry()
    props = feature.toDictionary().getInfo()
    # ... process statistics
```

## References Format

All references follow IEEE citation style. Key papers:
- Canty et al. (2020) - Sentinel-1 time series change detection on GEE
- Conradsen et al. (2003) - Wishart distribution test for polarimetric SAR
- Canty (2019) book - "Image Analysis, Classification and Change Detection in Remote Sensing"

## Troubleshooting

### "Earth Engine not initialized"
Run `ee.Authenticate()` then `ee.Initialize()` in the first cell.

### "Asset not found: users/geoia/MapasBase/ColMuni"
Ensure you have access to this Earth Engine asset or update the `ee_asset` parameter to point to your own municipality FeatureCollection.

### "No images found for orbit"
Adjust date range or check Sentinel-1 coverage for your AOI. The code automatically selects the orbit with more images.

### "parametros.json not found" in notebook 02+
Execute notebook 01 first to generate the parameters file with municipality codes and date ranges.

### Memory errors during statistics extraction
Reduce `maxPixels` parameter in `reduceRegion()` calls or process municipalities individually in a loop.
