

# **Plan Maestro de Muestreo Espacial para la Clasificación Fenológica del Arroz: Un Enfoque Práctico y Adaptativo**

## **Resumen Ejecutivo**

Este documento presenta un plan integral para la recolección de datos de campo, diseñados para entrenar y validar modelos de inteligencia artificial que clasifican las etapas de crecimiento del arroz. El enfoque combina el rigor estadístico con la flexibilidad práctica, asegurando resultados confiables, logísticamente eficientes y de bajo costo, con un énfasis particular en el uso de **imágenes de radar** por su capacidad para operar en cualquier condición climática, un factor crucial en zonas arroceras tropicales.1

Reconociendo que no siempre se cuenta con un mapa completo de todos los lotes de arroz, especialmente en ciclos de siembra variables como el segundo semestre, este plan se estructura en torno a dos estrategias principales:

1. **Estrategia con Mapa Base:** Para situaciones donde existe un inventario completo de los lotes, se utilizará un método de **Muestreo Espacialmente Equilibrado (GRTS)**. Este avanzado sistema distribuye los puntos de muestreo de manera inteligente y uniforme, garantizando una cobertura completa del área de estudio y evitando sesgos por concentración de muestras.3  
2. **Estrategia Adaptativa (Sin Mapa Base):** Cuando no se dispone de un mapa previo, se implementa un **muestreo en dos fases**. Primero, se crea un "mapa de probabilidad" utilizando la **interpretación visual** de imágenes satelitales recientes (tanto de radar como ópticas) y/o el conocimiento experto del personal de campo para identificar los conglomerados o *"clusters"* donde es más probable encontrar arroz. Segundo, los equipos se dirigen a estas zonas para identificar los lotes reales y realizar el muestreo de manera focalizada.

La estratificación, o división del área de estudio, se realizará por **municipio**, **etapa fenológica del cultivo** (escala BBCH) y **tamaño del lote**. Se establece un umbral mínimo de lotes por municipio para garantizar la viabilidad del muestreo. El número total de puntos de muestreo se calculará con fórmulas estadísticas estándar para asegurar una confianza del 95% en los resultados. Estos puntos se distribuirán de forma optimizada, asignando más muestras a las zonas con mayor variabilidad, la cual se estima usando la varianza de la retrodispersión de radar o del índice de verdor (NDVI) de las imágenes satelitales.14

El protocolo de campo es práctico y moderno: la navegación a cada punto se realizará con la aplicación **QField** en dispositivos móviles.16 Dentro de cada lote, el punto se ubicará en una zona interior representativa para evitar efectos de borde. Finalmente, la calidad del modelo se evaluará con una técnica de

**Validación Cruzada por Bloques Espaciales**, un método robusto que ofrece una medida honesta de la exactitud del mapa en áreas nuevas.32

---

## **1.0 El Fundamento: ¿Por Qué y Cómo Estratificar?**

Para entender un paisaje tan complejo como el de los cultivos de arroz, no es posible abordarlo como un todo homogéneo. La **estratificación** es el primer paso y consiste en dividir el área de estudio en subgrupos más pequeños y manejables que son internamente más homogéneos.46 Al hacerlo, se asegura que cada tipo de condición, incluso las menos comunes, esté bien representada en la muestra. Esto permite obtener estimaciones más precisas y reduce el error general del muestreo.47

Para este proyecto, se organizará el muestreo en tres niveles de estratos:

1. **Estrato por Etapa Fenológica (Etapa del Cultivo):** El arroz pasa por distintas fases de crecimiento, y cada una se ve diferente desde el espacio. Se agruparán los lotes según su etapa de desarrollo, utilizando la escala internacional BBCH como guía.52 Las etapas principales son:  
   * **Siembra y Germinación** (BBCH 00-09)  
   * **Macollamiento** (BBCH 21-29): Desarrollo de nuevos tallos.  
   * **Embuche** (BBCH 41-49): La panícula se hincha dentro de la vaina.  
   * **Floración** (BBCH 61-69): Aparición de las flores.  
   * **Llenado de Grano** (BBCH 71-77): El grano se forma y acumula almidón.  
   * **Madurez** (BBCH 83-89): El grano está listo para la cosecha.  
2. **Estrato por Tamaño del Lote:** Las prácticas de manejo pueden variar según el tamaño de la finca. Para capturar esta diversidad, se clasifican los lotes así:  
   * **Micro:** Menos de 3 hectáreas.  
   * **Medio:** Entre 3 y 10 hectáreas.  
   * **Grande:** Más de 10 hectáreas.  
3. **Estrato por Municipio:** Agrupar los lotes por municipio no solo facilita la logística y la organización de las brigadas de campo, sino que también permite analizar los resultados a nivel local, respondiendo a las necesidades de cada región.

### **1.1 Viabilidad del Muestreo a Nivel Municipal**

Para que el esfuerzo de muestreo en un municipio sea estadísticamente representativo y logísticamente eficiente, es necesario que exista una cantidad mínima de lotes de arroz. Un número muy bajo de lotes haría que el costo por muestra sea prohibitivo y que la población a muestrear no sea suficiente para realizar inferencias válidas.

Se establece un **umbral de viabilidad de 30 a 50 lotes de arroz activos por municipio**. Este rango se considera un mínimo práctico para:

* **Justificar la movilización de equipos de campo:** Asegura que haya suficientes objetivos en un área geográfica concentrada.  
* **Permitir una estratificación significativa:** Proporciona una población base suficiente para ser dividida en los estratos de fenología y tamaño de lote.  
* **Garantizar la validez estadística:** Un municipio con menos de este umbral se consideraría de producción esporádica, y sus lotes podrían ser agrupados con los de un municipio vecino para fines de muestreo, o ser excluidos si el objetivo es mapear zonas de producción consolidada.62

---

## **2.0 Dos Caminos para el Muestreo: Con y Sin Mapa Base**

El punto de partida ideal para un muestreo es tener un mapa completo y actualizado de todos los lotes de arroz. Sin embargo, la realidad del campo, especialmente en ciclos agrícolas secundarios o en zonas con información fragmentada, es que este mapa a menudo no existe. Por ello, el plan es flexible y se adapta a ambas situaciones.

### **Estrategia A: Muestreo con un Mapa Base Completo (El Escenario Ideal)**

Cuando se cuenta con un inventario geográfico de todos los lotes, se aplica un método de **Muestreo Espacialmente Equilibrado (GRTS)**.

