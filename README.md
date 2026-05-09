# Grupo12\_Taller\_Modelos\_No\_Supervisados

## Descripción del proyecto

Este repositorio contiene la estructura de trabajo para el taller académico de **modelos no supervisados**, aplicado a un dataset relacionado con información salarial de Cervecería Nacional.

El objetivo general del proyecto es analizar patrones en los datos y desarrollar modelos no supervisados que permitan identificar agrupaciones, comportamientos atípicos o posibles registros que requieran revisión adicional.

## Problema de análisis sugerido

**¿Es posible identificar registros salariales atípicos dentro de la nómina de Cervecería Nacional mediante modelos no supervisados, utilizando variables como salario base, horas extra, otros pagos, beneficios y pago total?**

Este enfoque permite aplicar técnicas como detección de anomalías, segmentación y análisis exploratorio sin utilizar una variable objetivo supervisada.

## Dataset utilizado

El dataset principal se encuentra en:

```text
data/raw/Salarios\\\_Cerveceria.csv
```

Este archivo contiene información relacionada con remuneraciones, cargos, departamentos, beneficios, pagos adicionales y tipo de contrato.

## Notebook principal

El notebook preparado para el desarrollo de la tarea se encuentra en:

```text
notebooks/01\\\_modelos\\\_no\\\_supervisados\\\_cerveceria.ipynb
```

También se conserva el notebook original recibido como referencia de clase:

```text
notebooks/00\\\_notebook\\\_base\\\_clase\\\_original\\\_Grupo12\\\_A1\\\_S3.ipynb
```

## Modelos sugeridos para el desarrollo

Para el análisis no supervisado se recomienda considerar:

* **Local Outlier Factor, LOF**, para detección de anomalías locales.
* **Isolation Forest**, para detección de registros atípicos.
* **K-Means**, para segmentación de perfiles salariales.
* **PCA**, para reducción de dimensionalidad y visualización de patrones.

## Estructura del repositorio

```text
Grupo12\\\_Taller\\\_Modelos\\\_No\\\_Supervisados/
│
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
│
├── data/
│   ├── raw/
│   │   └── Salarios\\\_Cerveceria.csv
│   │
│   └── processed/
│       └── .gitkeep
│
├── notebooks/
│   ├── 00\\\_notebook\\\_base\\\_clase\\\_original\\\_Grupo12\\\_A1\\\_S3.ipynb
│   └── 01\\\_modelos\\\_no\\\_supervisados\\\_cerveceria.ipynb
│
├── reports/
│   └── README.md
│
├── images/
│   └── README.md
│
└── docs/
    └── README.md
```

## Buenas prácticas aplicadas

* Separación entre datos originales, datos procesados, notebooks, reportes, imágenes y documentos de apoyo.
* Inclusión de archivo `requirements.txt` con las librerías necesarias.
* Inclusión de `.gitignore` para evitar subir archivos temporales o innecesarios.
* Conservación del dataset original dentro de `data/raw/`.
* Conservación del notebook original recibido como respaldo.
* Uso de nombres de archivos claros, sin espacios ni tildes.

## Integrantes

* Schubert Stalin Lombeida Manjarrez
* José Luis Peñafiel Fernández
* Juan Carlos Bajaña Gutiérrez
* Niko Dimitri Jiménez Bruno

## Herramientas utilizadas

* Python
* Google Colab / Jupyter Notebook
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* GitHub

## Nota académica

Los registros detectados como atípicos no deben interpretarse automáticamente como errores, fraudes o irregularidades. Deben considerarse como observaciones que presentan un comportamiento diferente al patrón general y que podrían requerir una revisión administrativa, técnica o estadística adicional.

