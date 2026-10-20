# Análisis de actividad sísmica en Argentina

## Dataset

Para este proyecto se utilizaron datos sísmicos pertenecientes al *United States Geological Survey (USGS)*. El dataset contiene registros de eventos sísmicos ocurridos en Argentina durante el período 2016 – 2026, incluyendo variables como fecha y hora, ubicación geográfica, profundidad y magnitud, entre otras.

**Fuente:** [USGS Earthquake Catalog](https://earthquake.usgs.gov/earthquakes/search/)

---

## Resumen del proyecto

Caracterizar la actividad sísmica de Argentina mediante el análisis exploratorio de datos y técnicas de aprendizaje automático, con el propósito de identificar patrones espaciales y temporales así como desarrollar una representación de las regiones según su comportamiento sísmico.

---

## Objetivos

* Realizar un análisis exploratorio y construir variables que permitan caracterizar la actividad sísmica.
* Analizar la distribución espacio-temporal de los eventos.
* Identificar grupos de regiones con características sísmicas similares mediante aprendizaje no supervisado.
* Desarrollar un modelo supervisado de regresión para estimar la cantidad mensual de sismos a partir de la actividad registrada en meses anteriores.

---

### 1. Análisis exploratorio

Explorar, comprender y limpiar el conjunto de datos, evaluando su estructura, calidad, consistencia y posibles valores faltantes o atípicos, para obtener un dataset adecuado para el análisis y el modelado.

---

### 2. Modelo supervisado

El objetivo del análisis supervisado es estimar la cantidad de sismos registrados durante un mes utilizando únicamente información disponible en meses anteriores. La unidad de análisis es el mes, por lo que los registros individuales del catálogo se agregan para obtener una serie temporal mensual.

La variable objetivo es `cantidad_sismos`, es decir, el número de eventos registrados durante el mes. Se construyeron cuatro conjuntos de predictores:

1. **Predictor 1:** cantidad de sismos del mes anterior.
2. **Predictor 2:** cantidad del mes anterior y cantidades acumuladas de los últimos 3 y 6 meses.
3. **Predictor 3:** Predictor 2 más resúmenes mensuales de magnitud y profundidad.
4. **Predictor 4:** Predictor 3 más variables de calidad del registro, como `gap`, `dmin`, `rms`, `horizontalError`, `depthError`, `magError` y `magNst`.

Para evitar la fuga temporal, las variables calculadas a nivel mensual se desplazan un período hacia atrás: la información de un mes se utiliza para predecir el mes siguiente. Se reservan los últimos 12 meses como conjunto de prueba final y la validación se realiza mediante `TimeSeriesSplit`, respetando el orden cronológico.

Se comparan modelos de referencia —persistencia, media del entrenamiento y promedio combinado— con regresión lineal, Random Forest y XGBoost. Para los modelos de aprendizaje automático se utilizan `Pipeline` y `StandardScaler`; además, se realiza una búsqueda acotada de hiperparámetros para Random Forest y XGBoost con validación temporal.

También se analizan dos escenarios para estudiar la influencia del pico de registros de agosto de 2021:

* **Agosto original:** conserva el conteo observado.
* **Agosto reemplazado por la mediana:** reemplaza el conteo mensual extremo por la mediana de los conteos mensuales.

La selección formal del modelo se realiza con las métricas de validación (`MAE` y `RMSE`), mientras que el conjunto de prueba se utiliza posteriormente para informar el rendimiento final. El notebook incluye una etapa preparada para reentrenar el modelo definitivo una vez que el equipo confirme el escenario y la configuración seleccionada. Los resultados se interpretan como un ejercicio académico sobre la cantidad mensual de eventos registrados y no como un sistema de alerta sísmica.

---

### 3. Modelo no supervisado

El objetivo del análisis no supervisado es identificar regiones con patrones similares de actividad sísmica, sin establecer previamente una clasificación de las zonas. A partir de los resultados obtenidos, se buscará caracterizar las diferencias entre las regiones y representar cómo se distribuyen espacialmente.

Esta clasificación puede servir como punto de partida para futuros análisis de riesgo, combinando las regiones según su actividad sísmica con información sobre la población, las características edilicias y otras variables relacionadas con la vulnerabilidad y la exposición. Esto permitiría estudiar qué zonas concentran mayores niveles de peligro y vulnerabilidad, y generar información que pueda ser útil para orientar medidas de prevención y planificación de recursos.

Los resultados también podrán compararse con los obtenidos mediante el modelo supervisado, incorporando una dimensión temporal al análisis según el objetivo definido para dicho modelo.

---


## Estructura del repositorio

```text
├── README.md
│
├── data/
│   ├── raw/
│       ├── sismos_usgs.csv
│       ├── geodata/
│            ├── limites.cpg
│            ├── limites.prj
│            ├── limites.shp
│            ├── limites.shx
│            ├── limites.dbf
│            ├── referencias.cpg
│            ├── referencias.prj
│            ├── referencias.shp
│            ├── referencias.shx
│            ├── referencias.dbf
│            ├── provinciaPolygon.cst
│            ├── provinciaPolygon.prj
│            ├── provinciaPolygon.shp
│            ├── provinciaPolygon.shx
│            ├── provinciaPolygon.dbf
│            ├── plataforma_continentalPolygon.cst
│            ├── plataforma_continentalPolygon.prj
│            ├── plataforma_continentalPolygon.shp
│            ├── plataforma_continentalPolygon.shx
│            └── plataforma_continentalPolygon.dbf
│   └── processed/
│       └── sismos_argentina_limpio.csv
│
├── notebooks/
│   ├── 01_analisis_exploratorio.ipynb
│   ├── 02_transformacion_datos.ipynb
│   └── 03_modelo_supervisado.ipynb

```

---

## Librerías utilizadas

* Requests
* Pandas
* Matplotlib
* GeoPandas
* Shapely
* Io
* PathLib
* NumPy
* Scikit-learn
* XGBoost

---

## Integrantes del equipo

Carina Dellasanta,
Fermín Hernando,
Sergio Mamani

Proyecto realizado en el marco del curso **Data Science + IA — Fundación YPF**.