* **¿Qué es?** Es un algoritmo avanzado que selecciona puntos de muestreo de manera que cubran uniformemente toda el área de estudio. En lugar de agrupar muestras en algunas zonas y dejar otras vacías, el GRTS garantiza una dispersión óptima.6  
* **¿Por qué es mejor?** El resultado es una distribución de puntos que ofrece una visión representativa y controla un efecto estadístico llamado "autocorrelación espacial" (la tendencia de los lugares cercanos a parecerse entre sí). Además, genera una lista ordenada de **puntos de reemplazo**, lo que simplifica enormemente la logística en caso de que un punto seleccionado sea inaccesible.10

### **Estrategia B: Muestreo Adaptativo Sin un Mapa Base Previo (El Escenario Realista)**

Esta estrategia es ideal para el segundo semestre, cuando los lotes son menos numerosos y más concentrados, o en regiones donde no existe un catastro agrícola digital.

#### **Fase 1: Creación de un "Mapa de Probabilidad"**

El primer paso es construir un mapa guía para dirigir a los equipos de campo.

1. **Análisis de Imágenes Satelitales:** Se utilizan imágenes recientes, con un fuerte énfasis en **datos de radar (como los del satélite Sentinel-1)**. El radar es fundamental porque puede "ver" a través de las nubes, garantizando información continua durante la temporada de lluvias, que a menudo coincide con el ciclo del arroz.1 Estos datos se complementan con imágenes ópticas (como Sentinel-2 o Landsat) cuando están libres de nubes.  
2. **Identificación de Zonas de Interés:** Este mapa preliminar se enriquece mediante la **interpretación visual** de las imágenes satelitales por parte de profesionales con experiencia en campo. Este conocimiento experto permite identificar patrones, texturas y contextos que los análisis automáticos podrían pasar por alto, delimitando así **agrupaciones o *clusters*** de lotes donde es más probable encontrar el cultivo. Su aporte es fundamental para refinar y validar las "zonas calientes" y dirigir los esfuerzos de campo de manera eficiente.

#### **Fase 2: Muestreo Dirigido en Campo**

Con este mapa de probabilidad, el trabajo de campo se vuelve mucho más eficiente.

1. **Selección de Bloques de Muestreo:** En lugar de seleccionar puntos individuales en todo el municipio, se seleccionan **bloques o áreas de trabajo** (por ejemplo, de 1 km²) dentro de las "zonas calientes".  
2. **Verificación y Muestreo en Sitio:** Al llegar a un bloque asignado, la brigada de campo:  
   * **Identifica los Lotes Reales:** Usando el mapa de probabilidad como guía en su dispositivo móvil, confirman y delimitan los lotes de arroz que existen dentro del bloque.  
   * **Aplica las Reglas de Muestreo:** Dentro de los lotes identificados, seleccionan uno o varios (según la densidad) y toman **un solo punto de datos por lote**, siguiendo el protocolo de ubicación interior y distancia mínima.

Este enfoque adaptativo optimiza los recursos, respeta los principios estadísticos y aprovecha al máximo la experiencia del equipo técnico.

---

## **3.0 ¿Cuántos Puntos se Necesitan y Dónde se Ubican?**

Esta sección define el tamaño de la muestra y su distribución para maximizar la exactitud de los resultados.

### **3.1 Cálculo del Número Total de Puntos**

Para decidir cuántos lotes se deben visitar en total, se utiliza una fórmula estadística estándar (la **fórmula de Cochran**) que permite calcular un tamaño de muestra ideal a partir de una población grande o desconocida.71

La fórmula inicial es:

n0​=e2Z2⋅p(1−p)​

Donde cada término tiene un significado preciso:

* Z: Es el valor estadístico que corresponde al **nivel de confianza** deseado. Para un nivel de confianza del 95%, que es el estándar en investigación, el valor de Z es **1.96**.71  
* p: Es una estimación de la proporción de una característica en la población. Cuando no se tiene información previa, se utiliza p=0.5. Este valor es el más conservador, ya que maximiza la variabilidad y, por lo tanto, produce el tamaño de muestra más grande y seguro.73  
* e: Es el **margen de error** máximo que se está dispuesto a aceptar. Un valor comúnmente utilizado es el 5% (o 0.05).71

Aplicando estos valores estándar, el cálculo del tamaño de muestra inicial (n0​) sería:

n0​=0.0521.962⋅0.5(1−0.5)​=0.00253.8416⋅0.25​=384.16≈385

Este valor representa el número de muestras necesarias si la población de lotes fuera infinita. Sin embargo, como se trabaja con un número finito de lotes (N), se aplica una fórmula de corrección para poblaciones finitas para ajustar este número 71:  
n=1+Nn0​−1​n0​​

Por ejemplo, si el número total de lotes de arroz en el área de estudio (N) fuera de 15,300, el tamaño de muestra final ajustado (n) sería:

n=1+15300385−1​385​=1.0251385​≈376

Este valor final de n es el número total de puntos de muestreo que se distribuirán entre los diferentes estratos.

### **3.2 Asignación Inteligente de la Muestra**

No todos los estratos son iguales. La **asignación de Neyman** es una estrategia para distribuir los puntos de muestreo de forma más eficiente: se asignan más puntos a los estratos que son más variables.77

* **¿Cómo se mide la variabilidad sin ir a campo?** Se usa un indicador de bajo costo derivado de las imágenes satelitales. Dado el enfoque en datos de radar, se puede utilizar la **varianza de la retrodispersión de la señal de radar** como un excelente indicador de la heterogeneidad estructural del cultivo. Alternativamente, si se dispone de imágenes ópticas sin nubes, se puede usar la **varianza del NDVI** (Índice de Vegetación de Diferencia Normalizada). Un estrato donde estos valores varían mucho sugiere que las condiciones del cultivo en el terreno también son más heterogéneas y, por lo tanto, necesita más puntos de muestreo.14

### **3.3 Cuotas Mínimas y Puntos de Reemplazo**

Para asegurar la robustez del modelo, se aplican dos reglas finales:

* **Cuotas Mínimas:** Para las etapas fenológicas que son raras o cubren poca área, se garantiza un número mínimo de muestras (ej. 50 para entrenamiento, 30 para validación) para que el modelo tenga suficientes ejemplos para aprender.\[1, 1, 1\]  
* **Sobremuestreo de Reemplazo:** Para cada estrato, se preseleccionará un **15% de puntos de reemplazo adicionales**. Si un punto principal no es accesible, se dispone de una lista ordenada de sustitutos listos para ser utilizados.

---

## **4.0 Manos a la Obra: Protocolo de Campo y Recomendaciones**

