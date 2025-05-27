# 📊 Planificación de Cubo OLAP con Arquitectura Medallion

Este documento contiene la planificación detallada para diseñar un cubo OLAP de ventas utilizando la arquitectura **Medallion** (Bronze, Silver, Gold). Incluye tareas por épica, herramientas recomendadas por etapa y plantillas de seguimiento.

---

## 📅 Épicas (Epics) y Tareas (Tasks)

### Epic 1: Recolección de Requisitos y Análisis del Negocio

- Entrevistas con stakeholders clave
- Definir métricas clave (KPIs)
- Definir dimensiones necesarias
- Definir granularidad del cubo
- Revisión de reportes actuales

### Epic 2: Diseño de la Arquitectura Medallion

- Seleccionar tecnologías y plataformas
- Diseñar capas Bronze, Silver, Gold
- Definir esquemas para cada capa
- Establecer estrategias de almacenamiento
- Definir estándares de transformación

### Epic 3: Ingesta y Almacenamiento en la Capa Bronze

- Conectar a fuentes de datos
- Diseñar pipelines de ingestión
- Registrar metadata y esquema
- Almacenar en formato Delta

### Epic 4: Procesamiento y Transformación en la Capa Silver

- Aplicar limpieza de datos
- Validar integridad referencial
- Unir datasets relevantes
- Crear columnas derivadas
- Corregir registros anómalos
- Crear vistas intermedias

### Epic 5: Modelado Semántico y Capa Gold

- Modelar tabla de hechos
- Modelar dimensiones
- Calcular KPIs complejos
- Validar resultados
- Optimización de queries

### Epic 6: Construcción del Cubo OLAP

- Seleccionar herramienta OLAP
- Crear modelo de cubo
- Definir jerarquías y agregaciones
- Habilitar funcionalidades de análisis
- Implementar seguridad y roles
- Pruebas con usuarios

### Epic 7: Orquestación, Automatización y Calidad

- Diseñar DAGs en Airflow o DBT
- Pruebas de calidad de datos
- Configurar monitoreo y alertas
- Auditoría y trazabilidad
- Documentar pipelines

### Epic 8: Capacitación, Documentación y Entrega

- Documentar modelo de datos
- Crear guía para analistas
- Capacitación a usuarios finales
- Entrega a producción y soporte
- Backlog de mejoras

---

## ✅ Plantilla de Seguimiento por Épica

### Ejemplo – Epic 1: Recolección de Requisitos

| Task                                  | Responsable | Estado     | Prioridad | Inicio      | Fin         | Notas                                  |
|---------------------------------------|-------------|------------|-----------|-------------|-------------|----------------------------------------|
| Entrevistas con stakeholders          | Ana Gómez   | En curso   | Alta      | 27/05/2025  | 30/05/2025  | Reunión con ventas el 28/05            |
| Definir métricas clave (KPIs)         | Pedro Ruiz  | Pendiente  | Alta      |             |             | Depende de entrevistas                 |
| Definir dimensiones necesarias        | Ana Gómez   | Pendiente  | Media     |             |             | Incluir ubicación, canal, producto     |
| Definir granularidad del cubo         | Laura Pérez | Pendiente  | Media     |             |             | Detalle diario vs mensual              |
| Revisión de reportes actuales         | Pedro Ruiz  | Pendiente  | Baja      |             |             | Reportes en Excel                      |

---

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

## 📁 Archivos Generados

- `Plan_Cubo_OLAP_Medallion.xlsx`: Planificación detallada por épica y tarea
- `Seguimiento_Cubo_OLAP_Medallion.xlsx`: Una hoja de seguimiento por épica
- `Herramientas_Por_Etapa.xlsx`: Tabla con herramientas recomendadas por etapa (opcional)

---

## 🧩 Recomendaciones

- Usa [DBT](https://www.getdbt.com/) para modelar la capa Gold como código
- Automatiza con [Apache Airflow](https://airflow.apache.org/) o [Prefect](https://www.prefect.io/)
- Usa [Great Expectations](https://greatexpectations.io/) para pruebas de calidad de datos
- Adopta [Power BI](https://powerbi.microsoft.com/) o [Looker](https://looker.com/) para OLAP moderno

---

## 🚀 Licencia

Este proyecto está bajo una licencia abierta para uso interno y educativo.
