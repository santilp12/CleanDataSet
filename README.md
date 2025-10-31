# 🧹✨ Clean_Exhaustive: Guía de Limpieza de Datos ✨🧹

Este repositorio contiene un notebook de Jupyter (`CleanExhaustive.ipynb`) que sirve como una plantilla exhaustiva y un tutorial paso a paso para el proceso de **limpieza y preprocesamiento de datos** (Data Cleaning).

El proyecto, desarrollado por Santiago Londoño Pérez, aplica un conjunto robusto de técnicas de limpieza a un dataset de **clientes bancarios** (`Bank_Clients.csv`) con el objetivo de prepararlo para un análisis exploratorio (EDA) o la construcción de modelos de machine learning.

##  metodológica de Limpieza

El notebook sigue un flujo de trabajo estructurado, abordando sistemáticamente los problemas más comunes en un conjunto de datos del mundo real.

### 1. Vistazo Inicial
* **Carga de datos:** `pd.read_csv('Bank_Clients.csv')`.
* **Exploración básica:** Uso de `df.head()`, `df.info()`, `df.describe()` y `df.shape` para entender la estructura, los tipos de datos y las estadísticas descriptivas iniciales.

### 2. Detección y Manejo de Duplicados
* Identificación de filas duplicadas exactas usando `df.duplicated().sum()`.
* Eliminación de duplicados para asegurar la integridad del dataset.

### 3. Análisis de Valores Faltantes (NaNs)
* Análisis cuantitativo con `df.isnull().sum()`.
* **Visualización avanzada** de patrones de nulidad usando la librería `missingno` (gráficos `msno.matrix` y `msno.heatmap`).
* **Estrategia de imputación:**
    * **Numéricos:** Imputación de `Credit_Limit` y `Total_Revolving_Bal` con la **mediana**, una medida robusta ante outliers.
    * **Categóricos:** Imputación de `Gender` con la categoría 'Desconocido'.
    * **Eliminación:** Descarte de columnas con un porcentaje excesivamente alto de valores faltantes.

### 4. Limpieza Categórica y de Texto
* Estandarización de valores únicos (ej. `M` -> `Male`, `F` -> `Female`).
* Análisis de `value_counts()` para identificar categorías ambiguas (ej. 'Unknown').
* Reemplazo de valores 'Unknown' en `Education_Level` por la **moda** (el valor más frecuente).

### 5. Detección y Manejo de Outliers
* Visualización de distribuciones usando `sns.boxplot` para variables como `Customer_Age` y `Credit_Limit`.
* Identificación de outliers usando el método del **Rango Intercuartílico (IQR)**.
* Aplicación de la técnica de **Capping (Winsorización)** con `np.clip` para acotar los valores atípicos a un umbral razonable (percentil 5 y 95) sin eliminarlos, preservando así la información.

### 6. Ingeniería de Características (Feature Engineering)
* **Discretización:** Creación de una nueva columna `Age_Group` (grupos de edad) a partir de `Customer_Age` usando `pd.cut`.
* **Creación de Ratios:** Creación de la columna `Utilization_Ratio` (Tasa de Utilización) como `Total_Revolving_Bal` / `Credit_Limit`, una métrica clave en el análisis bancario.

## 💾 Resultado Final

El proceso concluye con la exportación de un conjunto de datos limpio y listo para el análisis, guardado como **`Bank_Clients_Cleaned.csv`**.

## 🛠️ Librerías Utilizadas

Este proyecto utiliza el stack estándar de Data Science en Python:

* **Pandas:** Para la manipulación y análisis de datos.
* **NumPy:** Para operaciones numéricas y el manejo de outliers.
* **Matplotlib & Seaborn:** Para la visualización de datos (boxplots, etc.).
* **Missingno:** Para la visualización avanzada de valores faltantes.
