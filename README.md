# Grupo12\_Taller\_Modelos\_No\_Supervisados

## Descripción del proyecto

Este repositorio contiene el desarrollo del taller de **modelos no supervisados** aplicado al dataset `Salarios\_Cerveceria\_2025.csv`, relacionado con remuneraciones, horas extra, beneficios y composición salarial de empleados de una cervecería.

El trabajo utiliza técnicas de aprendizaje no supervisado para **segmentar perfiles salariales**, **visualizar patrones de compensación** y **detectar registros atípicos** que pueden requerir revisión administrativa o validación adicional.

> Nota de uso responsable: los registros detectados como anomalías no deben interpretarse automáticamente como errores, fraude o irregularidades comprobadas. Representan observaciones estadísticamente diferentes al patrón general del dataset.

\---

## Problema de análisis

**¿Es posible identificar perfiles salariales diferenciados y registros atípicos dentro de la nómina de Cervecería Nacional mediante modelos no supervisados, utilizando variables de salario total, horas extra, beneficios y proporciones de compensación?**

Este problema es adecuado para aprendizaje no supervisado porque no se utiliza una variable objetivo para entrenar los modelos. Los algoritmos descubren estructuras internas del dataset a partir de similitudes, densidades y distancias entre observaciones.

\---

## Justificación

El análisis de compensaciones permite comprender la estructura salarial de una organización, identificar segmentos de empleados con características similares y detectar combinaciones poco frecuentes entre salario, horas extra y beneficios.

En este caso, los modelos no supervisados aportan valor porque permiten agrupar empleados con perfiles de compensación semejantes, detectar microgrupos, identificar registros con comportamiento atípico y generar insumos para auditoría interna, control de calidad de datos y revisión administrativa.

\---

## Estructura del repositorio

```text
Grupo12\_Taller\_Modelos\_No\_Supervisados/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/Salarios\_Cerveceria\_2025.csv
│   └── processed/Salarios\_Cerveceria\_2025\_procesado.csv
├── notebooks/01\_modelos\_no\_supervisados\_cerveceria.ipynb
├── images/
├── reports/
│   ├── informe\_resultados\_modelos\_no\_supervisados.md
│   ├── informe\_resultados\_modelos\_no\_supervisados.docx
│   ├── resultados\_modelo\_cerveceria.csv
│   └── anomalias\_ambos\_modelos.csv
└── docs/
```

\---

## Dataset utilizado

|Elemento|Valor|
|-|-:|
|Registros originales|8,382|
|Columnas originales|14|
|Año analizado|2025|
|Registros procesados para modelado|8,382|
|Valores faltantes en HorasExtra|150|
|Valores faltantes en Beneficios|377|
|Valores faltantes en TipoContrato|1,200|

Variables derivadas para modelado: `LogSalarioTotal`, `OvertimeRatio`, `BeneficiosRatio`, `ExtraVsBase` y `BeneficiosVsSalario`.

\---

## Metodología aplicada

1. Carga y exploración de datos.
2. Preprocesamiento: conversión de variables, imputación, winsorización IQR y estandarización.
3. Feature engineering con variables proporcionales.
4. Clustering con K-Means y DBSCAN.
5. Reducción de dimensionalidad con PCA.
6. Detección de anomalías con Isolation Forest y LOF.

!\[Distribución por departamentos](images/01\_distribucion\_departamentos.png)

\---

## Resultados principales

### K-Means

Aunque el mejor Silhouette Score se observó en `k=2`, el notebook trabajó con `k=4` para obtener una segmentación más granular e interpretable desde el punto de vista empresarial.

|KMeans\_Cluster|LogSalarioTotal|OvertimeRatio|BeneficiosRatio|ExtraVsBase|BeneficiosVsSalario|Cantidad\_Registros|
|-:|-:|-:|-:|-:|-:|-:|
|0|8.5233|0.2143|0.152|0.2143|0.2041|4095|
|1|7.6656|0.4057|0.544|0.4057|0.9452|812|
|2|7.9395|1.0446|0.3124|1.0446|0.7765|989|
|3|8.0717|0.3816|0.2594|0.3816|0.4129|2486|

!\[Método del codo](images/03\_metodo\_codo\_kmeans.png)

!\[Segmentación K-Means](images/05\_segmentacion\_kmeans.png)

### DBSCAN

DBSCAN identificó **4 clusters sin considerar ruido** y **41 registros clasificados como ruido**.

!\[Segmentación DBSCAN](images/07\_segmentacion\_dbscan.png)

### PCA

PCA conservó aproximadamente **90.7%** de la varianza en dos componentes.

!\[PCA clusters](images/08\_pca\_clusters\_kmeans.png)

### Anomalías

|Modelo|Registros normales|Anomalías detectadas|Porcentaje|
|-|-:|-:|-:|
|Isolation Forest|7,962|420|5.0%|
|Local Outlier Factor|8,214|168|2.0%|
|Coincidencia ambos modelos|No aplica|51|0.6%|

!\[Comparación anomalías](images/13\_comparacion\_cantidad\_anomalias.png)

\---

## Análisis comparativo entre modelos

|Modelo|Fortalezas|Limitaciones|Uso recomendado|
|-|-|-|-|
|K-Means|Segmenta perfiles generales de compensación.|Requiere definir `k` y asigna todos los registros a un cluster.|Identificar grandes perfiles salariales.|
|DBSCAN|Detecta ruido y microgrupos sin definir número de clusters.|Sensible a `eps` y `min\_samples`.|Identificar densidades y posibles outliers.|
|PCA|Facilita visualización y reduce dimensiones.|No es un modelo de clustering.|Visualizar separación de clusters y anomalías.|
|Isolation Forest|Detecta anomalías globales y valores extremos.|Depende del parámetro `contamination`.|Búsqueda amplia de registros atípicos.|
|LOF|Detecta anomalías locales en zonas de baja densidad.|Sensible al número de vecinos.|Confirmar anomalías más diferenciadas localmente.|

\---

## Conclusiones

1. El dataset permite aplicar correctamente modelos no supervisados porque contiene variables numéricas suficientes para representar la estructura salarial.
2. K-Means permitió identificar perfiles salariales diferenciados, especialmente en la relación entre salario total, horas extra y beneficios.
3. DBSCAN complementó el análisis al identificar puntos de ruido y microgrupos basados en densidad.
4. PCA conservó aproximadamente **90.7%** de la varianza en dos componentes.
5. Isolation Forest detectó **420** anomalías, mientras que LOF detectó **168**; ambos modelos coincidieron en **51** registros.
6. Las anomalías deben entenderse como registros que requieren revisión, no como errores confirmados.

## Recomendaciones

* Revisar con mayor detalle los **51 registros detectados por ambos modelos**.
* Validar los resultados con personal de recursos humanos o compensaciones antes de tomar decisiones.
* Mantener el notebook con rutas relativas para que pueda ejecutarse desde el repositorio sin depender de rutas locales.

