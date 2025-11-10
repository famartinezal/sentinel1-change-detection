# Mosaicos Sentinel-2 Libres de Nubes - Google Colab

## Descripción

Este notebook permite generar mosaicos ópticos libres de nubes utilizando imágenes Sentinel-2 para cualquier conjunto de municipios en Colombia (o cualquier región).

## ¿Cómo usar?

### 1. Abrir en Google Colab

Haz clic en el badge de Colab en el notebook o usa este enlace:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/famartinezal/sentinel1-change-detection/blob/main/05_mosaicos_sentinel2_sin_nubes.ipynb)

### 2. Ejecutar celdas en orden

1. **Celda 1**: Copyright (solo informativo)
2. **Celda 2**: Autenticación de Google Earth Engine - Sigue las instrucciones en pantalla
3. **Celda 3**: Instalación de librerías (geemap, folium)
4. **Celda 4**: Subir archivo de municipios
5. **Celda 5**: Configurar fechas y parámetros
6. **Celdas siguientes**: Ejecutar secuencialmente

### 3. Preparar tu archivo de municipios

Puedes usar cualquier formato vectorial:

- **GeoPackage** (.gpkg) - Recomendado
- **Shapefile** (.shp + .shx + .dbf + .prj)
- **GeoJSON** (.geojson)

**Requisitos:**
- Sistema de coordenadas: WGS84 (EPSG:4326) o cualquier otro (se reproyecta automáticamente)
- Geometrías: Polígonos
- Campos sugeridos (nombres flexibles):
  - Nombre del municipio: `MPIO_CNMBR`, `NOMBRE`, `nombre`
  - Código: `MPIO_CCDGO`, `CODIGO`, `codigo`
  - Departamento: `DPTO_CNMBR`, `DEPARTAMENTO`, `departamento`

### 4. Configurar parámetros (Celda 5)

```python
# Fechas del análisis
fecha_inicio = '2024-01-01'
fecha_fin = '2024-12-31'

# Parámetros de enmascaramiento de nubes
CLOUD_FILTER = 60        # Cobertura nubosa máxima (%)
CLD_PRB_THRESH = 40      # Umbral de probabilidad de nube (%)
NIR_DRK_THRESH = 0.15    # Umbral NIR para sombras
CLD_PRJ_DIST = 2         # Distancia proyección sombras (km)
BUFFER = 100             # Buffer dilatación máscaras (m)
```

### 5. Visualizar resultados

Después de generar los mosaicos, usa:

```python
# Ver mosaico de un municipio específico
mapa = crear_mapa_municipio('CODIGO_MUNICIPIO')
display(mapa)
```

El mapa incluye capas interactivas:
- **RGB** (True Color)
- **NIR** (False Color)
- **NDVI** (Índice de Vegetación)
- **NDWI** (Índice de Agua)

### 6. Descargar resultados

El notebook descarga automáticamente un CSV con estadísticas:
- `estadisticas_mosaicos_sentinel2.csv`: Número de imágenes por municipio

## Interpretación de Índices

### NDVI (Índice de Vegetación)
- **0.6 - 0.8**: Vegetación densa
- **0.3 - 0.6**: Pasturas, cultivos en desarrollo
- **< 0.3**: Suelo desnudo, áreas urbanas

### NDWI (Índice de Agua)
- **Positivo**: Agua superficial, campos inundados
- **Negativo**: Suelo seco, vegetación

## Solución de Problemas

### Error: "No se encontraron imágenes"
- Verifica las fechas (formato YYYY-MM-DD)
- Aumenta `CLOUD_FILTER` a 80 o 100
- Verifica que el área de estudio tenga cobertura Sentinel-2

### Error al cargar archivo
- Asegúrate de subir TODOS los archivos del shapefile (.shp, .shx, .dbf, .prj)
- Para GeoPackage, solo necesitas el archivo .gpkg
- Verifica que el archivo contenga polígonos válidos

### Procesamiento muy lento
- Reduce el período temporal
- Procesa menos municipios a la vez
- Aumenta `CLOUD_FILTER` para filtrar más imágenes

## Créditos

Basado en el tutorial oficial de Google Earth Engine:
- [Sentinel-2 Cloud Masking with s2cloudless](https://developers.google.com/earth-engine/tutorials/community/sentinel-2-s2cloudless)

Autor original: jdbcode  
Adaptación: famartinezal