Un plan bien diseñado solo tiene éxito si se ejecuta con precisión y consistencia en el campo. Este protocolo detalla los procedimientos para garantizar una recolección de datos de alta calidad.

### **4.1 Navegación y Localización del Punto**

* **Herramienta de Navegación:** La navegación a los puntos seleccionados se realizará utilizando la aplicación **QField** en dispositivos móviles (tabletas o teléfonos inteligentes).16 Esta herramienta permite cargar los mapas del proyecto, los polígonos de los lotes y los puntos de muestreo, ofreciendo un guiado GPS preciso y la capacidad de visualizar toda la información relevante directamente en el campo, incluso sin conexión a internet.29  
* **Tolerancia de Exactitud:** Se acepta una tolerancia posicional de **5 a 10 metros**, la cual es compatible con la resolución de las imágenes satelitales de referencia.\[1, 1\]

### **4.2 Ubicación del Punto Dentro del Lote: El "Centroide Restringido"**

El borde de un lote suele ser diferente del interior. Para asegurar que el punto sea verdaderamente representativo del cultivo, se sigue esta regla:

1. Se calcula el centro geométrico (centroide) del lote seleccionado.  
2. Se aplica un "borde de seguridad" virtual de 10 metros hacia el interior del lote.  
3. Si el centroide cae dentro de esta zona segura, esa es la ubicación final. Si cae fuera, el punto se desplaza a la ubicación más cercana dentro de la zona segura.

### **4.3 Protocolo de Recolección de Datos**

En cada punto de muestreo, el equipo de campo realizará las siguientes tareas:

* **Registro Fotográfico:** Se tomará un set de fotos estandarizadas y georreferenciadas.  
* **Evaluación Fenológica:** Usando una guía visual de la escala BBCH, el técnico determinará y registrará el código de la etapa de crecimiento del arroz.52  
* **Formulario Digital:** Todos los datos se registrarán en un formulario digital estandarizado en QField, asegurando que la información sea completa y esté lista para su análisis.23

### **4.4 Plan de Contingencia: Activación de Reemplazos**

Si un lote primario no puede ser muestreado por una razón válida (negación de acceso, barrera física, riesgo de seguridad), se activa el plan de reemplazo: el coordinador activa el **primer lote de reemplazo disponible de la lista ordenada por GRTS que pertenezca al mismo estrato**.10

### **4.5 Recomendaciones Prácticas para el Diseño y la Toma de Puntos**

La calidad de un mapa depende directamente de la calidad del muestreo que lo sustenta. Las siguientes recomendaciones son fundamentales para garantizar que el proceso sea riguroso, eficiente y que los resultados sean defendibles.31

#### **Recomendaciones para el Diseño del Muestreo**

* **Planificación Rigurosa:** El éxito de un muestreo comienza mucho antes de salir al campo. Es crucial dedicar tiempo a la planificación para equilibrar los requisitos estadísticos con las limitaciones prácticas de tiempo y presupuesto. Un plan bien pensado anticipa problemas y asegura que cada dato recolectado contribuya de manera efectiva al objetivo final.  
* **Definir Claramente el Esquema de Clasificación:** Las reglas para definir cada clase de cobertura deben ser objetivas, cuantitativas y sin ambigüedades. Este mismo esquema debe ser utilizado tanto para la creación del mapa como para la recolección de los datos de referencia en campo. Esto incluye la definición de la **Unidad Mínima de Mapeo (UMM)**, que es el área más pequeña que será representada en el mapa.  
* **Utilizar un Muestreo Probabilístico:** Para que los resultados del muestreo puedan ser generalizados a toda el área de estudio, el diseño debe ser probabilístico. Esto significa que cada lote tiene una probabilidad conocida y no nula de ser seleccionado. El **muestreo aleatorio estratificado** es el método más recomendado, ya que garantiza que todas las clases, especialmente las raras, estén adecuadamente representadas en la muestra.\[1, 89, 90, 91, 92, 93, 94, 1, 1\]  
* **Asegurar la Independencia de los Datos:** Las muestras usadas para validar el mapa no deben haber sido utilizadas para entrenar el modelo de clasificación. Esta separación es fundamental para evitar una evaluación sesgada y demasiado optimista de la exactitud del mapa.\[1, 89, 90, 91, 92, 93, 94, 1, 1\]  
* **Seleccionar una Unidad de Muestra Adecuada:** La unidad de muestreo (el área que se evalúa en cada punto) debe ser lo suficientemente grande para compensar cualquier error de posicionamiento del GPS y de la imagen satelital. El uso de un único píxel como unidad de muestra casi nunca es apropiado, ya que es muy difícil asegurar que la ubicación en campo coincida exactamente con ese píxel en la imagen. Se recomienda usar un **clúster de píxeles homogéneo** (por ejemplo, un área de 3x3 píxeles) como una única unidad de muestra.\[1, 1\]

#### **Recomendaciones para la Toma de Puntos en Campo**

* **Garantizar la Calidad de los Datos de Referencia:** Los datos de campo son el "estándar de oro" contra el cual se mide el mapa. Por lo tanto, deben ser de una calidad considerablemente mayor. Esto se logra mediante el uso de fuentes de mayor resolución (imágenes de alta resolución) o la verificación directa en el terreno por personal experto.\[1, 89, 90, 91, 92, 93, 94, 1, 1\]  
* **Capacitar al Personal y Usar Procedimientos Estandarizados:** Todo el personal de campo debe recibir una capacitación adecuada sobre el esquema de clasificación y los protocolos de recolección. El uso de formularios de campo estandarizados (preferiblemente digitales, como en QField) asegura que todos los datos se recolecten de manera consistente y completa.\[1, 89, 90, 91, 92, 93, 94, 1\]  
* **Evitar Zonas Anómalas:** Al tomar una muestra dentro de un lote, se deben evitar áreas que no son representativas del manejo general, como bordes, caminos, cercas, zonas recién fertilizadas, áreas erosionadas o lugares donde se acumulan insumos agrícolas. Estas zonas pueden contaminar la muestra y no reflejar la condición real del lote.54  
* **Documentar Todo el Proceso:** La transparencia es clave para la credibilidad científica. Se debe documentar cada decisión, método y protocolo utilizado en el muestreo y análisis. Esto permite que otros puedan entender, evaluar y, si es necesario, replicar el trabajo realizado.\[1, 89, 90, 91, 92, 93, 94, 1\]

---

## **5.0 La Prueba de Fuego: Validación del Modelo y Mejora Continua**

Evaluar un mapa geoespacial requiere métodos que consideren la naturaleza espacial de los datos para obtener una medida realista de su rendimiento.

