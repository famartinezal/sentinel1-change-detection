

# **Plan de Monitoreo de Cambios Agrícolas en los Llanos Orientales con Imágenes Satelitales de Radar**

## **1\. Introducción al Monitoreo Agrícola con Tecnología Radar**

### **1.1. El Desafío: Nubes en los Llanos Orientales**

Los Llanos Orientales de Colombia son una región agrícola de gran importancia, con extensos cultivos de arroz, soya y palma de aceite.1 Monitorear estas áreas es fundamental para la planificación, la seguridad alimentaria y el cuidado del medio ambiente.

Sin embargo, existe un gran desafío: la constante presencia de nubes. Durante gran parte del año, las nubes impiden que los satélites ópticos tradicionales (similares a una cámara fotográfica) tomen imágenes claras de la superficie.4 Esto crea vacíos de información que dificultan el seguimiento continuo de los cultivos.

### **1.2. La Solución: El Satélite Sentinel-1**

Para superar este obstáculo, se propone el uso de la tecnología de Radar de Apertura Sintética (SAR), específicamente del satélite Sentinel-1. Este tipo de satélite no depende de la luz solar y sus señales de radar pueden atravesar las nubes, lo que permite obtener imágenes de día o de noche y sin importar las condiciones climáticas.5 Gracias a que Sentinel-1 captura imágenes de la misma zona cada 6 a 12 días, es posible construir una secuencia temporal detallada para observar la evolución de los campos.

### **1.3. Objetivos del Monitoreo**

El objetivo principal es diseñar e implementar un sistema en la plataforma Google Earth Engine (GEE) para detectar, medir y analizar los cambios en las áreas agrícolas de los Llanos Orientales, utilizando las imágenes del satélite Sentinel-1.

Este plan se enfocará en responder a las siguientes preguntas:

1. ¿Cuál es la mejor manera de preparar las imágenes de Sentinel-1 para que sean consistentes y comparables a lo largo del tiempo?  
2. ¿Qué método es más eficaz para detectar cambios agrícolas (como preparación del suelo, siembra o crecimiento inicial) cuando aún no se ha completado el ciclo del cultivo?  
3. ¿Cómo se pueden interpretar los cambios detectados para entender qué actividades agrícolas están ocurriendo en los cultivos de arroz, soya y palma de aceite?

### **1.4. Área de Estudio**

El monitoreo se centrará en municipios clave de los departamentos de Meta (Puerto López, Castilla la Nueva, San Carlos de Guaroa, Cabuyaro) y Casanare (Tauramena, Yopal, Aguazul, Nunchía, Villanueva). Esta selección abarca la diversidad de los sistemas productivos de la región.

## **2\. Preparación de los Datos Satelitales en Google Earth Engine**

Para garantizar un análisis fiable, el primer paso es procesar y estandarizar todas las imágenes de Sentinel-1. Este proceso asegura que los cambios detectados correspondan a actividades reales en el terreno y no a variaciones técnicas.

### **2.1. Creación de una Colección de Datos Consistente**

* **Fuente de Datos:** Se utilizará la colección de imágenes COPERNICUS/S1\_GRD de Google Earth Engine, que contiene datos de intensidad de la señal de radar.  
* **Periodo de Análisis:** Se definirá un periodo de estudio desde 2017 hasta la fecha actual para capturar la dinámica de varios años y establecer una base de comparación sólida.  
* **Consistencia Geométrica:** Un paso fundamental es seleccionar imágenes de una única dirección orbital (ascendente o descendente). Esto asegura que el satélite observe el terreno desde un ángulo similar en cada pasada, reduciendo variaciones que no están relacionadas con cambios en los cultivos.17

### **2.2. Pasos del Preprocesamiento en GEE**

Se aplicará una secuencia de correcciones a cada imagen para mejorar su calidad y precisión:

