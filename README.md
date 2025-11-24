
# Detector de Sonidos para Seguridad en el Hogar — IA1 (2025-2 C1)

**Curso:** Inteligencia Artificial I - 2025-2 C1  
**Equipo:** Proyect IA  
**Integrantes:**  
- BALLESTEROS MACIAS JUAN FERNANDO - 2224653
- HERRERA BAQUERO JUAN PABLO       - 2224512

---

## Resumen Ejecutivo del Proyecto

Este proyecto implementa un sistema completo de **clasificación de sonidos para seguridad en el hogar** mediante técnicas de Machine Learning. El sistema es capaz de identificar cinco tipos de eventos acústicos críticos para la seguridad doméstica: vidrios rompiéndose, alarmas de humo, agua corriendo, golpes en puertas y estufas prendiéndose.

### Resultados Clave Obtenidos

- **Modelo Final:** Random Forest con 97.5% de accuracy
- **Dataset:** 200 muestras de audio (40 por cada una de las 5 categorías)
- **Características Extraídas:** 70 features acústicas (MFCCs, espectrales, temporales)
- **Pipeline Completo:** Desde análisis exploratorio hasta modelos supervisados y no supervisados


---

## Descripción del Dataset

**Dataset:** Sonidos de eventos domésticos recopilados de Pixabay SFX — 5 clases × 40 muestras c/u (200 clips de audio, 1–10 segundos de duración).

