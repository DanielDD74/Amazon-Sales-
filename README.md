# 📊 Amazon Sales Data Analysis

Análisis exploratorio y de negocio de un dataset de ventas de Amazon, enfocado en evaluar el desempeño comercial mediante procesos de **limpieza, validación, transformación, análisis de datos y visualización en Power BI**.

El proyecto busca responder preguntas clave del negocio relacionadas con ingresos, comportamiento de compra y desempeño por categoría.

---

## 🎯 Objetivo del proyecto

Analizar los datos históricos de ventas para obtener indicadores que permitan comprender el comportamiento comercial y responder las siguientes preguntas:

* ¿Cuál es el ingreso total (`Revenue`)?
* ¿Cuál es el ticket promedio por orden?
* ¿Cuál es la cantidad promedio de productos por orden?
* ¿Cuál es la categoría más vendida?
* ¿Cómo se distribuyen las ventas entre las diferentes categorías?

---

## 🛠️ Tecnologías utilizadas

* **Python**
* **Pandas** — limpieza, transformación y análisis de datos
* **NumPy** — operaciones y cálculos numéricos
* **Matplotlib** — visualización de datos
* **Seaborn** — visualización exploratoria
* **SciPy** — análisis estadístico
* **Jupyter Notebook** — desarrollo y documentación del análisis
* **Power BI** — dashboard e indicadores de negocio
* **CSV** — fuente y almacenamiento de los datasets

---

# 🔄 Flujo del proyecto

```text
Dataset original
       │
       ▼
Carga de datos con Pandas
       │
       ▼
Exploración inicial
       │
       ▼
Limpieza de datos
       │
       ▼
Validación de calidad
       │
       ▼
Transformación
       │
       ▼
Análisis de KPIs
       │
       ├── Revenue total
       ├── Ticket promedio
       ├── Productos promedio por orden
       └── Ventas por categoría
       │
       ▼
Visualización con Matplotlib / Seaborn
       │
       ▼
Dashboard en Power BI
       │
       ▼
Insights de negocio
```

---

# 🧹 1. Limpieza y preparación de datos

El dataset original fue cargado utilizando Pandas:

```python
import pandas as pd

df = pd.read_csv("amazon_sales_dataset.csv")
```

Posteriormente se realizó una revisión de la estructura y calidad de los datos mediante:

```python
df.info()
df.describe()
df.isnull().sum()
df.duplicated().sum()
df.dtypes
```

### Procesos realizados

* Identificación de valores nulos.
* Detección de registros duplicados.
* Validación de tipos de datos.
* Revisión de valores inconsistentes.
* Conversión de columnas al tipo de dato correspondiente.
* Validación de variables numéricas.
* Revisión de categorías y valores únicos.
* Preparación del dataset para el análisis.

Las columnas de texto fueron normalizadas según su naturaleza y las variables numéricas fueron verificadas para asegurar que pudieran utilizarse correctamente en los cálculos.

Después del proceso de limpieza, se generó un nuevo dataset:

```python
df.to_csv("amazon_sales_clean.csv", index=False)
```

De esta manera se conserva el dataset original y se genera una versión preparada para análisis.

---

# 🔍 2. Validación de información

Antes de calcular los indicadores se realizaron validaciones para comprobar la consistencia de la información.

Algunas de las validaciones realizadas fueron:

```python
df.isnull().sum()
```

para identificar valores faltantes.

```python
df.duplicated().sum()
```

para detectar registros duplicados.

```python
df.dtypes
```

para verificar los tipos de datos.

También se revisaron los valores únicos de variables categóricas para identificar posibles inconsistencias en la clasificación de los productos.

El objetivo de esta etapa fue evitar que datos incompletos, duplicados o incorrectamente tipados afectaran los indicadores finales.

---

# 📈 3. Análisis del negocio

## 💰 Ingreso total

El ingreso total se obtuvo mediante la suma del revenue generado por las órdenes:

```python
revenue_total = df["Total Revenue"].sum()
```

**Resultado:**

> 💰 **Revenue total: $32866573.74

Este indicador representa el valor monetario total generado por las ventas incluidas en el dataset.

---

## 🧾 Ticket promedio por orden

El ticket promedio representa el ingreso promedio generado por cada orden.

Conceptualmente:

```text
Ticket promedio =
Revenue total / Número de órdenes
```

En Python:

```python
ticket_promedio = (
    df["Total Revenue"].sum() /
    df["Order ID"].nunique()
)
```

**Resultado:**

> 🧾 **Ticket promedio: $657.3314748

Este KPI permite conocer cuánto valor genera, en promedio, cada orden realizada.

---

## 📦 Cantidad promedio de productos por orden

Para conocer cuántos productos contiene una orden en promedio:

```python
productos_promedio = (
    df.groupby("Order ID")["Quantity"]
      .sum()
      .mean()
)
```

**Resultado:**

> 📦 **Productos promedio por orden: 2.9

Este indicador permite analizar el tamaño promedio de las órdenes y el comportamiento de compra de los clientes.

---

# 🏆 4. Categoría más vendida

Para identificar la categoría con mayor volumen de productos vendidos:

```python
ventas_categoria = (
    df.groupby("Product Category")["Quantity"]
      .sum()
      .sort_values(ascending=False)
)

ventas_categoria
```

La categoría con mayor cantidad de productos vendidos se obtiene mediante:

```python
categoria_mas_vendida = ventas_categoria.idxmax()

categoria_mas_vendida
```

**Resultado:**

> 🏆 **Categoría más vendida: Beauty

También se generó una visualización para comparar el volumen de ventas entre categorías.

---

# 📊 5. Visualización con Python

Se utilizó **Matplotlib** para representar gráficamente las ventas por categoría.

```python
plt.figure(figsize=(10, 5))

barras = plt.bar(
    ventas_categoria.index,
    ventas_categoria.values
)

plt.title("Ventas totales por categoría")
plt.xlabel("Categoría")
plt.ylabel("Cantidad de productos vendidos")
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

La visualización permite identificar rápidamente las diferencias de volumen entre categorías y facilita la interpretación de los resultados obtenidos mediante Pandas.

---

# 📊 6. Dashboard en Power BI

Los datos previamente limpiados y validados fueron utilizados para construir una visualización interactiva en **Power BI**.

El dashboard permite analizar:

* Revenue total.
* Ticket promedio.
* Cantidad promedio de productos por orden.
* Ventas por categoría.
* Distribución del desempeño comercial.
* Comparación entre categorías.

### Proceso de integración

```text
Amazon Sales Dataset
        ↓
Python / Pandas
        ↓
Limpieza y validación
        ↓
amazon_sales_clean.csv
        ↓
Power BI
        ↓
Dashboard
        ↓
Indicadores de negocio
```

La separación entre la etapa de preparación en Python y la etapa de visualización en Power BI permite mantener un flujo de trabajo reproducible y facilitar futuras actualizaciones del análisis.

---

# 💡 Insights de negocio

A partir del análisis se identificaron los siguientes aspectos:

* El dataset permite obtener una visión general del desempeño comercial mediante indicadores de ingresos y comportamiento de las órdenes.
* El **revenue total** permite dimensionar el volumen económico generado durante el periodo analizado.
* El **ticket promedio** permite conocer el valor monetario promedio de cada orden.
* La **cantidad promedio de productos por orden** permite analizar el tamaño de las compras.
* El análisis por categoría permite identificar qué líneas de productos concentran el mayor volumen de unidades vendidas.
* La visualización en Power BI facilita la exploración de los indicadores y la comunicación de resultados.

---

# 📁 Estructura del proyecto

```text
Amazon-Sales-Analysis/
│
├── data/
│   ├── amazon_sales_dataset.csv
│   └── amazon_sales_clean.csv
│
├── notebooks/
│   └── amazon_sales_analysis.ipynb
│
├── powerbi/
│   └── amazon_sales_dashboard.pbix
│
├── visualizations/
│   └── sales_by_category.png
│
└── README.md
```

---

# 🚀 Principales habilidades demostradas

### Data Cleaning

* Tratamiento de valores faltantes.
* Detección de duplicados.
* Validación de tipos de datos.
* Identificación de inconsistencias.
* Preparación de datasets para análisis.

### Data Analysis

* Agregaciones con `groupby()`.
* Cálculo de KPIs.
* Análisis de revenue.
* Cálculo de ticket promedio.
* Análisis de volumen de productos.
* Ranking de categorías.

### Data Visualization

* Matplotlib.
* Seaborn.
* Power BI.
* Construcción de indicadores.
* Visualización orientada a negocio.

### Herramientas

```text
Python
├── Pandas
├── NumPy
├── Matplotlib
├── Seaborn
└── SciPy

BI
└── Power BI

Environment
└── Jupyter Notebook
```

---

# 📌 Conclusión

Este proyecto demuestra un flujo completo de análisis de datos, desde la **preparación y validación de información hasta la generación de indicadores y visualizaciones orientadas al negocio**.

El proceso permitió transformar un dataset de ventas en información estructurada para responder preguntas comerciales relacionadas con **ingresos, comportamiento de las órdenes y desempeño por categoría**.

El proyecto forma parte de mi portafolio como **Junior Data Analyst**, con enfoque en Python, SQL, Power BI y análisis de datos orientado a la toma de decisiones.
