# Laboratorio 5: Comparativa de Preprocesamiento para RNA en Detección de Complicaciones por Infarto

**Autores:**
- Ana Sofia Arango Yanza
- Juan David Vela Coronado

## 1. Objetivo del Proyecto

El objetivo de este laboratorio fue entrenar y evaluar una Red Neuronal Artificial (RNA) para clasificar las complicaciones de un infarto de miocardio. El foco principal del análisis es comparar el impacto de dos estrategias de preprocesamiento de datos sobre el rendimiento del modelo:

1.  **Modelo 1:** Un pipeline de preprocesamiento propio, que incluye limpieza, imputación de datos y balanceo de clases con SMOTENC.
2.  **Modelo 2:** El mismo modelo de RNA entrenado con un conjunto de datos pre-imputado y proporcionado por el docente.

## 2. Estructura del Repositorio

*   `Laboratorio_No_5_Pt1_RNA_(Dataset_Myocardial).ipynb`: Contiene el código para el preprocesamiento de datos propio y el entrenamiento del **Modelo 1**.
*   `Laboratorio_No_5_Pt2_y_Pt3_RNA_(Dataset_Myocardial).ipynb`: Contiene el entrenamiento del **Modelo 2** con los datos proporcionados y la comparación final entre ambos modelos.
*   `data/`: Carpeta con los archivos CSV proporcionados (`X_imp_train.csv`, `y_imp_train.csv`, etc.).
*   `README.md`: Este documento.

## 3. Metodología

-   **Modelo:** Se utilizó un `MLPClassifier` de Scikit-learn con una arquitectura de dos capas ocultas `(10, 8)` y optimizador 'adam' en todos los experimentos para garantizar una comparación justa.
-   **Preprocesamiento (Modelo 1):** Se realizó una selección de características basada en las recomendaciones del dataset, se imputaron valores faltantes usando la **mediana** para variables numéricas y la **moda** para categóricas. El desbalance de clases se manejó con la técnica **SMOTENC**, ideal para datasets con variables mixtas (numéricas y categóricas).
-   **Evaluación:** El rendimiento de cada modelo se midió utilizando el reporte de clasificación (Precisión, Recall, F1-Score) y la matriz de confusión multiclase.

## 4. Resultados y Conclusión

La comparación de los modelos demostró de forma contundente la importancia de un preprocesamiento adecuado en problemas con datos desbalanceados.

| Métrica Clave | Modelo 1 (Preprocesamiento Propio) | Modelo 2 (Datos del Profesor) | Observación |
| :--- | :---: | :---: | :--- |
| **Accuracy General (Balanceado + Normalizado)** | 0.751 | 0.683 | Mi preprocesamiento retuvo una mayor precisión general. |
| **Capacidad de Detección** | **Detectó 7 de 8** complicaciones | **Detectó 5 de 8** complicaciones | Mi modelo fue capaz de generalizar y predecir un mayor número de clases minoritarias. |
| **F1-Score (Edema Pulmonar)** | **0.267** | 0.087 | Mi modelo mostró un rendimiento significativamente superior en la detección de esta complicación. |
| **F1-Score (Ruptura Miocárdica)** | **0.129** | 0.000 | Mi modelo pudo identificar esta complicación, mientras que el otro no. |

### **Conclusión Final**

Aunque los modelos base (sin balancear) mostraron una alta precisión, esta era engañosa, ya que fallaban en detectar las complicaciones reales.

El análisis final demuestra que **mi enfoque de preprocesamiento (Modelo 1) fue más efectivo**. La combinación de imputación selectiva y balanceo con SMOTENC permitió a la red neuronal aprender patrones de las clases minoritarias de manera más robusta.

En un problema clínico, es preferible un modelo con menor precisión general pero mayor capacidad para detectar eventos raros y críticos. Por lo tanto, se concluye que mi pipeline de preprocesamiento generó un conjunto de datos más adecuado para entrenar un modelo clínicamente relevante.

## 5. Cómo Ejecutar

1.  Asegurarse de tener las librerías de Python instaladas: `pandas`, `scikit-learn`, `imblearn`, `matplotlib`, `seaborn` y `ucimlrepo`.
2.  Abrir los archivos `.ipynb` en un entorno como Jupyter Notebook o Google Colab.
3.  Ejecutar las celdas en el orden presentado.
