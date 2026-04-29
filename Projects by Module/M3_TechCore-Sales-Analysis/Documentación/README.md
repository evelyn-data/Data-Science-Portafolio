# Proyecto Integrador – Análisis de Ventas TechCore

**Análisis de Ventas y Dashboard Interactivo**

**Información del Proyecto**

Cliente: TechCore

Consultor: DataVision Analytics 

Analista: Evelyn Berenice Hernández Ramírez

Periodo de análisis: 2014 - 2025


## 1. Descripción general del proyecto

Este proyecto forma parte de un proceso de selección para el rol de Analista de Datos Junior, en el cual se desarrolla un flujo completo de preparación, modelado y visualización de datos para TechCore, una cadena de tiendas minoristas especializada en la venta de computadores y accesorios tecnológicos.

El objetivo es transformar una base de datos cruda de facturación en un modelo relacional limpio, consistente y listo para análisis, finalizando con un dashboard interactivo en Power BI.

El proyecto se divide en tres fases principales:

- Limpieza y transformación de datos
- Diseño e implementación del modelo relacional
- Visualización y análisis en Power BI

## 2. Tech Stack

- Power Query (M): transformación y limpieza de datos.
- Power BI Desktop: visualización, modelado y DAX.
- Python: pandas, numpy y jupyter notebook.
- Excel


## 3. Estructura del proyecto

ProyectoM3_EvelynHernandezRamirez/
- Avances/
    - Avance_1/
        - Avance_1_Limpieza_Transformacion.pbix
        - ventas.csv
        - VentasTransformed.csv
    - Avance_2/
        - Avance_2_Modelo_Relacional.ipynb
        - ModeloVentas.xlsx
    - Avance_3/
        - Avance_3_Dashboard_Interactivo.pbix
- Documentación/
    - README.pdf
    - Conclusiones_Recomendaciones.pdf




## 4. Avance 1 - Limpieza y Transformación de Datos

**Objetivo**

Importar, limpiar y estandarizar la base de datos cruda de facturación utilizando Power BI (Power Query), asegurando consistencia, calidad y preparación para análisis posteriores.

**Herramientas utilizadas**

- Power BI Desktop
- Power Query Editor

**Actividades realizadas**

- **Importación de datos.** Importación del dataset original (ventas.csv) de facturación en Power BI Desktop.

- **Estandarización de nombres de columnas.** Renombrado de columnas por una nomenclatura uniforme y descriptiva (ej. Prod_Name → ProductoNombre).

- **Conversión correcta de tipos de datos:**

    - Fechas → Date
    - Precios → Decimal Number
    - Identificadores → Text

- **Detección y eliminación de registros duplicados.**

- **Tratamiento de valores nulos:**

    - Campos categóricos → "No especificado"
    - Campos numéricos → 0 (cuando es pertinente)

- **Normalización de categorías y campos textuales:**

    - "elec-trónica" / "Electronica" → Electrónica
    - "medellin" / "Medellín" → Medellín

- **Creación de columnas derivadas (Año y Mes a partir de la fecha de venta).**

**Resultados**

- Archivo PowerBI reutilizable con cada paso registrado.
- Dataset limpio exportado como VentasTransformed.csv

**Entregables**
- Avance_1_Limpieza_Transformacion.pbix
- VentasTransformed.csv






## 5. Avance 2 – Modelo Relacional

**Objetivo** 

Diseñar e implementar un modelo relacional normalizado que permita integrar ventas con productos, clientes, sucursales y vendedores, garantizando integridad referencial y trazabilidad de los datos.

**Actividades realizadas**

- Carga del dataset limpio (ventasTransformed.csv) en Python.
- Identificación de entidades y relaciones del negocio.
- Definición de claves primarias y foráneas.
- Construcción de las siguientes tablas:

**Facturas**
*Cada factura representa una venta completa*

- FacturaID (PK)
- Fecha
- ClienteID (FK)
- VendedorID (FK)
- SucursalID (FK)
- MetodoPagoID (FK)

**DetalleFacturas** 
*DetalleFacturas representa el detalle por producto dentro de una venta*

- DetalleID (PK)
- FacturaID (FK)
- ProductoID (FK)
- Cantidad
- Descuento
- Subtotal

