# Predicción de Biomarcadores Genéticos mediante Machine Learning

Este proyecto aplica técnicas de Machine Learning para analizar datos de expresión genética (RNA-seq) e identificar biomarcadores clave. El objetivo es construir un modelo predictivo robusto capaz de determinar [Inserta aquí tu Target, ej: niveles de progresión de una enfermedad] a partir de perfiles moleculares.

Problema de Negocio:
En la medicina de precisión, identificar qué genes influyen en una patología es crítico. Este proyecto busca:
* Automatizar la predicción de [Tu Target] reduciendo costes de diagnóstico.
* Identificar genes "estrella" que puedan servir como dianas terapéuticas.

Dataset:
El conjunto de datos contiene miles de variables de expresión génica. Durante el Análisis Exploratorio de Datos (EDA), se identificaron los siguientes biomarcadores con mayor relevancia:
1. **NCRNA00181** (Principal predictor)
2. **NDUFA11**
3. **HSPBP1**

Metodología:
Se implementó un **Pipeline** de Scikit-Learn que incluye:
* **Imputación:** Manejo de valores nulos mediante `SimpleImputer`.
* **Escalado:** Normalización de datos con `StandardScaler`.
* **Modelo:** Tras comparar varios algoritmos (Regresión Lineal, SVR, Random Forest), se seleccionó **Random Forest Regressor** por su capacidad para manejar relaciones no lineales.
* **Optimización:** Ajuste de hiperparámetros mediante `GridSearchCV`.

Resultados:
El modelo final alcanzó las siguientes métricas en el conjunto de test:
* **R² Score:** 0.82 (Explica el 82% de la varianza de los datos).
* **MAE (Error Medio Absoluto):** 0.34.

Estructura del Repositorio:
* `notebooks/`: Contiene el análisis exploratorio y el entrenamiento del modelo.
* `models/`: Incluye el modelo final guardado en formato `.pkl`.
* `data/`: (Opcional) Datos utilizados en el proyecto.
