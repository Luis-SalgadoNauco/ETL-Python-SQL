# ETL-Python-SQL

Repositorio de prácticas y proyecto final del módulo **Herramientas ETL** del curso de Análisis de Datos.

Este repositorio documenta el trabajo realizado durante la **Semana de ETL con Python y SQL**, cuyo foco es el diseño e implementación de procesos ETL (Extract, Transform, Load) a partir de múltiples fuentes de datos, utilizando herramientas ampliamente usadas en la industria.

---

## Descripción de la semana

Durante esta semana se desarrolla un flujo ETL completo, comenzando por la extracción de datos desde distintas fuentes, continuando con procesos de transformación y limpieza, y finalizando con la carga de datos y el manejo de errores.

El trabajo se realiza de forma incremental, permitiendo comprender cada etapa del proceso y su impacto en la calidad de los datos y en el análisis posterior.

---

## Objetivos generales

- Comprender la arquitectura y el flujo de un proceso ETL.
- Extraer datos desde múltiples fuentes utilizando Python y SQL.
- Limpiar, transformar y validar datos con Pandas.
- Aplicar criterios de calidad de datos según el contexto.
- Cargar datos transformados en distintos destinos.
- Implementar manejo de errores y logging en procesos ETL.
- Documentar y versionar el trabajo utilizando Git y GitHub.

---

## Contenidos del repositorio

### Día 1 – Extracción de datos

- Lectura de archivos CSV
- Extracción de datos desde APIs (simuladas)
- Conexión y extracción desde bases de datos SQLite
- Manejo de problemas reales de datos (codificación, delimitadores)
- Generación de evidencia de extracción en archivo Excel

**Archivos principales:**
- `ETL_Dia1_Extraccion_Multiples_Fuentes.ipynb`
- `clientes.csv`
- `evidencia_extraccion_dia1.xlsx`

---

### Día 2 – Transformaciones básicas y calidad de datos

- Identificación de problemas de calidad de datos
- Limpieza de datos (valores faltantes, duplicados, formatos inválidos)
- Imputación de valores según reglas de negocio
- Normalización de datos
- Validación de reglas básicas de consistencia
- Análisis del impacto de eliminar vs imputar datos

**Conceptos clave trabajados:**
- Sesgo introducido por limpieza estricta
- Importancia del contexto en decisiones de ETL
- Preparación de datos para etapas posteriores del pipeline

**Archivos principales:**
- `ETL_Dia2_Transformaciones_Basicas.ipynb`
- `evidencia_limpieza_validacion_dia2.xlsx`

---

## Días restantes

- Día 3 – Transformaciones avanzadas y enriquecimiento
- Día 4 – Carga de datos y estrategias de destino
- Día 5 – Manejo de errores y logging en ETL

---

## Tecnologías utilizadas

- Python
- Pandas
- NumPy
- SQL
- SQLite
- Jupyter Notebook
- Git y GitHub

---

## Estructura del repositorio

```

ETL-Python-SQL/
├── README.md
├── .gitignore
├── ETL_Dia1_Extraccion_Multiples_Fuentes.ipynb
├── clientes.csv
├── evidencia_extraccion_dia1.xlsx
├── ETL_Dia2_Transformaciones_Basicas.ipynb
├── evidencia_limpieza_validacion_dia2.xlsx

```





