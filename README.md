# Proyecto IA - Detector de Sonidos para Seguridad en el Hogar

## Identificación del proyecto

*   **Nombre del curso:** Inteligencia Artificial I - 2025-2 C1
*   **Nombre del equipo:** [Nombre del Equipo, ej: AudioGuardAI]
*   **Estudiantes:**
    *   [Nombre Estudiante 1 - Código UIS]
    *   [Nombre Estudiante 2 - Código UIS]
    *   [Nombre Estudiante 3 - Código UIS]

## Descripción concisa de los datos a usar

*   **Nombre del dataset:** Dataset Personalizado de Sonidos del Hogar.
*   **Enlace al dataset:** Los datos son una compilación de clips de audio de fuentes públicas como Freesound.org, Kaggle (ej: UrbanSound8K, ESC-50) y otras librerías de sonidos. [Enlace a tu repositorio o a un documento con los links de los sonidos usados].
*   **Cantidad de datos:** El dataset consta de [Número total] clips de audio en formato `.wav`, distribuidos equitativamente en 5 categorías: `vidrio rompiéndose`, `golpe de puerta`, `ladrido de perro`, `alarma de humo` y `aplausos`. Cada categoría contiene aproximadamente [Número] muestras.

---

## Preguntas a responder

### Antes del EDA (conceptual):

#### Problema y relevancia (máx. 100 palabras)
Los sistemas de seguridad para el hogar suelen ser costosos e invasivos. Este proyecto busca resolver el problema de la detección de eventos relevantes en el hogar de una manera accesible, utilizando únicamente el sonido ambiental. Un sistema capaz de identificar automáticamente sonidos como la rotura de un vidrio o una alarma de humo puede proporcionar alertas tempranas de posibles emergencias (robos, incendios), mejorando significativamente la seguridad y tranquilidad de los habitantes. La relevancia radica en crear una solución de bajo costo y fácil despliegue para la monitorización inteligente del hogar.

#### Objetivo del análisis (máx. 75 palabras)
El objetivo de esta primera fase (EDA) es comprender las características fundamentales de las señales de audio de cada categoría. Buscamos visualizar las formas de onda y los espectrogramas para identificar si existen "huellas" visuales distintivas para cada sonido. Esta exploración inicial es crucial para validar la hipótesis de que las cinco clases de sonidos son suficientemente diferentes como para que un modelo de machine learning pueda aprender a clasificarlas con alta precisión.

#### Métricas o indicadores (máx. 75 palabras)
Para evaluar la solución, las métricas clave serán la **Exactitud (Accuracy)** general, y la **Precisión (Precision)** y **Sensibilidad (Recall)** por cada clase. La **matriz de confusión** será un indicador visual fundamental. Estas métricas son útiles porque no solo nos dirán qué tan bien funciona el modelo en general (accuracy), sino también qué tan confiable es al predecir una clase específica (precisión) y su capacidad para no omitir eventos importantes como una alarma (recall).

#### Motivación de la elección (máx. 50 palabras)
Se eligió este problema por su aplicación práctica y directa en la vida cotidiana. Trabajar con audio representa un desafío más allá de los datos tabulares tradicionales, permitiéndonos aplicar técnicas de procesamiento de señales. El impacto potencial de crear una herramienta de seguridad accesible fue el principal motivador.

### Después de desarrollar el notebook de EDA (basado en datos):

#### Datos utilizados (máx. 50 palabras)
Se utilizó un dataset de [Número] archivos de audio en formato `.wav` obtenidos de fuentes públicas (Freesound, Kaggle). Los datos son de tipo serie de tiempo, representando la amplitud de la señal de audio a una frecuencia de muestreo de [ej: 22050] Hz, procesados para tener una duración uniforme.

#### Información contenida en los datos (máx. 100 palabras)
El análisis visual de los espectrogramas confirma que cada clase posee características distintivas. La `alarma de humo` muestra bandas de frecuencia altas, claras y sostenidas. La `rotura de vidrio` se caracteriza por una explosión inicial de energía en un amplio espectro de frecuencias. Los `golpes`, `ladridos` y `aplausos` son sonidos percusivos y de corta duración, pero se diferencian en su ritmo y distribución de frecuencias. Estas "huellas" visuales son la base que permitirá al modelo de IA realizar la clasificación.

#### Desafíos asociados a los datos (máx. 100 palabras)
El principal desafío identificado es el **ruido de fondo** presente en muchos clips, que podría confundir al modelo. Otro reto es la **variabilidad intracategórica**: existen muchos tipos de ladridos o formas de romper un vidrio. Además, la corta duración de algunos eventos y la posible superposición de sonidos en un entorno real son limitaciones a considerar para el desarrollo de la solución final. La calidad y limpieza de los datos serán cruciales para mitigar estos problemas.
