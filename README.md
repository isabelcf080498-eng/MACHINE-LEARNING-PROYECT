# Predicción de Agresividad Tumoral mediante Machine Learning y Biomarcadores Transcriptómicos

## Descripción del Proyecto

Este proyecto tiene como objetivo desarrollar un modelo de Machine Learning capaz de predecir el estadio patológico de un tumor utilizando información derivada de la expresión génica (biomarcadores transcriptómicos) y variables clínicas asociadas.

El propósito principal es mejorar la estratificación de los pacientes y avanzar en el desarrollo de enfoques de medicina personalizada y oncología computacional.

## Metodología y Flujo de Trabajo

El proyecto se dividió en dos fases principales.

### 1. Exploratory Data Analysis (EDA) y Selección de Biomarcadores

Para hacer frente a la alta dimensionalidad de los datos transcriptómicos y reducir el riesgo de *overfitting*, se aplicaron técnicas de reducción de dimensionalidad y análisis de redes de coexpresión génica.

Se seleccionaron los **10 genes más relevantes** basándose en su alta conectividad dentro de la red y su correlación con el fenotipo clínico.

A estos genes se les sumó la variable clínica `years_to_birth` (edad del paciente en el diagnóstico), formando las variables predictoras (*features*).

### 2. Preprocesamiento y Modelado

**Prevención de Data Leakage**

Se dividió el dataset en conjuntos de *training* y *test* antes de aplicar transformaciones.

**Balanceo de Clases**

Para evitar que el modelo favoreciera a la clase mayoritaria (problema común en datos médicos), se aplicó la técnica de sobremuestreo **SMOTE** únicamente en el conjunto de entrenamiento.

**Pipeline de Scikit-Learn**

Se construyó un pipeline reproducible que incluye estandarización (`StandardScaler`) y el propio algoritmo predictivo.

## Estrategia y Resultados

Inicialmente el problema se abordó como una clasificación multiclase (Estadios I, II, III y IV). Sin embargo, ante un rendimiento moderado, el problema se reformuló como una **clasificación binaria (Estadio Temprano vs. Estadio Tardío)**. Esta reformulación permitió aumentar el número de muestras por clase y reflejar una distinción más útil desde el punto de vista clínico.

Tras optimizar hiperparámetros mediante *GridSearchCV* (ajustando variables como `n_estimators` y `max_depth`) y comparar diversos algoritmos (Regresión Logística, SVM y Gradient Boosting), el **modelo con mejor rendimiento fue Random Forest**.

### Métricas del modelo final sobre el Test Set ciego

- **Recall (Sensibilidad): 81.82%**  
  El modelo logra detectar correctamente a 82 de cada 100 pacientes que realmente se encuentran en una fase tardía de la enfermedad.

- **Precisión: 71.05%**  
  De todas las predicciones de "Estadio Tardío", aproximadamente 7 de cada 10 corresponden a casos reales.

- **F1-Score: 0.76**  
  Indica un equilibrio adecuado entre sensibilidad y precisión.

**Nota de interpretabilidad**

El análisis de *feature importance* reveló que la edad (`years_to_birth`) es el principal indicador de la agresividad tumoral para este modelo, seguido de varios de los genes seleccionados como WISP2 y LRRC15.

## Limitaciones y Trabajo Futuro

### Limitaciones actuales

- Tamaño de dataset relativamente reducido.
- Número limitado de biomarcadores evaluados, cuya relevancia debe ser contrastada con literatura experimental.
- Ausencia de validación con datos externos.

### Posibles mejoras futuras

**Validación multicéntrica**

Evaluar el modelo con datos de diferentes hospitales para comprobar su robustez.

**Integración multi-ómica**

Combinar estos datos con mutaciones genómicas o datos proteómicos para aumentar la capacidad predictiva.

**Interpretabilidad avanzada**

Uso de valores SHAP para explicar predicciones de forma individualizada para cada paciente.

**Despliegue**

Integración del modelo como Sistema de Apoyo a la Decisión Clínica (CDSS) en entornos médicos.

+ ENLACE A VIDEOPRESENTACIÓN: https://drive.google.com/file/d/1H5MDEPGc270FwTEMorTkVsPyjw7aRgQq/view?usp=drive_link
