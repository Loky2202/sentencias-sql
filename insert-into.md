# INSERTAR DATOS 
Sentencias DML para datos

## INSERT INTO
Permite agregar una fila a una tabla o una vista de una determinada base de datos.

### Formato:

Sin especificar campos
```sql
INSERT INTO <NOMBRE_TABLA> VALUES (VALOR_1, VALOR_2, VALOR_3, VALOR_N)
GO
```

Especificando campos. No se consiederan las columnas que tiene la restriccion ```IDENTITY```
```sql
INSERT INTO <NOMBRE_TABLA> ( CAMPO_1, CAMPO_2, CAMPO_3 ) VALUES ( VALOR_1, VALOR_2, VALOR_3 )
GO
```

Insercion multiple
```sql
INSERT INTO <NOMBRE_TABLA> VALUES
    ( VALOR_1, VALOR_2, VALOR_3 ),
    ( VALOR_1, VALOR_2, VALOR_3 ),
    ( VALOR_1, VALOR_2, VALOR_3 )
GO
```
```sql
INSERT INTO <NOMBRE_TABLA> ( CAMPO_1, CAMPO_2, CAMPO_3 ) VALUES
    ( VALOR_1, VALOR_2, VALOR_3 ),
    ( VALOR_1, VALOR_2, VALOR_3 )
GO
```

## Llenado de una Tabla Externa
Guarda todo la consulta en la TABLA_DESTINO o los campos seleccionados.

```sql
INSERT INTO <NOMBRE_TABLA_DESTINO> 
    SELECT * FROM <NOMBRE_TABLA_ORIGEN>
```

