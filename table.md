# Creacion de tablas

## Sentencia para Crear Tablas

```sql
CREATE TABLE <NOMBRETBLA> (
    CAMPO1 TIPO,
    CAMPO2 TIPO,
    CAMPO_N TIPO
)
GO
```


## Validar Tablas
Creacion de una tabla validando su existencia primero

```sql
IF OBJECT_ID('<TABLA>') IS NOT NULL
    DROP TABLE <TABLA>
GO
```

## Mostrar todas la Tablas en DB

```sql
SP_TABLES 
GO
```

## Visualizar columna por tabla

```sql
SP_COLUMNS <TABLA>
GO
```

## Modificar una Tabla
Estructura para agregar, modificar o eliminar campos de una tabla

**Agregar Columna**
```sql 
ALTER TABLE <NOMBRE_TABLA> (
    ADD <COLUMNA TIPO>,
        <COLUMNA TIPO>
)
GO
```

**Modificar Columna**
```sql
ALTER TABLE <NOMBRE_TABLA>(
    ALTER COLUMN <COLUMNA TIPO>
)
GO
```

**Eliminar Columna**
```sql
ALTER TABLE <NOMBRE_TABLE> (
    DROP COLUMN <COLUMNA>
)
GO
```

*Comprobando modificaciones*
```sql
SP_COLUMNS <TABLA>
```

## Eliminando una Tabla
```sql
DROP TABLE <TABLA>
GO
```