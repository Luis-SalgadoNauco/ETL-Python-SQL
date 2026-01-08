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

**Verificación:**  
¿Qué consideraciones de seguridad debes tener al conectar con bases de datos y APIs?  
¿Cómo manejarías errores de conexión o respuestas inválidas?

**Respuesta:**

Al conectar con bases de datos y APIs es fundamental considerar:

- No incluir credenciales directamente en el código fuente.
- Usar variables de entorno o archivos de configuración excluidos del repositorio.
- Aplicar el principio de menor privilegio en usuarios de bases de datos.
- Preferir conexiones seguras (HTTPS, SSL/TLS).

Para el manejo de errores:
- Utilizar bloques `try/except` para capturar errores de conexión.
- Validar códigos de respuesta y estructura de datos de APIs.
- Registrar errores mediante logging.
- Evitar que un fallo detenga todo el proceso ETL.

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

**Verificación:**  
¿Cuándo deberías eliminar datos faltantes vs imputarlos?  
¿Qué tipos de validaciones son más importantes para diferentes tipos de datos?

**Respuesta:**

La decisión depende del contexto del análisis y del impacto en la calidad de los datos:

- **Eliminar datos faltantes** cuando:
  - El dato es crítico y no puede inferirse.
  - La cantidad de registros afectados es baja.
  - Mantenerlos introduce sesgos importantes.

- **Imputar datos faltantes** cuando:
  - El volumen de datos incompletos es alto.
  - Existen reglas claras de negocio.
  - Se requiere conservar la mayor cantidad de información posible.

Validaciones más relevantes:
- Numéricos: rangos válidos y valores positivos.
- Categóricos: dominios permitidos y normalización.
- Fechas: formatos correctos y coherencia temporal.
- Identificadores: unicidad y ausencia de duplicados.

---

### Día 3 – Transformaciones avanzadas y enriquecimiento

- Uniones de datos entre múltiples tablas (joins)
- Enriquecimiento de datasets con información relacionada
- Agregaciones y cálculos derivados por entidad
- Generación de métricas analíticas por cliente
- Validación de integridad referencial
- Validación de reglas de negocio
- Preparación de datos para análisis y carga posterior

**Archivos principales:**
- `ETL_Dia3_Transformaciones_Avanzadas.ipynb`
- `evidencia_transformaciones_avanzadas_dia3.xlsx`

**Verificación:**  
¿Qué tipo de join usarías cuando quieras mantener todos los registros de una tabla principal?  
¿Cómo decides qué métricas calcular para un análisis específico?

**Respuesta:**

Para mantener todos los registros de una tabla principal se utiliza un **LEFT JOIN**, ya que permite conservar todas las filas de la tabla principal y agregar información de la tabla relacionada solo cuando existe coincidencia.

La selección de métricas depende del objetivo del análisis y del contexto del negocio. Para decidir qué métricas calcular se consideran:
- Las preguntas que se desea responder con los datos.
- Las decisiones de negocio que se deben apoyar.
- Las reglas del dominio.
- La calidad y disponibilidad de la información.

Las métricas deben ser relevantes, coherentes y útiles para etapas posteriores del proceso ETL.

---

### Día 4 – Carga de datos y estrategias de destino

- Implementación de distintas estrategias de carga de datos
- Carga completa (Full Load) en base de datos SQLite
- Carga incremental basada en identificadores
- Comparación de rendimiento entre estrategias de carga
- Generación de evidencia en archivo Excel
- Evaluación de eficiencia según volumen y frecuencia de datos

**Archivos principales:**
- `ETL_Dia4_Carga_Datos.ipynb`
- `evidencia_carga_dia4.xlsx`

**Verificación:**  
¿En qué situaciones usarías carga completa vs incremental?  
¿Qué factores influyen en el tamaño óptimo de lote para carga de datos?

**Respuesta:**

- **Carga completa (Full Load)** se utiliza cuando:
  - El volumen de datos es pequeño o manejable.
  - Los datos cambian completamente entre ejecuciones.
  - Se requiere asegurar consistencia total del dataset.
  - El costo de recargar todo es bajo.

- **Carga incremental** se utiliza cuando:
  - Existen grandes volúmenes de datos.
  - Los cambios son frecuentes pero parciales.
  - Se necesita optimizar tiempos y recursos.
  - Se dispone de campos como `id`, `timestamp` o `updated_at`.

Factores que influyen en el tamaño óptimo de lote:
- Capacidad de la base de datos de destino.
- Memoria disponible.
- Latencia de red.
- Presencia de índices y restricciones.
- Requerimientos de atomicidad y rollback.

La elección correcta de estrategia y tamaño de lote impacta directamente en el rendimiento, la confiabilidad y la escalabilidad del proceso ETL.

---

## Días restantes

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
├── ETL_Dia3_Transformaciones_Avanzadas.ipynb
├── evidencia_transformaciones_avanzadas_dia3.xlsx
├── ETL_Dia4_Carga_Datos.ipynb
├── evidencia_carga_dia4.xlsx

```





