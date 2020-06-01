# PRIMARY KEY
Son las que Registren que una columna sea unica en tabla. Deben de ser **CHAR** ò **INT**
*Son para identificar una columna en la tabla*

## Restriccion de LLave Primary 
**Creando un tabla**

```sql
CREATE TABLE <NOMBRE_TABLA> (
    CAMPO_CLAVE TIPO NOT NULL PRIMARY KEY,
    CAMPO_2 TIPO NOT NULL | NULL
)
GO
```

**Atravez de un conjunto de campos**
```sql
CREATE TABLE <NOMBRE_TABLA> (
    CAMPO_1 TIPO NOT NULL,
    CAMPO_2 TIPO NOT NULL | NULL,
    CAMPO_3 TIPO NOT NULL | NULL,
    PRIMARY KEY (<CAMPO_1>, <CAMPO_2>)
)
GO
```

**Modificando una Tabla**
```sql
ALTER TABLE <NOMBRE_TABLA>
    ADD PRIMARY KEY (<CAMPO_CLAVE>)
GO
```

