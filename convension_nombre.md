# **Convenciones de nombres**

Este documento describe las convenciones de nombres utilizadas para los esquemas, tablas, vistas, columnas y otros objetos para el Data Warehouse.

## **Contenido**

1. [Principios generales](#general-principles)
2. [Convenciones para nombrar las tablas](#table-naming-conventions)
   - [Bronze Rules](#bronze-rules)
   - [Silver Rules](#silver-rules)
   - [Gold Rules](#gold-rules)
3. [Convenciones para nombrar columnas](#column-naming-conventions)
   - [Surrogate Keys](#surrogate-keys)
   - [Columnas técnicas](#technical-columns)
4. [Stored Procedure](#stored-procedure-naming-conventions)
---

## **Principios generales**

- **Convenciones de nombres**: Utiliza snake_case, con minúsculas y guiones bajos (`_`) para separar palabras.
- **Idiona**: Utilice el inglés para todos los nombres.
- **Evitar palabras reservadas**: No utilice palabras reservadas de SQL como nombres de objetos.

## **Convecion de nombre en tablas**

### **Bronze Rules**
- Todos los nombres deben empezar por el nombre del sistema fuente, y los nombres de las tablas deben coincidir con sus nombres originales sin renombrar.
- **`<sourcesystem>_<entity>`**  
  - `<sourcesystem>`: Nombre del sistema fuente (Ejemplo, `crm`, `erp`).  
  - `<entity>`: Nombre exacto de la tabla del sistema fuente.  
  - Ejemplo: `erp_customer_info` → Información del cliente del sistema ERP.

### **Silver Rules**
- Todos los nombres deben empezar por el nombre del sistema fuente, y los nombres de las tablas deben coincidir con sus nombres originales sin renombrar.
- **`<sourcesystem>_<entity>`**  
  - `<sourcesystem>`: Nombre del sistema fuente (Ejemplo, `crm`, `erp`).  
  - `<entity>`: Nombre exacto de la tabla del sistema fuente.  
  - Ejemplo: `erp_customer_info` → Información del cliente del sistema ERP.

### **Gold Rules**
- Todos los nombres deben usar nombres significativos y alineados con el negocio para las tablas, comenzando con el prefijo de categoría.
- **`<category>_<entity>`**  
  - `<category>`: Describe la función de la tabla, como `dim` (dimension) or `fact` (fact table).  
  - `<entity>`: Nombre descriptivo de la tabla, alineado con el dominio de negocio (ejemplo, `customers`, `products`, `sales`).  
  - Ejemplos:
    - `dim_customers` → Tabla de dimensiones para datos de clientes.
    - `fact_sales` → Tabla de hechos que contiene transacciones de ventas.

#### **Glosario de patrones de categorías**

| Patrón      | Significado                           | Ejemplo(s)                              |
|-------------|-----------------------------------|-----------------------------------------|
| `dim_`      | Dimension table                  | `dim_customer`, `dim_product`           |
| `fact_`     | Fact table                       | `fact_sales`                            |
| `agg_`      | Aggregated table                 | `agg_customers`, `agg_sales_monthly`    |

## **Convenciones para nombrar columnas**

### **Surrogate Keys**  
- Todas las claves primarias de las tablas de dimensiones deben utilizar el sufijo `_key`.
- **`<table_name>_key`**  
  - `<table_name>`: Hace referencia al nombre de la tabla o entidad a la que pertenece la clave.
  - `_key`: Un sufijo que indica que esta columna es una clave sustituta.
  - Ejemplo: `customer_key` → Surrogate key en la tabla `dim_customers`.
  
### **Columnas técnicas**
- Todas las columnas técnicas deben comenzar con el prefijo `dwh_`, seguido de un nombre descriptivo que indique la finalidad de la columna.
- **`dwh_<column_name>`**  
  - `dwh`: Prefijo exclusivo para metadatos generados por el sistema.
  - `<column_name>`: Nombre descriptivo que indica la finalidad de la columna.
  - Ejemplo: `dwh_load_date` → Columna generada por el sistema utilizada para almacenar la fecha en la que se cargó el registro.
 
## **Stored Procedure**

- Todos los procedimientos almacenados utilizados para cargar datos deben seguir el patrón de nomenclatura:
- **`load_<layer>`**.
  
  - `<layer>`: Representa la capa que se está cargando, such as `bronze`, `silver`, o `gold`.
  - Ejemplo: 
    - `load_bronze` → Procedimiento almacenado para cargar datos en la Bronze layer.
    - `load_silver` → Procedimiento almacenado para cargar datos en la Silver layer.