### **5.1 Validación Cruzada por Bloques Espaciales (Block CV)**

Los datos geográficos tienen una propiedad llamada **autocorrelación espacial**: puntos cercanos tienden a ser más similares que puntos lejanos.\[1, 1\] Si se usa una validación cruzada aleatoria tradicional, se podría estar entrenando y probando el modelo con puntos vecinos, lo que inflaría artificialmente los resultados de exactitud.

Para evitar esto, se usa la **Validación Cruzada por Bloques Espaciales (Block CV)**.32

* **¿Cómo funciona?** Se divide el área de estudio en una cuadrícula de grandes bloques geográficos. Luego, se entrena el modelo usando los datos de varios bloques y se prueba en un bloque completamente separado espacialmente.  
* **¿Por qué es mejor?** Este método simula de manera mucho más realista el desafío de predecir en un área geográfica nueva, dándonos una medida de exactitud más honesta y confiable.32

### **5.2 Determinación del Tamaño de Bloque mediante Análisis de Variograma**

La clave del Block CV es elegir un tamaño de bloque adecuado, que debe ser mayor que el rango de la autocorrelación espacial. Para definir este tamaño de forma objetiva, se usa una herramienta geoestadística llamada **variograma**.87

* **¿Qué hace un variograma?** Mide cómo la similitud entre los lotes de arroz disminuye a medida que aumenta la distancia entre ellos. Se puede calcular sobre datos proxy como la retrodispersión de radar o el NDVI.  
* **El "Rango":** El variograma permite calcular el **"rango"**, que es la distancia a partir de la cual los lotes ya no están correlacionados espacialmente.87  
* **Definición del Tamaño del Bloque:** El tamaño de los bloques de validación se establecerá para que sea **mayor que este rango de autocorrelación**, garantizando la independencia entre los datos de entrenamiento y prueba.

### **5.3 Recomendaciones para la Mejora Continua**

El muestreo no es un evento único, sino parte de un ciclo. Si después de la validación, alguna clase de cultivo no alcanza las metas de exactitud (por ejemplo, un **F1-score por clase ≥ 0.80**), se tomarán las siguientes acciones en futuras campañas:

* **Muestreo Enfocado:** Se aumentará el número de muestras para las clases problemáticas.  
* **Análisis de Confusiones:** Se analizará en detalle qué clases se confunden entre sí (por ejemplo, si el modelo confunde "Llenado de Grano" con "Madurez"). Esto puede guiar un muestreo futuro en zonas de transición entre estas etapas.  
* **Revisión del Protocolo:** Se verificará si la confusión puede deberse a ambigüedades en la guía de campo, para mejorar el entrenamiento del personal y la claridad de las definiciones.

#### **Fuentes citadas**

