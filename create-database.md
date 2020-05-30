# Crear una base de dato

## Validando una base de datos

Primero Evaluamos si existe la DB
Si existe la borra y luego la crea sino crea una nueva

```sql
IF DB_ID('BASEDEDATOS')IS NOT NULL
    DROP DATABASE BASEDEDATOS
GO

CREATE DATABASE BASEDEDATOS
GO
```

## Mostrar todas las tablas de la base de datos
Sentencia para ver las tablas que contiene la base de datos

```sql
SELECT * FROM SYS.sysdatabases s
    WHERE s.name = 'VENTAS'
GO
```

## Muestra los archivos que componen la base de datos

```sql
SP_HELPDB BASEDEDATOS
GO
```

