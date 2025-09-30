# Detección de Cambios con Sentinel-1 en Municipios de Casanare y Meta

## Descripción del Proyecto

Este proyecto implementa metodologías avanzadas de detección de cambios usando imágenes de radar Sentinel-1 SAR (Synthetic Aperture Radar) en Google Earth Engine para identificar cambios potencialmente asociados a actividad agrícola en municipios seleccionados de los departamentos de Casanare y Meta, Colombia.

## Área de Estudio

### Municipios Analizados

**Departamento del Meta:**
- Puerto López (código: 50-573)
- Castilla La Nueva (código: 50-150)
- San Carlos de Guaroa (código: 50-680)
- Cabuyaro (código: 50-124)

**Departamento de Casanare:**
- Tauramena (código: 85-410)
- Yopal (código: 85-001)
- Aguazul (código: 85-010)
- Nunchía (código: 85-225)
- Villanueva (código: 85-440)

**Total:** 9 municipios en la región de la Orinoquía colombiana

## Estructura del Proyecto

El proyecto está organizado en 4 notebooks Jupyter secuenciales:

### 1. `01_preparacion_datos.ipynb`
**Preparación de Datos y Definición del Área de Estudio**

- Carga de la capa de municipios del DANE 2023 (GeoPackage)
- Selección y filtrado de municipios objetivo
- Reproyección a WGS84 para compatibilidad con Earth Engine
- Conversión de geometrías a formato Earth Engine
- Definición de parámetros temporales
- Visualización del área de estudio
- Exportación de datos preprocesados

### 2. `02_preprocesamiento_sentinel1.ipynb`
**Preprocesamiento y Filtrado de Imágenes Sentinel-1**

- Acceso a la colección Sentinel-1 GRD en Google Earth Engine
- Filtrado por modo de adquisición (IW), polarización (VV+VH) y órbita
- Análisis de disponibilidad temporal de datos
- Conversión de backscatter a escala logarítmica (dB)
- Cálculo de ratio VV/VH
- Aplicación de filtro de speckle (focal median)
- Creación de composiciones mensuales
- Extracción de estadísticas por municipio

### 3. `03_deteccion_cambios.ipynb`
**Análisis de Detección de Cambios**

- Implementación de múltiples métodos de detección:
  - Análisis de diferencias temporales
  - Análisis de anomalías (Z-scores)
  - Índice Normalizado de Vector de Cambio (NDCV)
- Clasificación de tipos de cambio (5 categorías)
- Estadísticas de cambio por municipio
- Análisis de series temporales
- Visualización de resultados

### 4. `04_visualizacion_interpretacion.ipynb`
**Visualización e Interpretación de Resultados**

- Visualizaciones avanzadas (gráficos estadísticos)
- Mapas temáticos interactivos
- Análisis comparativo por departamento
- Interpretación agrícola contextualizada
- Reporte de síntesis
- Exportación de resultados finales

## Metodología

### Marco Teórico

El proyecto se basa en la metodología de análisis estadístico de cambios en series temporales de Sentinel-1 propuesta por:

- **Canty et al. (2020)**: Statistical analysis of changes in Sentinel-1 time series on the Google Earth Engine
- **Conradsen et al. (2003)**: Test estadístico en distribución compleja de Wishart para detección de cambios en datos SAR polarimétricos

### Datos Utilizados

- **Sensor**: Sentinel-1 A/B (banda C, 5.405 GHz)
- **Producto**: GRD (Ground Range Detected)
- **Modo**: IW (Interferometric Wide swath)
- **Polarizaciones**: VV y VH (dual-pol)
- **Resolución espacial**: 10 metros
- **Resolución temporal**: 6-12 días

### Procesamiento

1. **Preprocesamiento**: Calibración radiométrica, corrección de terreno, filtro de speckle
2. **Composiciones temporales**: Agregación mensual usando mediana
3. **Detección de cambios**: Diferencias entre períodos, NDCV, anomalías
4. **Clasificación**: 5 categorías de cambio según magnitud y dirección

## Requisitos

### Dependencias de Python

```bash
pip install earthengine-api geemap geopandas fiona matplotlib seaborn pandas numpy plotly jupyter
```

### Autenticación de Google Earth Engine

```python
import ee
ee.Authenticate()
ee.Initialize()
```

## Uso

### Ejecución Secuencial

Los notebooks deben ejecutarse en orden:

```bash
jupyter notebook 01_preparacion_datos.ipynb
jupyter notebook 02_preprocesamiento_sentinel1.ipynb
jupyter notebook 03_deteccion_cambios.ipynb
jupyter notebook 04_visualizacion_interpretacion.ipynb
```

