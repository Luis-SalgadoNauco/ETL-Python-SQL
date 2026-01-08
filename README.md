# ETL-Python-SQL

Repositorio de prácticas y proyecto final del módulo **Herramientas ETL** del curso de Análisis de Datos.

Este repositorio documenta el trabajo realizado durante la **Semana de ETL con Python y SQL**, enfocado en el diseño e implementación de **pipelines ETL completos, robustos y reproducibles**, similares a los utilizados en entornos reales de análisis y datos.

A lo largo del repositorio se construye un flujo **end-to-end (Extract, Transform, Load)**, incorporando buenas prácticas de calidad de datos, validaciones, manejo de errores, logging y generación de evidencias.

---

## Descripción de la semana

Durante esta semana se desarrolla un flujo ETL completo de extremo a extremo, comenzando por la extracción de datos desde múltiples fuentes, continuando con procesos de transformación, limpieza y validación, y finalizando con la carga de datos y la implementación de manejo de errores y logging.

El trabajo se realiza de forma incremental, permitiendo comprender el rol de cada etapa dentro de un pipeline ETL, su impacto en la calidad de los datos, la confiabilidad del proceso y la trazabilidad necesaria para entornos productivos.

---

## Objetivos generales

- Comprender la arquitectura y el flujo de un pipeline ETL.
- Diseñar procesos ETL modulares utilizando Python.
- Extraer datos desde múltiples fuentes (archivos, bases de datos y APIs).
- Limpiar, transformar y validar datos utilizando Pandas.
- Aplicar criterios de calidad de datos según el contexto del negocio.
- Implementar estrategias de carga completa e incremental.
- Incorporar manejo de errores, validaciones y logging para aumentar la robustez del proceso.
- Generar evidencias de ejecución y resultados del ETL.
- Documentar y versionar el proyecto utilizando Git y GitHub.

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

### Día 5 – Manejo de errores y logging en procesos ETL

- Identificación de fallos comunes en pipelines ETL
- Manejo de errores por tipo (datos, conectividad, recursos, lógica)
- Implementación de reintentos y fallos controlados
- Uso del módulo `logging` para trazabilidad del proceso
- Registro de eventos por etapa del pipeline
- Medición de tiempos de ejecución
- Validaciones post-ETL
- Construcción de un pipeline ETL completo y robusto
- Simulación de errores reales en extracción y carga
- Generación de evidencia del proceso desde Jupyter

**Conceptos clave trabajados:**
- Diferencia entre errores críticos y no críticos
- Importancia del logging para monitoreo y depuración
- Fallar rápido vs continuar con errores parciales
- Observabilidad en procesos ETL
- Robustez y mantenibilidad de pipelines

**Archivos principales:**
- `ETL_Dia5_Pipeline_ETL_Manejo_Errores.ipynb`
- `etl_ecommerce.log`
- `evidencia_etl_dia5.xlsx`

**Verificación:**  
¿Qué información debería incluir un registro (log) para facilitar la depuración de un pipeline ETL?  
¿Cómo decides entre continuar el pipeline con errores parciales o detenerlo completamente?

**Respuesta:**

Un registro efectivo debe incluir:

- Timestamp del evento.
- Etapa del pipeline donde ocurre el evento.
- Tipo de evento (INFO, WARNING, ERROR).
- Cantidad de registros procesados.
- Tiempo de ejecución por etapa.
- Mensaje de error claro y específico.
- Contexto suficiente para reproducir el problema.

La decisión entre continuar o detener el pipeline depende del impacto del error:

- **Detener el pipeline** cuando:
  - Fallan conexiones a fuentes o destinos.
  - Los datos críticos están ausentes o corruptos.
  - Se rompe la integridad del proceso.
  - La carga es incompleta o inconsistente.

- **Continuar con errores parciales** cuando:
  - El error afecta a pocos registros.
  - Existen valores por defecto o reglas de imputación.
  - El impacto analítico es bajo.
  - El error puede corregirse en etapas posteriores.

Un pipeline bien diseñado prioriza la calidad, la trazabilidad y la confiabilidad por sobre la ejecución silenciosa.

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

## Conclusiones

Este proyecto permitió consolidar conocimientos clave sobre procesos ETL, abordando no solo la manipulación de datos, sino también aspectos fundamentales como la calidad, la trazabilidad, el manejo de errores y la robustez del pipeline.

El enfoque incremental facilitó la comprensión del impacto de cada etapa y sentó las bases para escalar estos procesos hacia entornos productivos más complejos.

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
├── ETL_Dia5_Pipeline_ETL_Manejo_Errores.ipynb
├── evidencia_etl_dia5.xlsx

```

