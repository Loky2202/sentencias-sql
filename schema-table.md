# MANEJO DE ESQUEMAS 
Es un contenedor que puede contener tablas, vistas o procedimientos almacenados dentro de la misma
BD 

## Creando un Esquema

```sql
CREATE SCHEMA <NOMBRE_SCHEMA> AUTHORIZATION DBO
GO 
```

# Usando Esquema

## Creando una Tabla con Esquema

```sql
CREATE TABLE <NOMBRE_SCHEMA>.<NOMBRE_TABLA> (
    CAMPO_1 TIPO NOT NULL,
    CAMPO_2 TIPO NOT NULL | NULL,
    CAMPO_N TIPO NOT NULL | NULL,
    PRIMARY KEY(<CAMPO_1>, <CAMPO_N>)
)
GO
```


Implementacion de la BD "Empresa" con el uso de Esquema como ejemplo:

# Esquema
Observamos que esto es para organizar las tablas de la Base de Datos
* Compras
    * Productos
    * Proveedor
    * Orden de Compra
    * Detalle de Orden de Compra
* Ventas
    * Cliente
    * Factura
    * Detallae de Factura
* RRHH
    * Vendedor
    * Distrito
