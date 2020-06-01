# RESTRICION DE DATOS O **CONSTRAINT**

## Uso de IDENTITY
Uso solo para campos tipo numericos; aunmentan su valor de forma automatica por cada registro dentro de la tabla

**agregar esto cuando creamos la tabla**
```sql
CAMPO_1 TIPO NOT NULL PRIMARY KEY IDENTITY(VALOR_1, VALOR_2)
```
*donde VALOR_1 es **Punto de Inicio***  
*VALOR_2 es **La Forma de Incremento***

## Uso de DEFAULT
Asignando un valor por defecto segun el tipo de dato; dicho valor debe de ser especificado antes de registrar valores en la tabla

**cuando creamos una tabla**
```sql
CAMPO TIPO NULL | NOT NULL DEFAULT <VALOR>
```

**modificando una tabla**
```sql
ALTER TABLE <NOMBRE_TABLA>
    ADD DEFAULT '<VALOR>' FOR <CAMPO>
GO
```

### Observar los **CONSTRAINT** de la tabla
```sql
SP_HELPCONTRAINT <NOMBRE_TABLA>
GO
```

## Uso de CHECK
Permite restringir el rango de valores que pueden estar permitidos ingresando en una o mas columna de una tabla.

**creando una tabla**
```sql
CAMPO TIPO NOT NULL | NULL CHECK (<CONDICION>)
```

**modificando una tabla**
```sql
ALTER TABLE <NOMBRE_TABLA>
    ADD CONSTRAINT <NOMBRE> CHECK (<CONDICION>)
```

##### Ejemplos: 
Al campo solo acepta valor entre 1 y 100
```sql
PRE_PRO MONEY NOT NULL CHECK (PRE_PRO BETWEEN 1 AND 100)
```



