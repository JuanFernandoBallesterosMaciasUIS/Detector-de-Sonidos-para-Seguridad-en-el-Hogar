
# Detector de Sonidos para Seguridad en el Hogar — IA1 (2025-2 C1)

**Curso:** Inteligencia Artificial I - 2025-2 C1  
**Equipo:** _(reemplazar con el nombre del equipo)_  
**Integrantes (nombre y código UIS):**  
- _Apellido, Nombre — Código_  
- _Apellido, Nombre — Código_  
- _Apellido, Nombre — Código_

---

## Descripción concisa de los datos a usar
**Dataset:** Sonidos de eventos domésticos (Pixabay SFX) — 5 clases × 30 muestras c/u (≈150 clips, 1–10 s).  
**Fuente:** [Pixabay — Sound Effects](https://pixabay.com/es/sound-effects/search/) y [Carpeta en Google Drive](https://drive.google.com/drive/folders/1y7ibtNqqgdMhxik_176RQQprkYSIPpYf?usp=sharing).  
**Cantidad de datos:**  Se han recopilado 30 muestras de audio por cada una de las 5 categorías (vidrios rompiéndose, alarma de humo, agua corriendo, golpe de puerta, estufa prendiendo), para un total de 150 archivos de audio.

---

## Preguntas a responder

### Antes del EDA (conceptual)
**Problema y relevancia** 
Buscamos desarrollar un sistema de clasificación de sonidos que identifique un rango de eventos acústicos relevantes para la seguridad y el monitoreo del hogar. Este sistema es importante porque puede alertar a los residentes sobre diversas situaciones, como posibles intrusiones, emergencias, descuidos domésticos o el uso no supervisado de electrodomésticos. El objetivo es proporcionar una capa de seguridad, especialmente útil cuando la vivienda está sola o con niños.

**Objetivo del análisis (EDA)**
El Análisis Exploratorio de Datos (EDA) nos permitirá comprender las características acústicas fundamentales de cada categoría de sonido. Mediante la visualización y extracción de propiedades, identificaremos patrones distintivos. Esta fase es crucial para determinar qué características son más informativas y, en consecuencia, guiar la selección de las técnicas de preprocesamiento y los modelos de machine learning más adecuados para construir un clasificador robusto.

**Métricas o indicadores** 
Utilizaremos la Precisión (Accuracy) para una visión general del rendimiento. Sin embargo, dado que un falso negativo (no detectar un evento relevante) es crítico, también emplearemos la Sensibilidad (Recall) y la Puntuación F1 (F1-Score) por clase. Estas métricas aseguran que el modelo sea fiable en la identificación específica de cada uno de los eventos monitoreados.

**Motivación de la elección**
Elegimos este proyecto por su gran aplicabilidad en la vida diaria. La seguridad y el monitoreo del hogar son preocupaciones universales. El análisis de audio ofrece una vía innovadora y de bajo costo para proporcionar tranquilidad a las familias de una manera no invasiva.

### Después del EDA (basado en datos)
**Datos utilizados** 
Se utilizaron archivos de audio en formatos .mp3, descargados de la plataforma Pixabay.com y organizados en una carpeta pública de Google Drive. Los datos son series de tiempo que representan la amplitud del sonido.

**Información contenida en los datos** 
Los eventos de audio combinan transientes (sonidos impulsivos como vidrios rompiéndose, golpe de puerta y la chispa de estufa) y señales sostenidas (como la alarma de humo y el agua corriendo). Características como la energía de la señal (RMS), su periodicidad (ZCR) y descriptores de timbre como los MFCCs serán clave para diferenciarlos. La diversidad de patrones acústicos entre las clases sugiere que un modelo podrá aprender a separarlas eficazmente.

**Desafíos asociados a los datos** 
El principal desafío es el tamaño reducido del dataset (30 muestras por categoría), que podría limitar la capacidad de generalización del modelo. Otro reto es la posible variabilidad dentro de cada clase (ej. diferentes tipos de golpes) y la presencia de ruido de fondo en las muestras. La duración variable de los audios también requerirá un preprocesamiento cuidadoso para estandarizar la entrada del modelo.

---

## Estructura del repositorio (sugerida)