1. **Aplicación de Archivos de Órbita:** Se refina la geolocalización de cada imagen para asegurar que todas estén perfectamente alineadas.  
2. **Eliminación de Ruido Térmico:** Se corrige el ruido en los bordes de las imágenes, que puede afectar la calidad de la medición.  
3. **Calibración Radiométrica:** Los valores de las imágenes se convierten a un coeficiente de retrodispersión (![][image1]), una medida física que representa la reflectividad del terreno. Para el análisis, estos valores se suelen expresar en decibelios (dB).  
4. **Filtrado de Ruido "Speckle":** Las imágenes de radar tienen un ruido inherente con apariencia de "sal y pimienta" (conocido como *speckle*), que se debe a la naturaleza de la señal de microondas.9 Este ruido se modela como un ruido multiplicativo que sigue una distribución Gamma.12 Se aplicará un filtro para suavizar este ruido y hacer más visibles los patrones reales de los cultivos. Se pueden usar filtros espaciales (que promedian píxeles vecinos) o filtros multi-temporales (que usan información de varias imágenes en el tiempo para reducir el ruido sin perder detalle espacial).  
5. **Corrección del Terreno:** Se utilizan modelos de elevación digital para corregir las distorsiones geométricas causadas por el relieve, como colinas o valles.

## **3\. Métodos para la Detección de Cambios Agrícolas**

Dado que el ciclo completo de los cultivos no está disponible, el enfoque se centrará en detectar cambios significativos entre fechas o anomalías en el comportamiento temporal de la señal de radar.

### **3.1. Método 1: Comparación Directa entre Fechas (Índice Log-Ratio)**

* **Concepto:** Este es el método más directo. Compara dos imágenes, un "antes" y un "después", para resaltar dónde han ocurrido cambios. En lugar de una simple resta, se utiliza el "índice log-ratio", que es una fórmula matemática más robusta para datos de radar.18  
* **Aplicación Práctica:**  
  1. **Selección de Fechas:** Se eligen dos períodos para comparar (por ejemplo, el inicio de un mes contra el final del mismo mes, o el mismo mes en años diferentes).  
  2. **Cálculo del Cambio:** Se aplica la fórmula del log-ratio a las imágenes. El resultado es una nueva imagen donde los valores de cada píxel representan la magnitud del cambio.  
  3. **Interpretación:**  
     * Valores muy positivos indican un aumento en la retrodispersión, lo que puede sugerir crecimiento de la vegetación o preparación del suelo (aumento de la rugosidad).  
     * Valores muy negativos indican una disminución, que podría estar asociada a una cosecha, una inundación (como en el caso del arroz) o el alisamiento del terreno.13  
  4. **Mapa de Cambios:** Se puede aplicar un umbral estadístico para crear un mapa simple que muestre únicamente las áreas con cambios significativos.

### **3.2. Método 2: Análisis de la Serie Temporal Completa**

* **Concepto:** En lugar de comparar solo dos fechas, este método utiliza toda la secuencia de imágenes disponible. Analiza la "firma temporal" de cada píxel, que es el patrón de sus valores de retrodispersión a lo largo del tiempo. Un cambio en la actividad agrícola se manifiesta como una ruptura o anomalía en este patrón.5  
* **Aplicación Práctica:**  
  1. **Construcción de la Serie Temporal:** Se crea una gráfica que muestra cómo cambia el valor de retrodispersión de un píxel o un área a lo largo de los meses.  
  2. **Detección de Anomalías:** Se buscan cambios abruptos en la serie temporal. Una caída repentina en la señal puede indicar una cosecha o inundación, mientras que una subida sostenida puede señalar el inicio del crecimiento de un cultivo.5  
  3. **Análisis de la Variabilidad:** Se pueden calcular estadísticas como la desviación estándar a lo largo del tiempo.  
     * **Áreas dinámicas:** Un píxel con alta variabilidad probablemente corresponde a un cultivo de ciclo corto (como arroz o soya) donde hay siembra, crecimiento y cosecha.  
     * **Áreas estables:** Un píxel con baja variabilidad suele corresponder a coberturas estables como bosques o plantaciones de palma de aceite ya maduras.

## **4\. Interpretación de los Cambios en el Contexto Agrícola**

La clave para dar sentido a los cambios detectados es entender cómo las diferentes actividades agrícolas afectan la señal de radar.

### **4.1. Firmas de Radar de los Cultivos Principales**

