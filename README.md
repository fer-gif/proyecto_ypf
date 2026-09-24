# Análisis de actividad sísmica en Argentina

## Dataset

Para este proyecto se utilizaron datos sísmicos pertenecientes al *United States Geological Survey (USGS)*. El dataset contiene registros de eventos sísmicos ocurridos en Argentina durante el período 2016 – 2026, incluyendo variables como fecha y hora, ubicación geográfica, profundidad y magnitud, entre otras.

**Fuente:** [USGS Earthquake Catalog](https://earthquake.usgs.gov/earthquakes/search/)

---

## Resumen del proyecto

Caracterizar la actividad sísmica de Argentina mediante el análisis exploratorio de datos y técnicas de aprendizaje automático, con el propósito de identificar patrones espaciales y temporales y desarrollar una representación de las regiones según su comportamiento sísmico.

---

## Objetivos

* Realizar un análisis exploratorio y construir variables que permitan caracterizar la actividad sísmica.
* Analizar la distribución espacio-temporal de los eventos.
* Identificar grupos de regiones con características sísmicas similares mediante aprendizaje no supervisado.
* Desarrollar un modelo supervisado para estimar la probabilidad de actividad sísmica significativa en un período posterior.

---

### 1. Análisis exploratorio

Explorar, comprender y limpiar el conjunto de datos, evaluando su estructura, calidad, consistencia y posibles valores faltantes o atípicos, para obtener un dataset adecuado para el análisis y el modelado.

---

### 2. Modelo supervisado

El objetivo del análisis supervisado es evaluar si la actividad sísmica registrada previamente en una región puede utilizarse para estimar su comportamiento en un período posterior, a partir de los patrones observados en los datos históricos.

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
│   └── raw/
│       ├── sismos_usgs.csv
│       └── geodata/
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
│
├── notebooks/
│   ├── 01_analisis_exploratorio.ipynb

```

---

## Librerías utilizadas

* Requests
* Pandas
* Matplotlib
* GeoPandas
* Shapely
* Io

---

## Integrantes del equipo

Carina Dellasanta
Fermín Hernando
Sergio Mamani

Proyecto realizado en el marco del curso **Data Science + IA — Fundación YPF**.