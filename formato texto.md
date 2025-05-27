# 📊 Planificación de Cubo OLAP de Ventas

Este documento contiene la planificación detallada para diseñar un cubo OLAP de ventas utilizando la arquitectura **Medallion** (Bronze, Silver, Gold). Incluye tareas por épica, herramientas recomendadas por etapa y plantillas de seguimiento.

### 🔷 Epic 1: Recolección de Requisitos y Análisis del Negocio
Objetivo: Alinear los objetivos del cubo OLAP con las necesidades del negocio y definir qué datos deben ser modelados.
##### Tasks:
###### 1. Entrevistas con stakeholders clave (ventas, marketing, finanzas):
- Recoger objetivos analíticos y casos de uso.
- Identificar reportes actuales y limitaciones.

###### 2. Definir métricas clave (KPIs):
- Ingresos brutos/netos, unidades vendidas, ticket promedio, márgenes, % de conversión.

###### 3. Definir dimensiones necesarias:
- Producto (categoría, marca), Cliente (segmento, canal), Tiempo (día, semana, mes), Vendedor, Canal de ventas, Ubicación geográfica.

###### 4. Definir granularidad del cubo:
- Nivel de transacción por cliente y producto por día.
- Considerar si se necesitan acumulados mensuales o anuales.

###### 5. Revisión de reportes actuales:
- Identificar qué reportes se podrán migrar al cubo OLAP.


### 🔶 Epic 2: Diseño de la Arquitectura Medallion
Objetivo: Estructurar cómo se organizarán y evolucionarán los datos desde su ingesta hasta el modelo analítico.
##### Tasks:
###### 1. Seleccionar tecnologías y plataformas:
- Data Lakehouse (Databricks, Azure Synapse, Snowflake), Delta Lake para versionado.
- Orquestador (Airflow, DBT).

###### 2. Diseñar capas Bronze, Silver, Gold:
- Bronze: Datos crudos, sin limpieza.
- Silver: Datos limpios y relacionados.
- Gold: Datos agregados y listos para consumo analítico.

###### 3. Definir esquemas para cada capa:
- Estructura de tablas, tipos de datos, particionado.

###### 4. Establecer estrategias de almacenamiento:
- Particionado por fecha o región para optimizar lectura.
- Uso de Delta Lake para versionado y ACID.

###### 5. Definir estándares de transformación:
- Formato de fechas, codificación de campos categóricos, manejo de nulos.

### 🔷 Epic 3: Ingesta y Almacenamiento en la Capa Bronze
Objetivo: Capturar los datos de múltiples fuentes y almacenarlos sin transformar.
##### Tasks:
###### 1. Conectar a fuentes de datos:
- Bases de datos relacionales (PostgreSQL, MySQL, Oracle).
- Archivos planos (CSV, Excel).
- APIs de servicios de ventas o e-commerce.

###### 2. Diseñar pipelines de ingestión:
- Ingestión diaria/incremental de datos de ventas.
- Gestión de errores, duplicados y reintentos.

###### 3. Registrar metadata y esquema:
- Crear catálogo de datos con descripciones de columnas y tipos de datos.

###### 4. Almacenamiento en formato Delta:
- Evitar sobreescritura accidental.
- Habilitar auditar cambios.

### 🔶 Epic 4: Procesamiento y Transformación en la Capa Silver
Objetivo: Estandarizar, limpiar y relacionar los datos para un análisis consistente.
##### Tasks:
###### 1. Aplicar limpieza de datos:
- Remover duplicados, valores inválidos o inconsistentes.
- Normalizar texto y campos categóricos.

###### 2. Validar integridad referencial:
- Relaciones entre ventas y clientes, productos, fechas.

###### 3. Unir datasets relevantes:
- Integrar transacciones de ventas con dimensiones auxiliares.

###### 4. Crear nuevas columnas derivadas:
- Total venta, descuento aplicado, impuestos, costo total.

###### 5. Detectar y corregir registros anómalos:
- Outliers en precios, ventas negativas, fechas inválidas.

###### 6. Crear vistas intermedias:
- Transacciones limpias y datos de referencia ya unificados.

### 🔷 Epic 5: Modelado Semántico y Capa Gold
Objetivo: Diseñar el modelo estrella o snowflake para habilitar análisis multidimensional.
##### Tasks:
###### 1. Modelar tabla de hechos:
- fact_sales con claves foráneas hacia dimensiones.

###### 2. Modelar dimensiones:
- dim_product, dim_customer, dim_date, dim_region, etc.
- Añadir jerarquías (producto → categoría → línea; día → mes → año).