* **Arroz:** El ciclo del arroz es muy distintivo para el radar. La inundación inicial de los campos provoca una caída drástica de la señal (el agua actúa como un espejo).14 A medida que las plantas crecen y emergen del agua, la señal aumenta rápidamente. La cosecha vuelve a generar una caída abrupta.7  
* **Soya:** La soya muestra un patrón de crecimiento claro. La señal de radar (especialmente en polarización VH) aumenta a medida que la planta desarrolla biomasa y estructura. Antes de la cosecha, cuando la planta se seca y pierde hojas, la señal disminuye.28  
* **Palma de Aceite:** Las plantaciones de palma madura tienen una estructura de dosel grande y compleja, lo que resulta en una señal de radar consistentemente alta y estable durante todo el año.4 Por lo tanto, un cambio de un área de pastizal (señal baja y variable) a una señal alta y estable a lo largo de los años puede indicar la expansión de este cultivo.

### **4.2. Visualización de los Resultados**

Para comunicar los hallazgos de manera efectiva, se proponen las siguientes visualizaciones:

* **Mapa de Magnitud de Cambio:** Un mapa a color donde cada píxel muestra la intensidad del cambio entre dos fechas. Los colores cálidos (rojos) pueden indicar una disminución de la señal (posible cosecha) y los colores fríos (azules) un aumento (posible crecimiento).  
* **Mapa de Alertas de Cambio:** Un mapa binario (dos colores) que resalta únicamente las áreas donde se detectaron cambios estadísticamente significativos, sirviendo como un sistema de alerta.  
* **Gráficas de Series Temporales:** Gráficas que muestran la evolución de la señal de radar promedio para un municipio o un lote específico. Estas gráficas son la herramienta más poderosa para visualizar y entender la dinámica de los cultivos a lo largo del tiempo.

## **5\. Recomendaciones Finales**

Para un monitoreo agrícola efectivo en los Llanos Orientales, especialmente cuando no se dispone del ciclo completo de los cultivos, se recomienda un enfoque combinado:

1. **Usar el Análisis de Series Temporales como base:** Este método permite obtener una visión general de la dinámica agrícola, identificando qué zonas son estables y cuáles están en constante cambio. La creación de mapas de variabilidad (como la desviación estándar anual) es un excelente primer paso para diferenciar entre cultivos anuales y coberturas perennes.  
2. **Utilizar la Comparación Bitemporal para análisis específicos:** Este método es ideal para responder preguntas concretas y rápidas, como "¿qué áreas del municipio de Yopal mostraron un cambio significativo en la actividad agrícola durante el último mes?".

En todos los casos, la fase de preparación y preprocesamiento de los datos es crucial. Asegurar la consistencia geométrica (filtrado por órbita) y reducir el ruido (*speckle*) son pasos indispensables que garantizan la fiabilidad de cualquier método de detección de cambios que se aplique posteriormente.

#### **Fuentes citadas**

