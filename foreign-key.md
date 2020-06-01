# FOREIGN KEY
Permite la asociacion de una tabla a otra.

## Restriccion de Llave Secundaria o Foranea

**Creando una tabla**
```sql
CREATE TABLE <NOMBRE_TABLA> (
    CAMPO_1 TIPO NULL | NOT NULL,
    CAMPO_2 TIPO NOT NULL REFERENCES <NOMBRE_TABLA_A_RELACIONAR>,
    CAMPO_N TIPO NULL | NOT NULL 
)
GO
```

**Modificando Tabla**
```sql
ALTER TABLE <NOMBRE_TABLA>
    ADD FOREIGN KEY (<CAMPO_REFERENCIA>) REFERENCES (<NOMBRE_TABLA_A_RELACIONAR>)
GO
```