**Productos**

- ProductoID (PK)
- NombreProducto
- MarcaProducto
- Precio

**Clientes**

- ClienteID (PK)
- Nombre
- Género
- Edad
- Teléfono
- Email
- Dirección

**Sucursales**

- SucursalID (PK)
- NombreSucursal
- CiudadID (FK)

**Ciudades**

- CiudadID (PK)
- NombreCiudad

**Vendedores**

- VendedorID (PK)
- NombreVendedor

**Métodos de Pago**

- MetodoPagoID (PK)
- MetodoPago

### 5.1. Relaciones del modelo (Power BI)

- Facturas (1) → DetalleFacturas (*)
- Productos (1) → DetalleFacturas (*)
- Clientes (1) → Facturas (*)
- Vendedores (1) → Facturas (*)
- Sucursales (1) → Facturas (*)
- Ciudades (1) → Sucursales (*)
- Métodos de Pago (1) → Facturas (*)

Todas las relaciones son uno a muchos (1:*), activas y con integridad referencial validada.



### 5.2 Análisis exploratorio en Python

Para validar el modelo se realizaron análisis rápidos, entre ellos:

- Total de ventas por marca.
- Top 10 productos más vendidos.
- Verificación de distribución de ventas por sucursal y ciudad.


**Resultados**

- Notebook python
- Archivo de Excel con las tablas creadas listo para cargar a PowerBI con modelo relacional implementado y validado.


**Entregables**

- Avance_2_Modelo_Relacional.ipynb
- modeloVentas.xlsx



## 6. Avance 3 – Visualización en Power BI

**Objetivo**

Construir un dashboard interactivo que permita analizar el desempeño de ventas desde distintas dimensiones del negocio.

**Herramientas utilizadas**

- Power BI Desktop
- DAX (Data Analysis Expressions)

**Actividades realizadas**

- Importación del archivo modeloVentas.xlsx en Power BI.
- Configuración del modelo relacional.
- Creación de medidas en DAX (almacenadas en una tabla dedicada de medidas).
- Implementación de filtros interactivos.

**KPIs y medidas implementadas**

- Ventas Totales: importe total de las ventas, considera el subtotal de cada producto vendido en todas las facturas. 
- Productos Vendidos: Total de productos vendidos. Considera la cantidad de productos vendidos en cada línea de factura.
- Ticket Promedio: Calcula el valor promedio por factura.
- Ventas Globales: Devuelve el total global de ventas, ignorando cualquier filtro aplicado por ciudad o producto. Se utiliza como referencia para comparar resultados parciales contra el total general del negocio.
-  Porcentaje de Participación por Ciudad: Calcula el porcentaje de participación de cada ciudad sobre el total de ventas considerando el contexto de filtros activos.

Nota: Las métricas de ventas se calcularon a partir de la tabla DetalleFacturas, ya que representa el nivel más granular del modelo. Esto garantiza consistencia en los análisis por producto, marca y ciudad, y evita duplicidades al aplicar filtros en el dashboard.



## 7. Reproducibilidad

Este proyecto fue desarrollado siguiendo un flujo reproducible de análisis de datos.  
Para replicar el proceso completo, se deben ejecutar las etapas en el siguiente orden:

1. Abrir el archivo `Avance_1_Limpieza_Transformacion.pbix` y ejecutar las transformaciones en Power Query.
2. Exportar el dataset limpio como `VentasTransformed.csv`. Este archivo es un dataset desnormalizado (tabla plana).
3. Ejecutar el notebook `Avance_2_Modelo_Relacional.ipynb` para generar las tablas del modelo relacional.
4. El notebook genera el archivo `modeloVentas.xlsx`, el cual es importado en Power BI.
5. Abrir el archivo `Avance_3_Dashboard_Interactivo.pbix` para visualizar el dashboard final.

Las transformaciones, relaciones y medidas fueron documentadas para garantizar la consistencia de los resultados.

## 8. Requisitos técnicos
- Power BI Desktop
- Python 3.9+
- pandas
- numpy





*Este proyecto fue desarrollado con fines académicos y de evaluación técnica para DataVision Analytics.*