### Datos de Entrada

- **Capa de municipios**: `/home/famartinezal/Dropbox/Base/DANE_BASE_2023.gpkg`
  - Layer: `MGN_MPIO_POLITICO`
  - Sistema de referencia: MAGNA-SIRGAS (EPSG:4686)

### Datos de Salida

Todos los resultados se guardan en el directorio `data/`:

- `municipios_seleccionados.gpkg`: Geometrías de municipios
- `parametros.json`: Parámetros del análisis
- `procesamiento_info.json`: Información de procesamiento
- `change_analysis_params.json`: Parámetros de detección de cambios
- `estadisticas_cambio_municipios.csv`: Estadísticas por municipio
- `resultados_finales_con_interpretacion.csv`: Resultados finales
- `municipios_con_resultados.gpkg`: GeoPackage con resultados espaciales
- `resumen_ejecutivo.json`: Resumen en formato JSON
- Gráficos PNG de visualización

## Resultados Principales

### Métricas Calculadas

Para cada municipio se calcula:
- Porcentaje de área con cambios detectados
- Área total con cambios (hectáreas)
- Cambio medio en backscatter VV y VH (dB)
- Magnitud de cambio normalizada (NDCV)
- Interpretación agrícola contextualizada

### Interpretación de Cambios

| Cambio Observado | Interpretación Agrícola |
|------------------|-------------------------|
| Aumento VV y VH | Crecimiento vegetativo, emergencia de cultivos |
| Aumento VV, estable VH | Inundación de campos (preparación arroz) |
| Disminución VV y VH | Cosecha, senescencia, preparación de suelo |
| Alta variabilidad | Rotación de cultivos, gestión activa |
| Cambios abruptos | Eventos climáticos, quemas, mecanización |

## Referencias Bibliográficas (IEEE)

[1] M. J. Canty, A. A. Nielsen, H. Skriver, and K. Conradsen, "Statistical analysis of changes in Sentinel-1 time series on the Google Earth Engine," *Remote Sens.*, vol. 12, no. 1, p. 46, Jan. 2020.

[2] K. Conradsen, A. A. Nielsen, J. Schou, and H. Skriver, "A test statistic in the complex Wishart distribution and its application to change detection in polarimetric SAR data," *IEEE Trans. Geosci. Remote Sens.*, vol. 41, no. 1, pp. 4–19, Jan. 2003.

[3] V. Veloso et al., "Understanding the temporal behavior of crops using Sentinel-1 and Sentinel-2-like data for agricultural applications," *Remote Sens. Environ.*, vol. 199, pp. 415–426, Sep. 2017.

[4] A. Nelson et al., "Towards an operational SAR-based rice monitoring system in Asia: Examples from 13 demonstration sites across Asia in the RIICE project," *Remote Sens.*, vol. 6, no. 11, pp. 10773–10812, Nov. 2014.

[5] ESA, "Sentinel-1 User Handbook," European Space Agency, Tech. Rep. ESA-EOEP-CSCOP-TN-13-0001, 2013.

[6] M. J. Canty, *Image Analysis, Classification and Change Detection in Remote Sensing, with Algorithms for Python*, 4th ed. Boca Raton, FL: CRC Press, 2019.

[7] Google Earth Engine, "Detecting changes in Sentinel-1 imagery," [Online]. Available: https://developers.google.com/earth-engine/tutorials/community/detecting-changes-in-sentinel-1-imagery-pt-1

## Aplicaciones

Este análisis puede ser utilizado para:

- Monitoreo de expansión/retracción de áreas agrícolas
- Identificación de períodos críticos de actividad agrícola
- Apoyo a sistemas de alerta temprana de sequías o inundaciones
- Validación de reportes oficiales de producción agrícola
- Planificación territorial y políticas agrícolas

## Trabajo Futuro

- Validación de campo con datos de cultivos reales
- Fusión con datos Sentinel-2 (óptico)
- Análisis de múltiples años para detectar tendencias
- Implementación de clasificación supervisada con machine learning
- Análisis fenológico vinculado a modelos de crecimiento
- Desarrollo de sistema de monitoreo continuo automatizado

## Autor

Proyecto desarrollado para el análisis de cambios agrícolas en la región de la Orinoquía colombiana.

## Licencia

Este proyecto utiliza datos públicos de:
- Sentinel-1 (ESA/Copernicus)
- DANE Colombia (límites municipales)

---

*Última actualización: 2025-09-30*