1. CIAT Research Online \- Accepted Manuscript \- CGSpace, acceso: septiembre 30, 2025, [https://cgspace.cgiar.org/bitstreams/3caf90c9-3ba4-4c73-9ea0-d4c7a7f21b0c/download](https://cgspace.cgiar.org/bitstreams/3caf90c9-3ba4-4c73-9ea0-d4c7a7f21b0c/download)  
2. 2019-03-30 Cifras Sectoriales Soya \- SIOC \- Ministerio de Agricultura y Desarrollo Rural, acceso: septiembre 30, 2025, [https://sioc.minagricultura.gov.co/AlimentosBalanceados/Documentos/2019-03-30%20Cifras%20Sectoriales%20Soya.pdf](https://sioc.minagricultura.gov.co/AlimentosBalanceados/Documentos/2019-03-30%20Cifras%20Sectoriales%20Soya.pdf)  
3. Red de Innovación de Cultivos Transitorios y Agroindustriales, acceso: septiembre 30, 2025, [https://vivo.agrosavia.co/display/unor4276](https://vivo.agrosavia.co/display/unor4276)  
4. Application of Sentinel-1 satellite to identify oil palm plantations in Balikpapan Bay, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/326725929\_Application\_of\_Sentinel-1\_satellite\_to\_identify\_oil\_palm\_plantations\_in\_Balikpapan\_Bay](https://www.researchgate.net/publication/326725929_Application_of_Sentinel-1_satellite_to_identify_oil_palm_plantations_in_Balikpapan_Bay)  
5. Sentinel-1 Time Series for Crop Identification in the Framework of the Future CAP Monitoring, acceso: septiembre 30, 2025, [https://www.mdpi.com/2072-4292/13/14/2785](https://www.mdpi.com/2072-4292/13/14/2785)  
6. Crop Health Assessment Using Sentinel-1 SAR Time Series Data in a Part of Central India, acceso: septiembre 30, 2025, [https://www.semanticscholar.org/paper/Crop-Health-Assessment-Using-Sentinel-1-SAR-Time-in-Kaushik-Mishra/772e7b1c53524efbca66d6854f57e21affe89dd5](https://www.semanticscholar.org/paper/Crop-Health-Assessment-Using-Sentinel-1-SAR-Time-in-Kaushik-Mishra/772e7b1c53524efbca66d6854f57e21affe89dd5)  
7. RICE CROP MONITORING USING SENTINEL-1 C-BAND DATA, acceso: septiembre 30, 2025, [https://isprs-archives.copernicus.org/articles/XLII-3-W6/73/2019/](https://isprs-archives.copernicus.org/articles/XLII-3-W6/73/2019/)  
8. (PDF) RICE CROP MONITORING USING SENTINEL-1 C-BAND DATA \- ResearchGate, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/334741588\_RICE\_CROP\_MONITORING\_USING\_SENTINEL-1\_C-BAND\_DATA](https://www.researchgate.net/publication/334741588_RICE_CROP_MONITORING_USING_SENTINEL-1_C-BAND_DATA)  
9. \[2408.10283\] Perception-based multiplicative noise removal using SDEs \- arXiv, acceso: septiembre 30, 2025, [https://arxiv.org/abs/2408.10283](https://arxiv.org/abs/2408.10283)  
10. SAR Image Despeckling Using a Convolutional Neural Network, acceso: septiembre 30, 2025, [https://engineering.jhu.edu/vpatel36/wp-content/uploads/2018/08/despeckle\_SPL\_v5.pdf](https://engineering.jhu.edu/vpatel36/wp-content/uploads/2018/08/despeckle_SPL_v5.pdf)  
11. THE CONTRAST RESEARCH OF THE METHODS OF RESTRAINING THE SPECKLE NOISE OF SAR IMAGES ),(\*),( ),( yxFyxR yxI \= V \=, acceso: septiembre 30, 2025, [https://www.isprs.org/proceedings/xxxv/congress/comm2/papers/110.pdf](https://www.isprs.org/proceedings/xxxv/congress/comm2/papers/110.pdf)  
12. Image Analysis Classification and Change Detection in Remote Sensing.pdf  
13. Rice Monitoring Using Sentinel-1 Data in the Google Earth Engine Platform \- ResearchGate, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/336056750\_Rice\_Monitoring\_Using\_Sentinel-1\_Data\_in\_the\_Google\_Earth\_Engine\_Platform](https://www.researchgate.net/publication/336056750_Rice_Monitoring_Using_Sentinel-1_Data_in_the_Google_Earth_Engine_Platform)  
14. ARTICLE Mapping rice areas with Sentinel-1 time-series and ..., acceso: septiembre 30, 2025, [https://elib.dlr.de/114137/1/manuscript\_rice-mapping-with-Sentinel-1\_final.pdf](https://elib.dlr.de/114137/1/manuscript_rice-mapping-with-Sentinel-1_final.pdf)  
15. The potential of Sentinel-1 time series for large-scale assessment of maize and wheat phenology across Germany, acceso: septiembre 30, 2025, [https://tandf.figshare.com/articles/journal\_contribution/The\_potential\_of\_Sentinel-1\_time\_series\_for\_large-scale\_assessment\_of\_maize\_and\_wheat\_phenology\_across\_Germany/29597250](https://tandf.figshare.com/articles/journal_contribution/The_potential_of_Sentinel-1_time_series_for_large-scale_assessment_of_maize_and_wheat_phenology_across_Germany/29597250)  
16. The potential of Sentinel-1 time series for large-scale assessment of maize and wheat phenology across Germany, acceso: septiembre 30, 2025, [https://www.tandfonline.com/doi/full/10.1080/15481603.2025.2531593](https://www.tandfonline.com/doi/full/10.1080/15481603.2025.2531593)  
17. Sentinel-1 Algorithms \- Earth Engine \- Google for Developers, acceso: septiembre 30, 2025, [https://developers.google.com/earth-engine/guides/sentinel1](https://developers.google.com/earth-engine/guides/sentinel1)  
18. A change detection measure based on a likelihood ratio and statistical properties of SAR intensity images \- University of Toronto, acceso: septiembre 30, 2025, [http://faculty.geog.utoronto.ca/Chen/Chen's%20homepage/PDFfiles2/RSL-2012-Xiong-SAR-ChangeDetection.pdf](http://faculty.geog.utoronto.ca/Chen/Chen's%20homepage/PDFfiles2/RSL-2012-Xiong-SAR-ChangeDetection.pdf)  
19. A change detection measure based on a likelihood ratio and statistical properties of SAR intensity images | Request PDF \- ResearchGate, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/241731232\_A\_change\_detection\_measure\_based\_on\_a\_likelihood\_ratio\_and\_statistical\_properties\_of\_SAR\_intensity\_images](https://www.researchgate.net/publication/241731232_A_change_detection_measure_based_on_a_likelihood_ratio_and_statistical_properties_of_SAR_intensity_images)  
20. Small-Target Detection between SAR Images Based on Statistical Modeling of Log-Ratio Operator \- PubMed Central, acceso: septiembre 30, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC6471731/](https://pmc.ncbi.nlm.nih.gov/articles/PMC6471731/)  
21. A Generalized Beta Prime Distribution as the Ratio Probability Density Function for Change Detection between Two SAR Intensity I \- DTU Research Database, acceso: septiembre 30, 2025, [https://orbit.dtu.dk/files/355321500/Accepted\_version.pdf](https://orbit.dtu.dk/files/355321500/Accepted_version.pdf)  
22. Detecting Changes in Sentinel-1 Imagery (Part 2\) | Google Earth ..., acceso: septiembre 30, 2025, [https://developers.google.com/earth-engine/tutorials/community/detecting-changes-in-sentinel-1-imagery-pt-2](https://developers.google.com/earth-engine/tutorials/community/detecting-changes-in-sentinel-1-imagery-pt-2)  
23. Radar vegetation phenology using Sentinel-1 \- Digital Earth Africa Docs, acceso: septiembre 30, 2025, [https://docs.digitalearthafrica.org/en/latest/sandbox/notebooks/Real\_world\_examples/Phenology\_radar.html](https://docs.digitalearthafrica.org/en/latest/sandbox/notebooks/Real_world_examples/Phenology_radar.html)  
24. How Phenology Shapes Crop-Specific Sentinel-1 PolSAR Features and InSAR Coherence across Multiple Years and Orbits \- MDPI, acceso: septiembre 30, 2025, [https://www.mdpi.com/2072-4292/16/15/2791](https://www.mdpi.com/2072-4292/16/15/2791)  
25. monitoring rice crop using time series sentinel-1 data in google earth engine platform, acceso: septiembre 30, 2025, [https://www.semanticscholar.org/paper/MONITORING-RICE-CROP-USING-TIME-SERIES-SENTINEL-1-Mandal-Kumar/3e25aef18367a42bf00e85f6502236c00bc7a6f4](https://www.semanticscholar.org/paper/MONITORING-RICE-CROP-USING-TIME-SERIES-SENTINEL-1-Mandal-Kumar/3e25aef18367a42bf00e85f6502236c00bc7a6f4)  
26. Using Sentinel-1 Time Series Data for the Delineation of Management Zones \- MDPI, acceso: septiembre 30, 2025, [https://www.mdpi.com/2624-7402/7/5/150](https://www.mdpi.com/2624-7402/7/5/150)  
27. Rice Phenology Classification Model Based on Sentinel-1 Using Machine Learning Method on Google Earth Engine \- ResearchGate, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/382339444\_Rice\_Phenology\_Classification\_Model\_Based\_on\_Sentinel-1\_Using\_Machine\_Learning\_Method\_on\_Google\_Earth\_Engine](https://www.researchgate.net/publication/382339444_Rice_Phenology_Classification_Model_Based_on_Sentinel-1_Using_Machine_Learning_Method_on_Google_Earth_Engine)  
28. SOYBEAN CROPLAND MAPPING USING MULTI-TEMPORAL SENTINEL-1 DATA, acceso: septiembre 30, 2025, [https://isprs-archives.copernicus.org/articles/XLII-3-W6/109/2019/](https://isprs-archives.copernicus.org/articles/XLII-3-W6/109/2019/)  
29. (PDF) SOYBEAN CROPLAND MAPPING USING MULTI-TEMPORAL SENTINEL-1 DATA, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/334739809\_SOYBEAN\_CROPLAND\_MAPPING\_USING\_MULTI-TEMPORAL\_SENTINEL-1\_DATA](https://www.researchgate.net/publication/334739809_SOYBEAN_CROPLAND_MAPPING_USING_MULTI-TEMPORAL_SENTINEL-1_DATA)  
30. SOYBEAN CROPLAND MAPPING USING MULTI-TEMPORAL SENTINEL-1 DATA \- Semantic Scholar, acceso: septiembre 30, 2025, [https://pdfs.semanticscholar.org/6bc0/1deb79a14010cc9e336b8d6c64094cb04537.pdf](https://pdfs.semanticscholar.org/6bc0/1deb79a14010cc9e336b8d6c64094cb04537.pdf)  
31. Application of SAR data for oil palm tree discrimination \- ResearchGate, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/326727710\_Application\_of\_SAR\_data\_for\_oil\_palm\_tree\_discrimination](https://www.researchgate.net/publication/326727710_Application_of_SAR_data_for_oil_palm_tree_discrimination)  
32. Evaluation of JERS-l, ERS-l and Almaz SAR backscatter for rubber and oil palm stands in West Malaysia, acceso: septiembre 30, 2025, [https://www.tandfonline.com/doi/pdf/10.1080/01431169608949140](https://www.tandfonline.com/doi/pdf/10.1080/01431169608949140)  
33. Usability of Sentinel-1 C-band VV and VH SAR data for the detection of flooded oil palm, acceso: septiembre 30, 2025, [https://agris.fao.org/search/en/providers/125386/records/6765a28350e69ae81839589f](https://agris.fao.org/search/en/providers/125386/records/6765a28350e69ae81839589f)  
34. OBSERVER: How do Copernicus data help monitor and understand the impacts of palm oil plantations?, acceso: septiembre 30, 2025, [https://www.copernicus.eu/en/news/news/observer-how-do-copernicus-data-help-monitor-and-understand-impacts-palm-oil-plantations](https://www.copernicus.eu/en/news/news/observer-how-do-copernicus-data-help-monitor-and-understand-impacts-palm-oil-plantations)  
35. SAR Oil Palm Plantation Mapping in Batu Pahat with X, C, L bands for Change Detection, acceso: septiembre 30, 2025, [https://isprs-archives.copernicus.org/articles/XLVIII-G-2025/155/2025/isprs-archives-XLVIII-G-2025-155-2025.pdf](https://isprs-archives.copernicus.org/articles/XLVIII-G-2025/155/2025/isprs-archives-XLVIII-G-2025-155-2025.pdf)  
36. SAR Oil Palm Plantation Mapping in Batu Pahat with X, C, L bands for Change Detection, acceso: septiembre 30, 2025, [https://www.researchgate.net/publication/394742048\_SAR\_Oil\_Palm\_Plantation\_Mapping\_in\_Batu\_Pahat\_with\_X\_C\_L\_bands\_for\_Change\_Detection](https://www.researchgate.net/publication/394742048_SAR_Oil_Palm_Plantation_Mapping_in_Batu_Pahat_with_X_C_L_bands_for_Change_Detection)

[image1]: <data:image/png;base64,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>