**Fuente:** [Pixabay — Sound Effects](https://pixabay.com/es/sound-effects/search/) y [Carpeta en Google Drive](https://drive.google.com/drive/folders/1y7ibtNqqgdMhxik_176RQQprkYSIPpYf?usp=sharing).

**Categorías de Sonidos:**
1. **Agua corriendo** (agua_corriendo) — 40 muestras
2. **Alarma de humo** (alarma_humo) — 40 muestras
3. **Estufa prendiéndose** (estufa_prendiendose) — 40 muestras
4. **Golpe de puerta** (golpe_puerta) — 40 muestras
5. **Vidrios rompiéndose** (vidrio_rompiendose) — 40 muestras

**Total:** 200 archivos de audio en formato .mp3


## Estructura del Proyecto

El proyecto se desarrolló en tres fases principales, cada una documentada en un notebook de Jupyter, siguiendo el pipeline de Machine Learning ilustrado a continuación:

### Diagrama de Flujo del Pipeline

![Diagrama de Flujo del Pipeline de ML del Proyecto](diagrama.jpg)

Este diagrama muestra el flujo completo del proyecto, desde la ingesta de datos brutos hasta la obtención de resultados y métricas de evaluación, cubriendo tanto el enfoque de **Aprendizaje Supervisado** como el de **Aprendizaje No Supervisado**.

---

### 1. Análisis Exploratorio de Datos (EDA)
**Notebook:** `01-exploratory_data_analysis.ipynb`

En esta fase se realizó:
- Carga y exploración inicial de los 200 archivos de audio
- Visualización de formas de onda y espectrogramas por categoría
- Extracción de 70 características acústicas:
  - **MFCCs** (13 coeficientes cepstrales)
  - **Características espectrales** (centroide, rolloff, ancho de banda, flatness)
  - **Características temporales** (RMS, Zero Crossing Rate)
  - **Características estadísticas** (media, desviación estándar, kurtosis, skewness)
- Análisis de distribuciones y correlaciones entre características
- Identificación de patrones distintivos por categoría

**Conclusiones EDA:**
- Los sonidos impulsivos (vidrio, golpe) tienen alta energía en transientes
- Los sonidos continuos (agua, alarma) muestran periodicidad
- Las características MFCCs son altamente discriminativas
- Existe separabilidad entre clases en el espacio de características

### 2. Modelos de Aprendizaje Supervisado
**Notebook:** `02-supervised_learning_models.ipynb`

Se entrenaron y evaluaron múltiples modelos de clasificación:

**Modelos Implementados:**
- Regresión Logística
- K-Nearest Neighbors (KNN)
- Árboles de Decisión
- Random Forest
- Support Vector Machines (SVM)

**Resultados Finales:**
- **Mejor Modelo:** Random Forest
- **Accuracy:** 97.5%
- **Precision/Recall/F1-Score:** >95% en todas las clases
- **Matriz de Confusión:** Solo 1 error en 40 muestras de test

**Optimización:**
- Búsqueda de hiperparámetros con GridSearchCV
- Validación cruzada estratificada (5-fold)
- Análisis de importancia de características
- Evaluación de métricas por clase

### 3. Aprendizaje No Supervisado y Reducción de Dimensionalidad
**Notebook:** `03-unsupervised_learning.ipynb`

Se exploraron técnicas no supervisadas para validar la estructura de los datos:

**Clustering Implementado:**
- **KMeans:** Identificó 2 clusters principales (Silhouette: 0.3385)
- **DBSCAN:** Detectó 3 clusters + 18.5% ruido (Silhouette: 0.3187)
- **Agglomerative Clustering:** 2 clusters jerárquicos (Silhouette: 0.3361)

**Reducción de Dimensionalidad:**
- **PCA:** 25 componentes para 90% varianza, 53 para 99%
- **t-SNE:** Visualización 2D/3D con excelente separación de clases

**Conclusiones Clave:**
- La estructura natural del dataset presenta 2-3 agrupaciones acústicas
- La reducción dimensional empeora el rendimiento (de 97.5% a 87.5%)
- Las 70 características originales son complementarias y necesarias
- Para producción se recomienda mantener el espacio de características completo

---

## Metodología y Pipeline de Machine Learning

El proyecto siguió un pipeline completo de Machine Learning:

1. **Ingesta de Datos:** Descarga y organización de 200 archivos de audio
2. **Preprocesamiento:** Normalización de duración, muestreo a 22050 Hz
3. **Extracción de Features:** 70 características acústicas con Librosa
4. **Análisis Exploratorio:** Visualizaciones, estadísticas, correlaciones
5. **División de Datos:** Train-test split estratificado (80-20)
6. **Entrenamiento Supervisado:** 5 algoritmos de clasificación
7. **Evaluación y Selección:** Random Forest como mejor modelo (97.5% accuracy)
8. **Clustering:** Validación de estructura con KMeans, DBSCAN, Agglomerative
9. **Reducción Dimensional:** Exploración con PCA y t-SNE

---

## Problema y Relevancia

### Contexto del Problema
Buscamos desarrollar un sistema de clasificación de sonidos que identifique eventos acústicos relevantes para la seguridad y el monitoreo del hogar. Este sistema puede alertar a los residentes sobre situaciones críticas como:

- **Intrusiones:** Detección de vidrios rompiéndose o golpes en puertas
- **Emergencias:** Activación de alarmas de humo
- **Descuidos domésticos:** Agua corriendo sin supervisión, estufas encendidas

### Importancia
El proyecto proporciona una capa adicional de seguridad, especialmente útil cuando:
- La vivienda está desocupada
- Hay niños o adultos mayores en casa
- Se busca automatizar el monitoreo sin sistemas invasivos de video

### Ventajas de la Solución
- **No invasivo:** Basado en audio, sin necesidad de cámaras
- **Bajo costo:** Utiliza micrófonos convencionales
- **Tiempo real:** Clasificación rápida para alertas inmediatas
- **Escalable:** Puede expandirse a más categorías de sonidos

---

## Resultados y Hallazgos Principales

### Desempeño del Modelo Final

| Métrica | Valor |
|---------|-------|
| Accuracy | 97.50% |
| Precision (promedio) | 97.62% |
| Recall (promedio) | 97.50% |
| F1-Score (promedio) | 97.49% |

### Rendimiento por Categoría

| Categoría | Precision | Recall | F1-Score |
|-----------|-----------|--------|----------|
| Agua corriendo | 100% | 100% | 100% |
| Alarma humo | 100% | 87.5% | 93.3% |
| Estufa prendiéndose | 87.5% | 100% | 93.3% |
| Golpe puerta | 100% | 100% | 100% |
| Vidrio rompiéndose | 100% | 100% | 100% |

### Características Más Importantes

Según el análisis de importancia de Random Forest:
1. **MFCCs** (coeficientes 1-8): 45% de importancia total
2. **Spectral Rolloff:** 12%
3. **RMS Energy:** 10%
4. **Zero Crossing Rate:** 8%
5. **Spectral Centroid:** 7%

### Comparación de Modelos

| Modelo | Accuracy | Tiempo Entrenamiento |
|--------|----------|---------------------|
| Random Forest | **97.5%** | Rápido |
| SVM (RBF) | 95.0% | Moderado |
| KNN (k=5) | 92.5% | Muy rápido |
| Árbol de Decisión | 87.5% | Muy rápido |
| Regresión Logística | 85.0% | Rápido |

---

## Desafíos y Soluciones

### Desafíos Identificados

1. **Tamaño del Dataset:** 200 muestras es relativamente pequeño
   - **Solución:** Extracción de múltiples características por muestra, validación cruzada

2. **Variabilidad Intra-Clase:** Diferentes tipos de golpes, velocidades de agua
   - **Solución:** Aumento de datos mediante augmentation, características robustas

3. **Duración Variable:** Audios de 1-10 segundos
   - **Solución:** Normalización a 5 segundos mediante padding/truncamiento

4. **Ruido de Fondo:** Algunas muestras con ruido ambiental
   - **Solución:** Características robustas (MFCCs) menos sensibles al ruido

5. **Desbalance Potencial:** Algunas clases más fáciles de grabar
   - **Solución:** División estratificada, métricas balanceadas (F1-Score)

---

## Tecnologías Utilizadas

### Lenguaje y Entorno
- **Python 3.8+**
- **Jupyter Notebooks**

### Librerías Principales

**Procesamiento de Audio:**
- `librosa` — Extracción de características acústicas
- `soundfile` — Lectura/escritura de archivos de audio
- `scipy` — Procesamiento de señales

**Machine Learning:**
- `scikit-learn` — Modelos de clasificación, clustering, PCA
- `numpy` — Operaciones numéricas
- `pandas` — Manipulación de datos

**Visualización:**
- `matplotlib` — Gráficos básicos
- `seaborn` — Visualizaciones estadísticas
- `plotly` — Gráficos interactivos (opcional)

**Utilidades:**
- `tqdm` — Barras de progreso
- `joblib` — Serialización de modelos

## Configuración e Instalación

### Requisitos Previos

- Python 3.8 o superior
- pip (gestor de paquetes de Python)
- Jupyter Notebook o JupyterLab

### Instalación de Dependencias

```bash
# Instalar librerías necesarias
pip install librosa soundfile scikit-learn pandas numpy matplotlib seaborn scipy tqdm
```

O mediante archivo de requisitos:

```bash
pip install -r requirements.txt
```

### Archivos de Audio Requeridos

**IMPORTANTE:** Los archivos de audio NO están incluidos en este repositorio debido a su tamaño. Para ejecutar el análisis completo, es necesario descargar los audios del Google Drive.

#### Pasos para configurar el dataset:

1. **Descargar los audios** desde la [Carpeta en Google Drive](https://drive.google.com/drive/folders/1y7ibtNqqgdMhxik_176RQQprkYSIPpYf?usp=sharing)

2. **Crear la estructura de carpetas** en el directorio raíz del proyecto:
   ```
   Detector-de-Sonidos-para-Seguridad-en-el-Hogar/
   ├── audios/
   │   ├── agua_corriendo/          (40 archivos .mp3)
   │   ├── alarma_humo/             (40 archivos .mp3)
   │   ├── estufa_prendiendose/     (40 archivos .mp3)
   │   ├── golpe_puerta/            (40 archivos .mp3)
   │   └── vidrio_rompiendose/      (40 archivos .mp3)
   ├── 01-exploratory_data_analysis.ipynb
   ├── 02-supervised_learning_models.ipynb
   ├── 03-unsupervised_learning.ipynb
   ├── diagrama.png
   └── README.md
   ```

3. **Verificar la estructura** ejecutando el notebook `01-exploratory_data_analysis.ipynb`

> **Nota:** Sin los archivos de audio, los notebooks no podrán ejecutarse correctamente.

---

## Cómo Usar Este Proyecto

### Ejecución Paso a Paso

1. **Clonar el repositorio:**
   ```bash
   git clone https://github.com/JuanFernandoBallesterosMaciasUIS/Detector-de-Sonidos-para-Seguridad-en-el-Hogar.git
   cd Detector-de-Sonidos-para-Seguridad-en-el-Hogar
   ```

2. **Instalar dependencias:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Descargar y configurar los audios** según las instrucciones anteriores

4. **Ejecutar los notebooks en orden:**
   - `01-exploratory_data_analysis.ipynb` — Análisis exploratorio
   - `02-supervised_learning_models.ipynb` — Entrenamiento de modelos supervisados
   - `03-unsupervised_learning.ipynb` — Clustering y reducción dimensional

### Uso del Modelo Entrenado

```python
import joblib
import librosa
import numpy as np

# Cargar el modelo entrenado
model = joblib.load('random_forest_model.pkl')

# Cargar y procesar un audio nuevo
audio, sr = librosa.load('nuevo_sonido.mp3', sr=22050)

# Extraer características (mismas 70 features del entrenamiento)
features = extract_features(audio, sr)  # Función definida en el notebook

# Realizar predicción
prediction = model.predict([features])
probability = model.predict_proba([features])

print(f"Clase predicha: {prediction[0]}")
print(f"Confianza: {max(probability[0])*100:.2f}%")
```

---

## Conclusiones y Trabajo Futuro

### Conclusiones Principales

1. **Viabilidad Técnica Confirmada:** Es posible clasificar sonidos de seguridad doméstica con alta precisión (97.5%) usando características acústicas tradicionales y Random Forest.

2. **Características Discriminativas:** Los MFCCs y características espectrales son suficientemente informativos para separar las 5 categorías de sonidos.

3. **Clustering Valida Estructura:** Los algoritmos no supervisados confirman que existen agrupaciones naturales en los datos acústicos, validando la calidad de las características extraídas.

4. **Reducción Dimensional No Recomendada:** Para aplicaciones de seguridad, mantener las 70 características originales es crucial. La reducción dimensional sacrifica precisión inaceptable (de 97.5% a 87.5%).

5. **Simplicidad vs Complejidad:** Random Forest superó a modelos más complejos (SVM con kernel RBF) manteniendo rapidez de inferencia.

### Limitaciones Actuales

- **Tamaño del Dataset:** 200 muestras es moderado; más datos mejorarían generalización
- **Ambiente Controlado:** Los audios provienen de grabaciones relativamente limpias
- **Categorías Limitadas:** Solo 5 tipos de eventos monitoreados
- **Sin Tiempo Real:** El sistema actual no está optimizado para inferencia en tiempo real

### Trabajo Futuro

#### Corto Plazo
- **Aumento de Datos:** Implementar data augmentation (pitch shifting, time stretching, adición de ruido)
- **Más Categorías:** Incluir sonidos como timbre, teléfono, llanto de bebé, ladridos
- **Optimización de Modelo:** Probar redes neuronales (CNN 1D, RNN) para mejorar accuracy

#### Mediano Plazo
- **Implementación en Tiempo Real:** Desarrollar sistema de inferencia continua con ventanas deslizantes
- **Edge Computing:** Portar modelo a dispositivos IoT (Raspberry Pi, ESP32)
- **Interfaz de Usuario:** Crear aplicación web/móvil para monitoreo y alertas

#### Largo Plazo
- **Transfer Learning:** Utilizar modelos pre-entrenados (AudioSet, VGGish)
- **Detección Multiclase Simultánea:** Identificar múltiples sonidos concurrentes
- **Localización Espacial:** Integrar múltiples micrófonos para ubicar fuente sonora
- **Integración con Domótica:** Conectar con sistemas de automatización del hogar (Google Home, Alexa)

---

## Contribuciones y Licencia

### Autores
Este proyecto fue desarrollado como parte del curso Inteligencia Artificial I (2025-2 C1) por:
- **Juan Fernando Ballesteros Macias** (2224653)
- **Juan Pablo Herrera Baquero** (2224512)

### Agradecimientos
- **Pixabay.com** por proporcionar los efectos de sonido de dominio público
- **Librosa Community** por la excelente librería de procesamiento de audio
- **Scikit-learn Team** por las herramientas de Machine Learning

### Licencia
Este proyecto es de uso académico. Los audios utilizados provienen de Pixabay y están sujetos a la licencia de contenido gratuito de dicha plataforma.

---

## Referencias

### Librerías y Herramientas
- Librosa: https://librosa.org/
- Scikit-learn: https://scikit-learn.org/
- Pixabay Sound Effects: https://pixabay.com/es/sound-effects/

### Documentación Técnica
- McFee, B., et al. (2015). "librosa: Audio and Music Signal Analysis in Python"
- Pedregosa, F., et al. (2011). "Scikit-learn: Machine Learning in Python"

### Contacto
Para consultas o colaboraciones:
- Juan Fernando Ballesteros: [GitHub Profile](https://github.com/JuanFernandoBallesterosMaciasUIS)
- Repositorio del Proyecto: [Detector-de-Sonidos-para-Seguridad-en-el-Hogar](https://github.com/JuanFernandoBallesterosMaciasUIS/Detector-de-Sonidos-para-Seguridad-en-el-Hogar)

---

**Última actualización:** 23 de noviembre de 2025  
**Estado del Proyecto:** Completado ✓