###### 3. Calcular KPIs complejos:
- Ventas acumuladas, crecimiento YoY, % participación.

###### 4. Validar consistencia de resultados:
- Comparar con reportes oficiales del negocio.

###### 5. Optimización de queries:
- Indexación, uso de formatos columnar, particionado efectivo.

### 🔶 Epic 6: Construcción del Cubo OLAP
Objetivo: Permitir la exploración multidimensional con herramientas analíticas o motores OLAP.
##### Tasks:
###### 1. Seleccionar herramienta OLAP:
- Power BI, SSAS Tabular, Apache Druid, Clickhouse, Cube.js.

###### 2. Crear modelo de cubo:
- Cargar dimensiones, medidas, relaciones.

###### 3. Definir jerarquías y agregaciones:
- Por tiempo, ubicación, producto.

###### 4. Habilitar funcionalidades de análisis:
- Drill-down, filtros, comparaciones YoY.

###### 5. Implementar seguridad y roles:
- Accesos por región, rol, tipo de usuario.

###### 6. Pruebas con usuarios:
- Validar casos de uso reales.

### 🔷 Epic 7: Orquestación, Automatización y Calidad
Objetivo: Habilitar un flujo de datos automatizado, confiable y monitoreado.
##### Tasks:
###### 1. Diseñar DAGs en Airflow o DBT:
- Dependencias claras entre tareas (bronze → silver → gold → cubo).

###### 2. Crear pruebas de calidad de datos:
- DQ: % nulos, unicidad, integridad.

###### 3. Configurar monitoreo y alertas:
- Notificaciones si fallan jobs o métricas están fuera de rango.

###### 4. Auditoría y trazabilidad de datos:
- Uso de herramientas de data lineage (OpenMetadata, Unity Catalog).

###### 5. Documentar pipelines y scripts:
- Manual de despliegue y recuperación de fallos.

### 🔶 Epic 8: Capacitación, Documentación y Entrega
Objetivo: Asegurar que el cubo sea comprendido, mantenido y explotado correctamente.
##### Tasks:
###### 1. Documentar modelo de datos:
- Diccionario de datos, lógica de KPIs, relaciones.

###### 2. Crear guía de usuario para analistas:
- Cómo usar el cubo, qué filtros aplicar.

###### 3. Capacitación a usuarios finales:
- Sesiones prácticas, navegación por dimensiones.

###### 4. Entrega a producción y soporte post-lanzamiento:
- Plan de soporte, feedback inicial, ajustes menores.

###### 5. Backlog de mejoras:
- Nuevas métricas, nuevas fuentes, evolución del cubo.

## 🛠️ Herramientas Recomendadas por Etapa

| Etapa                                     | Tipo de Herramienta               | Herramientas Recomendadas                                  |
|------------------------------------------|----------------------------------|-------------------------------------------------------------|
| Recolección de Requisitos                | Documentación                    | Notion, Confluence, Google Docs                            |
|                                          | Diagramas                        | Miro, Figma, Lucidchart                                    |
|                                          | Formularios                      | Google Forms, Microsoft Forms                              |
|                                          | Toma de decisiones               | Trello, Jira, ClickUp                                      |
| Diseño de Arquitectura Medallion         | Modelado lógico                  | dbdiagram.io, Draw.io                                      |
|                                          | Infraestructura cloud            | Databricks, Snowflake, Azure Synapse                       |
|                                          | Infraestructura como código      | Terraform, Pulumi                                          |
| Ingesta de datos (Capa Bronze)           | ETL / Ingesta                    | Apache Nifi, Airbyte, Fivetran                             |
|                                          | Procesamiento                    | PySpark, Spark Streaming                                   |
|                                          | Almacenamiento                   | Delta Lake, S3, ADLS, GCS                                  |
| Transformación (Capa Silver)            | Transformaciones                 | DBT, PySpark, SQL                                          |
|                                          | Calidad de datos                 | Great Expectations, Soda.io                               |
| Capa Gold y Semántica                    | Modelado                         | DBT, BigQuery, Snowflake                                   |
|                                          | Visualización de datos           | Tableau, Power BI                                          |
| Construcción del Cubo OLAP              | Cubo OLAP                        | SSAS, Power BI, Tableau, Cube.js                           |
| Orquestación y QA                        | Orquestación de workflows        | Apache Airflow, Prefect, Dagster                          |
|                                          | Validación de datos              | Great Expectations, Datafold, Monte Carlo                 |
| Capacitación y Documentación            | Documentación técnica            | Notion, Confluence                                         |
|                                          | Capacitación                     | Loom, Zoom, Google Slides                                 |

---