1. Determining Rice Growth Stage with X-Band SAR: A Metamodel Based Inversion \- MDPI, acceso: septiembre 29, 2025, [https://www.mdpi.com/2072-4292/9/5/460](https://www.mdpi.com/2072-4292/9/5/460)  
2. Good Practices for Assessing Accuracy and Estimating Area of Land Change | Request PDF, acceso: septiembre 29, 2025, [https://www.researchgate.net/publication/260138121\_Good\_Practices\_for\_Assessing\_Accuracy\_and\_Estimating\_Area\_of\_Land\_Change](https://www.researchgate.net/publication/260138121_Good_Practices_for_Assessing_Accuracy_and_Estimating_Area_of_Land_Change)  
3. 2.6.1.2.11 GRTS stratified or variable probability design pros & cons, acceso: septiembre 29, 2025, [https://groups.nceas.ucsb.edu/monitoring-kb/2-design/2.1\_Status\_Trend\_Design/2.1.1-spatial/2.1.6-survey\_design/2.6.1.2.11-grts-strat\_variable\_proscons.html](https://groups.nceas.ucsb.edu/monitoring-kb/2-design/2.1_Status_Trend_Design/2.1.1-spatial/2.1.6-survey_design/2.6.1.2.11-grts-strat_variable_proscons.html)  
4. 2.6.1.2.7 GRTS non-stratified design pros & cons — Salmon Monitoring Advisor, acceso: septiembre 29, 2025, [https://groups.nceas.ucsb.edu/monitoring-kb/2-design/2.1\_Status\_Trend\_Design/2.1.1-spatial/2.1.6-survey\_design/2.6.1.2.7-grts\_non-stratified\_proscons.html](https://groups.nceas.ucsb.edu/monitoring-kb/2-design/2.1_Status_Trend_Design/2.1.1-spatial/2.1.6-survey_design/2.6.1.2.7-grts_non-stratified_proscons.html)  
5. Spatially Balanced Survey Designs for Large Scale Monitoring Programs, acceso: septiembre 29, 2025, [https://sites.stat.washington.edu/peter/stevens.htm](https://sites.stat.washington.edu/peter/stevens.htm)  
6. Spatially Balanced Sampling of Natural Resources | Request PDF \- ResearchGate, acceso: septiembre 29, 2025, [https://www.researchgate.net/publication/4746793\_Spatially\_Balanced\_Sampling\_of\_Natural\_Resources](https://www.researchgate.net/publication/4746793_Spatially_Balanced_Sampling_of_Natural_Resources)  
7. 2.1.6.1 Survey spatial design overview — Salmon Monitoring Advisor, acceso: septiembre 29, 2025, [https://groups.nceas.ucsb.edu/monitoring-kb/2-design/2.1\_Status\_Trend\_Design/2.1.1-spatial/2.1.6-survey\_design.html](https://groups.nceas.ucsb.edu/monitoring-kb/2-design/2.1_Status_Trend_Design/2.1.1-spatial/2.1.6-survey_design.html)  
8. Spatially Balanced Sampling of Natural Resources | US EPA ARCHIVE DOCUMENT, acceso: septiembre 29, 2025, [https://archive.epa.gov/nheerl/arm/web/pdf/grts\_asa.pdf](https://archive.epa.gov/nheerl/arm/web/pdf/grts_asa.pdf)  
9. Spatially Balanced Sampling \- University of Canterbury, acceso: septiembre 29, 2025, [https://ir.canterbury.ac.nz/bitstreams/2cdbf347-af83-40b2-8131-38c31377446e/download](https://ir.canterbury.ac.nz/bitstreams/2cdbf347-af83-40b2-8131-38c31377446e/download)  
10. spsurvey: Spatial Sampling Design and Analysis in R \- PMC, acceso: septiembre 29, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC9926341/](https://pmc.ncbi.nlm.nih.gov/articles/PMC9926341/)  
11. Spatially Balanced Sampling • spsurvey, acceso: septiembre 29, 2025, [https://usepa.github.io/spsurvey/articles/sampling.html](https://usepa.github.io/spsurvey/articles/sampling.html)  
12. Using GIS to Generate Spatially Balanced Random Survey Designs for Natural Resource Applications | Request PDF \- ResearchGate, acceso: septiembre 29, 2025, [https://www.researchgate.net/publication/6289106\_Using\_GIS\_to\_Generate\_Spatially\_Balanced\_Random\_Survey\_Designs\_for\_Natural\_Resource\_Applications](https://www.researchgate.net/publication/6289106_Using_GIS_to_Generate_Spatially_Balanced_Random_Survey_Designs_for_Natural_Resource_Applications)  
13. Generalized Random Tessellation Stratified (GRTS) | Oregon Adult Salmonid Inventory & Sampling Project, acceso: septiembre 29, 2025, [https://odfw-oasis.forestry.oregonstate.edu/generalized-random-tessellation-stratified-grts](https://odfw-oasis.forestry.oregonstate.edu/generalized-random-tessellation-stratified-grts)  
14. Normalized Difference Vegetation Index as a Proxy of Urban Bird Species Presence and Distribution at Different Spatial Scales \- MDPI, acceso: septiembre 29, 2025, [https://www.mdpi.com/1424-2818/15/11/1139](https://www.mdpi.com/1424-2818/15/11/1139)  
15. Modeling Species Distribution Using Niche-Based Proxies Derived from Composite Bioclimatic Variables and MODIS NDVI \- MDPI, acceso: septiembre 29, 2025, [https://www.mdpi.com/2072-4292/4/7/2057](https://www.mdpi.com/2072-4292/4/7/2057)  
16. Spatial analysis of NDVI readings with difference sampling density \- Publication : USDA ARS, acceso: septiembre 29, 2025, [https://www.ars.usda.gov/research/publications/publication/?seqNo115=242544](https://www.ars.usda.gov/research/publications/publication/?seqNo115=242544)  
17. SPATIAL ANALYSIS OF NDVI READINGS WITH DIFFERENT SAMPLING DENSITIES \- USDA ARS, acceso: septiembre 29, 2025, [https://www.ars.usda.gov/ARSUserFiles/30910515/Publications/2011/Lan-Spatial%20Analysis%20of%20NDVI.pdf](https://www.ars.usda.gov/ARSUserFiles/30910515/Publications/2011/Lan-Spatial%20Analysis%20of%20NDVI.pdf)  
18. VNAI-NDVI-space and polar coordinate method for assessing crop leaf chlorophyll content and fractional cover \- ResearchGate, acceso: septiembre 29, 2025, [https://www.researchgate.net/publication/369701783\_VNAI-NDVI-space\_and\_polar\_coordinate\_method\_for\_assessing\_crop\_leaf\_chlorophyll\_content\_and\_fractional\_cover](https://www.researchgate.net/publication/369701783_VNAI-NDVI-space_and_polar_coordinate_method_for_assessing_crop_leaf_chlorophyll_content_and_fractional_cover)  
19. GC43K-1415: A Comparison of Techniques for Estimating NDVI For Agricultural Intervention Impact Assessment, acceso: septiembre 29, 2025, [https://ntrs.nasa.gov/api/citations/20190034028/downloads/20190034028.pdf](https://ntrs.nasa.gov/api/citations/20190034028/downloads/20190034028.pdf)  
20. Utilizing NDVI and remote sensing data to identify spatial variability in plant stress as \- Iowa State University Digital Repository, acceso: septiembre 29, 2025, [https://dr.lib.iastate.edu/bitstreams/aeab0350-3b52-4c3a-8254-d610e1c97e6e/download](https://dr.lib.iastate.edu/bitstreams/aeab0350-3b52-4c3a-8254-d610e1c97e6e/download)  
21. Seasonal Variation in the NDVI–Species Richness Relationship in a Prairie Grassland Experiment (Cedar Creek) \- MDPI, acceso: septiembre 29, 2025, [https://www.mdpi.com/2072-4292/8/2/128](https://www.mdpi.com/2072-4292/8/2/128)  
22. A commentary review on the use of normalized difference vegetation index (NDVI) in the era of popular remote sensing, acceso: septiembre 29, 2025, [https://d-nb.info/1217951091/34](https://d-nb.info/1217951091/34)  
23. A Uniform, Objective, and Adaptive System for Expressing Rice Development, acceso: septiembre 29, 2025, [https://www.researchgate.net/publication/237499182\_A\_Uniform\_Objective\_and\_Adaptive\_System\_for\_Expressing\_Rice\_Development](https://www.researchgate.net/publication/237499182_A_Uniform_Objective_and_Adaptive_System_for_Expressing_Rice_Development)  
24. 2.Cartilla con metodología para la obtención de información georreferenciada de cultivos \- UPME, acceso: septiembre 29, 2025, [https://www1.upme.gov.co/Documents/Enfoque-territorial/Resultados\_convenios/2\_Cartilla\_Metodologia\_obtencion\_inf\_georreferenciada\_Andes\_v2.pdf](https://www1.upme.gov.co/Documents/Enfoque-territorial/Resultados_convenios/2_Cartilla_Metodologia_obtencion_inf_georreferenciada_Andes_v2.pdf)  
25. QField: QGIS para dispositivos móviles y trabajo de campo \- MappingGIS, acceso: septiembre 29, 2025, [https://mappinggis.com/2019/04/qfield-qgis-para-dispositivos-moviles/](https://mappinggis.com/2019/04/qfield-qgis-para-dispositivos-moviles/)  
26. QField: Captura de datos SIG en dispositivos móviles \- Agrícolas Castilla Duero, acceso: septiembre 29, 2025, [https://www.agricolascastilladuero.es/attachments/article/739/QFIELD1.pdf](https://www.agricolascastilladuero.es/attachments/article/739/QFIELD1.pdf)  
27. Introducción a QField: Crea tu Primer Proyecto \- YouTube, acceso: septiembre 29, 2025, [https://www.youtube.com/watch?v=51r1rwn4iPs](https://www.youtube.com/watch?v=51r1rwn4iPs)  
28. Uso de QField para levantar información de campo en el ámbito comunitario, acceso: septiembre 29, 2025, [https://www.fii.gob.ve/uso-de-qfield-para-levantar-informacion-de-campo-en-el-ambito-comunitario/](https://www.fii.gob.ve/uso-de-qfield-para-levantar-informacion-de-campo-en-el-ambito-comunitario/)  
29. Manual de instalación y uso de QField para levantamiento de información de campo por medio de teléfonos móviles. \- Zona de Conocimiento, acceso: septiembre 29, 2025, [https://pnud-conocimiento.cr/wp-content/uploads/2022/03/Manual-de-instalacion-y-uso-de-QField-V2.pdf](https://pnud-conocimiento.cr/wp-content/uploads/2022/03/Manual-de-instalacion-y-uso-de-QField-V2.pdf)  
30. Guía Técnica para Muestreo de Suelos \- Repositorio Institucional de la Universidad Nacional Agraria, acceso: septiembre 29, 2025, [https://repositorio.una.edu.ni/3613/1/P33M539.pdf](https://repositorio.una.edu.ni/3613/1/P33M539.pdf)  
31. Assessing the Accuracy of Remotely Sensed Data Principles and Practices, Third Edition.pdf  
32. Spatial cross-validation for GeoAI 1, acceso: septiembre 29, 2025, [https://www.acsu.buffalo.edu/\~yhu42/papers/2023\_GeoAIHandbook\_SpatialCV.pdf](https://www.acsu.buffalo.edu/~yhu42/papers/2023_GeoAIHandbook_SpatialCV.pdf)  
33. Choosing blocks for spatial cross-validation: lessons from a marine remote sensing case study \- Frontiers, acceso: septiembre 29, 2025, [https://www.frontiersin.org/journals/remote-sensing/articles/10.3389/frsen.2025.1531097/full](https://www.frontiersin.org/journals/remote-sensing/articles/10.3389/frsen.2025.1531097/full)  
34. Choosing blocks for spatial cross-validation: lessons from a marine remote sensing case study \- Frontiers, acceso: septiembre 29, 2025, [https://www.frontiersin.org/journals/remote-sensing/articles/10.3389/frsen.2025.1531097/epub](https://www.frontiersin.org/journals/remote-sensing/articles/10.3389/frsen.2025.1531097/epub)  
35. Cross-validation for geospatial data: Estimating generalization performance in geostatistical problems \- Bangor University Research Portal, acceso: septiembre 29, 2025, [https://research.bangor.ac.uk/files/70920068/1149\_cross\_validation\_for\_geospatia.pdf](https://research.bangor.ac.uk/files/70920068/1149_cross_validation_for_geospatia.pdf)  
36. Cross-validation strategies for data with temporal, spatial, hierarchical, or phylogenetic structure, acceso: septiembre 29, 2025, [https://www.wsl.ch/lud/biodiversity\_events/papers/Roberts\_et\_al-2017-Ecography.pdf](https://www.wsl.ch/lud/biodiversity_events/papers/Roberts_et_al-2017-Ecography.pdf)  
37. Choosing blocks for spatial cross-validation: Lessons from a marine remote sensing case study \- ResearchGate, acceso: septiembre 29, 2025, [https://www.researchgate.net/publication/390049401\_Choosing\_blocks\_for\_spatial\_cross-validation\_Lessons\_from\_a\_marine\_remote\_sensing\_case\_study](https://www.researchgate.net/publication/390049401_Choosing_blocks_for_spatial_cross-validation_Lessons_from_a_marine_remote_sensing_case_study)  
38. Specialized R packages for spatial cross-validation: sperrorest and blockCV | R-bloggers, acceso: septiembre 29, 2025, [https://www.r-bloggers.com/2025/07/specialized-r-packages-for-spatial-cross-validation-sperrorest-and-blockcv/](https://www.r-bloggers.com/2025/07/specialized-r-packages-for-spatial-cross-validation-sperrorest-and-blockcv/)  
39. H-block cross-validation \- CRAN, acceso: septiembre 29, 2025, [https://cran.r-project.org/web/packages/palaeoSig/vignettes/h-block-crossvalidation.html](https://cran.r-project.org/web/packages/palaeoSig/vignettes/h-block-crossvalidation.html)  
40. blockCV: Spatial and Environmental Blocking for K-Fold and LOO Cross-Validation \- rvalavi, acceso: septiembre 29, 2025, [https://rvalavi.r-universe.dev/blockCV](https://rvalavi.r-universe.dev/blockCV)  
41. Foundation for unbiased cross-validation of spatio-temporal models for species distribution modeling \- arXiv, acceso: septiembre 29, 2025, [https://arxiv.org/html/2502.03480v1](https://arxiv.org/html/2502.03480v1)  
42. The blockCV package creates spatially or environmentally separated training and testing folds for cross-validation to provide a robust error estimation in spatially structured environments. See \- GitHub, acceso: septiembre 29, 2025, [https://github.com/rvalavi/blockCV](https://github.com/rvalavi/blockCV)  
43. Basic Steps in Geostatistics: The Variogram and Kriging, acceso: septiembre 29, 2025, [https://www.geokniga.org/bookfiles/geokniga-basicstepsingeostatistics.pdf](https://www.geokniga.org/bookfiles/geokniga-basicstepsingeostatistics.pdf)  
44. Spatial Analysis and Decision Assistance (SADA) Version 4 Geospatial Overview \- CLU-IN, acceso: septiembre 29, 2025, [https://clu-in.org/conf/tio/sada2/prez/SADA\_v\_4\_Geospatial\_Overview\_Cluin\_3-09-07bw.pdf](https://clu-in.org/conf/tio/sada2/prez/SADA_v_4_Geospatial_Overview_Cluin_3-09-07bw.pdf)  
45. Variograms for kriging and clustering of spatial functional data with phase variation \- PMC, acceso: septiembre 29, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC9912960/](https://pmc.ncbi.nlm.nih.gov/articles/PMC9912960/)  
46. Sampling methods in Clinical Research; an Educational Review \- PMC, acceso: septiembre 29, 2025, [https://pmc.ncbi.nlm.nih.gov/articles/PMC5325924/](https://pmc.ncbi.nlm.nih.gov/articles/PMC5325924/)  
47. Stratified sampling \- Wikipedia, acceso: septiembre 29, 2025, [https://en.wikipedia.org/wiki/Stratified\_sampling](https://en.wikipedia.org/wiki/Stratified_sampling)  
48. What is Stratified Sampling? Definition, Types & Examples \- Researcher.Life, acceso: septiembre 29, 2025, [https://researcher.life/blog/article/what-is-stratified-sampling-definition-types-examples/](https://researcher.life/blog/article/what-is-stratified-sampling-definition-types-examples/)  
49. Stratified Random Sampling: Definition & Guide \- Qualtrics, acceso: septiembre 29, 2025, [https://www.qualtrics.com/experience-management/research/stratified-random-sampling/](https://www.qualtrics.com/experience-management/research/stratified-random-sampling/)  
50. How Stratified Random Sampling Works, With Examples \- Investopedia, acceso: septiembre 29, 2025, [https://www.investopedia.com/terms/stratified\_random\_sampling.asp](https://www.investopedia.com/terms/stratified_random_sampling.asp)  
51. Good Practices for Estimating Area and Assessing Accuracy of Land Change Maps \- CORE, acceso: septiembre 29, 2025, [https://core.ac.uk/download/pdf/84637113.pdf](https://core.ac.uk/download/pdf/84637113.pdf)  
52. Growth Stages of Mono- and Dicotyledonous Plants-a.pdf, acceso: septiembre 29, 2025, [https://www.julius-kuehn.de/media/Veroeffentlichungen/bbch%20epaper%20en/page.pdf](https://www.julius-kuehn.de/media/Veroeffentlichungen/bbch%20epaper%20en/page.pdf)  
53. BBCH-scale (rice) \- Wikipedia, acceso: septiembre 29, 2025, [https://en.wikipedia.org/wiki/BBCH-scale\_(rice)](https://en.wikipedia.org/wiki/BBCH-scale_\(rice\))  
54. Rice Growth Stages BBCH Guide | PDF | Leaf | Plant Stem \- Scribd, acceso: septiembre 29, 2025, [https://www.scribd.com/document/46871655/BBCH-Rice](https://www.scribd.com/document/46871655/BBCH-Rice)  
55. Rice Growth Stages: Crop Development From Seed To Grain \- EOS Data Analytics, acceso: septiembre 29, 2025, [https://eos.com/crop-management-guide/rice-growth-stages/](https://eos.com/crop-management-guide/rice-growth-stages/)  
56. Estados fenologicos del arroz escala extendida BBCH \- tecnicoagricola.es, acceso: septiembre 29, 2025, [https://www.tecnicoagricola.es/estados-fenologicos-del-arroz-escala-extendida-bbch/](https://www.tecnicoagricola.es/estados-fenologicos-del-arroz-escala-extendida-bbch/)  
57. 111 Estadios fenológicos de las plantas mono- y dicotiledoneas \- OpenAgrar, acceso: septiembre 29, 2025, [https://www.openagrar.de/servlets/MCRFileNodeServlet/openagrar\_derivate\_00051858/Meier\_BBCH-Monograph\_III%20Estadios%20fenol%C3%B3gicos%20de%20las%20plantas%20mono-%20y%20dicotiledoneas\_es.pdf](https://www.openagrar.de/servlets/MCRFileNodeServlet/openagrar_derivate_00051858/Meier_BBCH-Monograph_III%20Estadios%20fenol%C3%B3gicos%20de%20las%20plantas%20mono-%20y%20dicotiledoneas_es.pdf)  
58. Determinación de las etapas de inicio de macollamiento, inicio de primordio, floración y madurez en la planta de arroz,con el sistema s, v y r correlacionado con la sumatoria térmica \- SciELO, acceso: septiembre 29, 2025, [https://www.scielo.sa.cr/scielo.php?script=sci\_arttext\&pid=S0377-94242015000200121](https://www.scielo.sa.cr/scielo.php?script=sci_arttext&pid=S0377-94242015000200121)  
59. Codificación BBCH de los principales estados fenológicos del arroz. \- FERTIHOUSE, la mejor línea de fertilizantes para todo tipo de plantas., acceso: septiembre 29, 2025, [https://www.fertihouse.es/conceptos-basicos-cultivo/codificacion-bbch-de-los-principales-estados-fenologicos-del-arroz](https://www.fertihouse.es/conceptos-basicos-cultivo/codificacion-bbch-de-los-principales-estados-fenologicos-del-arroz)  
60. Morfología y Fases fenológicas de la planta de arroz, acceso: septiembre 29, 2025, [https://www.acpaarrozcorrientes.org.ar/academico/Apunte-MORFOLOGIA.pdf](https://www.acpaarrozcorrientes.org.ar/academico/Apunte-MORFOLOGIA.pdf)  
61. Índices fisiotécnicos, fases de crecimiento y etapas de desarrollo de la planta de arroz \- CGSpace, acceso: septiembre 29, 2025, [https://cgspace.cgiar.org/server/api/core/bitstreams/b80e5062-8098-44ea-9e93-6fe84df50fe9/content](https://cgspace.cgiar.org/server/api/core/bitstreams/b80e5062-8098-44ea-9e93-6fe84df50fe9/content)  
62. Muestreo para la aceptacin de lotes, acceso: septiembre 29, 2025, [https://www.chospab.es/calidad/archivos/Metodos/Muestreoparalaaceptacindelotes.pdf](https://www.chospab.es/calidad/archivos/Metodos/Muestreoparalaaceptacindelotes.pdf)  
63. Muestrear el suelo cuidadosamente: la clave para obtener información confiable sobre el análisis de suelo, acceso: septiembre 29, 2025, [https://content.ces.ncsu.edu/muestrear-el-suelo-cuidadosamente-la-clave-para-obtener-informacion-confiable-sobre-el-analisis-de](https://content.ces.ncsu.edu/muestrear-el-suelo-cuidadosamente-la-clave-para-obtener-informacion-confiable-sobre-el-analisis-de)  
64. Muestreo de Suelos para el Manejo de Nutrientes \- USDA, acceso: septiembre 29, 2025, [https://www.nrcs.usda.gov/sites/default/files/2022-10/Sampling%20Soils%20for%20Nutrient%20Mgt%20en%20Espa%C3%B1ol.pdf](https://www.nrcs.usda.gov/sites/default/files/2022-10/Sampling%20Soils%20for%20Nutrient%20Mgt%20en%20Espa%C3%B1ol.pdf)  
65. Guía para muestreo de suelos. \- Abonamos, acceso: septiembre 29, 2025, [https://www.abonamos.com/blog/2020/6/19/gua-para-muestreo-de-suelos](https://www.abonamos.com/blog/2020/6/19/gua-para-muestreo-de-suelos)  
66. Spatial Sampling Design and Analysis • spsurvey \- GitHub Pages, acceso: septiembre 29, 2025, [https://usepa.github.io/spsurvey/](https://usepa.github.io/spsurvey/)  
67. spsurvey: Spatial Sampling Design and Analysis \- usepa \- R-universe, acceso: septiembre 29, 2025, [https://usepa.r-universe.dev/spsurvey](https://usepa.r-universe.dev/spsurvey)  
68. spsurvey source: R/grts.R \- rdrr.io, acceso: septiembre 29, 2025, [https://rdrr.io/cran/spsurvey/src/R/grts.R](https://rdrr.io/cran/spsurvey/src/R/grts.R)  
69. grts Select a generalized random tessellation stratified (GRTS) sample \- RDocumentation, acceso: septiembre 29, 2025, [https://www.rdocumentation.org/packages/spsurvey/versions/5.5.1/topics/grts](https://www.rdocumentation.org/packages/spsurvey/versions/5.5.1/topics/grts)  
70. spsurvey: Spatial Sampling Design and Analysis \- CRAN, acceso: septiembre 29, 2025, [https://cran.r-project.org/web/packages/spsurvey/spsurvey.pdf](https://cran.r-project.org/web/packages/spsurvey/spsurvey.pdf)  
71. 6.2.1. Cochran's Sample Size Formula \- My Research Lab, acceso: septiembre 29, 2025, [https://www.myrelab.com/learn/sample-size](https://www.myrelab.com/learn/sample-size)  
72. Cochran's sample size formula \- GitHub Gist, acceso: septiembre 29, 2025, [https://gist.github.com/marcoscaceres/7137166](https://gist.github.com/marcoscaceres/7137166)  
73. Guide to Cochran's Sample Size Calculator, acceso: septiembre 29, 2025, [https://spssservices.com/cochran-sample-size-calculator-guide/](https://spssservices.com/cochran-sample-size-calculator-guide/)  
74. Organizational Research: Determining Appropriate Sample Size in Survey Research Appropriate Sample Size in Survey Research \- OPALCO, acceso: septiembre 29, 2025, [https://www.opalco.com/wp-content/uploads/2014/10/Reading-Sample-Size1.pdf](https://www.opalco.com/wp-content/uploads/2014/10/Reading-Sample-Size1.pdf)  
75. Sample Size Estimation using Yamane and Cochran and Krejcie and Morgan and Green Formulas and Cohen Statistical Power Analysis b \- thaijo.org, acceso: septiembre 29, 2025, [https://so04.tci-thaijo.org/index.php/ATI/article/download/254253/173847/938756](https://so04.tci-thaijo.org/index.php/ATI/article/download/254253/173847/938756)  
76. Sample Size in Statistics (How to Find it): Excel, Cochran's Formula, General Tips, acceso: septiembre 29, 2025, [https://www.statisticshowto.com/probability-and-statistics/find-sample-size/](https://www.statisticshowto.com/probability-and-statistics/find-sample-size/)  
77. Sample Size: Stratified Sample \- Stat Trek, acceso: septiembre 29, 2025, [https://stattrek.com/sample-size/stratified-sample](https://stattrek.com/sample-size/stratified-sample)  
78. Chapter 3 Stratification | Survey data in the field of economy and finance \- Bookdown, acceso: septiembre 29, 2025, [https://bookdown.org/osierguillaume/mybook/stratification.html](https://bookdown.org/osierguillaume/mybook/stratification.html)  
79. Chapter 8 Stratified Sampling | STAT392, acceso: septiembre 29, 2025, [https://homepages.ecs.vuw.ac.nz/\~rarnold/STAT392/SampleSurveysBook/\_book/stratified-sampling.html](https://homepages.ecs.vuw.ac.nz/~rarnold/STAT392/SampleSurveysBook/_book/stratified-sampling.html)  
80. Neyman allocation \- Wikipedia, acceso: septiembre 29, 2025, [https://en.wikipedia.org/wiki/Neyman\_allocation](https://en.wikipedia.org/wiki/Neyman_allocation)  
81. 6\. Stratified Random Sampling, acceso: septiembre 29, 2025, [https://www.asc.ohio-state.edu/kaizar.1/courses/6510/notes/6\_stratified\_sampling.pdf](https://www.asc.ohio-state.edu/kaizar.1/courses/6510/notes/6_stratified_sampling.pdf)  
82. Stratified sampling | Probability and Statistics Class Notes \- Fiveable, acceso: septiembre 29, 2025, [https://fiveable.me/probability-and-statistics/unit-6/stratified-sampling/study-guide/kU5CImxBkehuCWP2](https://fiveable.me/probability-and-statistics/unit-6/stratified-sampling/study-guide/kU5CImxBkehuCWP2)  
83. Good practices for estimating area and assessing accuracy of land change, acceso: septiembre 29, 2025, [https://samv.elearning.unipd.it/pluginfile.php/175898/mod\_resource/content/0/articolo\_oloffson.pdf](https://samv.elearning.unipd.it/pluginfile.php/175898/mod_resource/content/0/articolo_oloffson.pdf)  
84. Good Practices for Object-Based Accuracy Assessment \- MDPI, acceso: septiembre 29, 2025, [https://www.mdpi.com/2072-4292/9/7/646](https://www.mdpi.com/2072-4292/9/7/646)  
85. (PDF) Sampling design for accuracy assessment of land cover \- ResearchGate, acceso: septiembre 29, 2025, [https://www.researchgate.net/publication/253147366\_Sampling\_design\_for\_accuracy\_assessment\_of\_land\_cover](https://www.researchgate.net/publication/253147366_Sampling_design_for_accuracy_assessment_of_land_cover)  
86. Sampling design for estimation of area and map accuracy \- openMRV, acceso: septiembre 29, 2025, [https://openmrv.org/web/guest/w/modules/mrv/modules\_3/sampling-design-for-estimation-of-area-and-map-accuracy](https://openmrv.org/web/guest/w/modules/mrv/modules_3/sampling-design-for-estimation-of-area-and-map-accuracy)  
87. Spatial Sampling \- UNC Charlotte Pages, acceso: septiembre 29, 2025, [https://pages.charlotte.edu/wp-content/uploads/sites/150/2012/12/Spatial-Sampling-Regional-Science-Chapter.pdf](https://pages.charlotte.edu/wp-content/uploads/sites/150/2012/12/Spatial-Sampling-Regional-Science-Chapter.pdf)  
88. Variogram and spatial autocorrelation \- Aspexit, acceso: septiembre 29, 2025, [https://www.aspexit.com/variogram-and-spatial-autocorrelation/](https://www.aspexit.com/variogram-and-spatial-autocorrelation/)  
89. Exploring spatial autocorrelation in R \- R-bloggers, acceso: septiembre 29, 2025, [https://www.r-bloggers.com/2019/07/exploring-spatial-autocorrelation-in-r/](https://www.r-bloggers.com/2019/07/exploring-spatial-autocorrelation-in-r/)