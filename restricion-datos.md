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
Crea un campo que solo acepta valor entre 1 y 100
```sql
PRE_PRO MONEY NOT NULL CHECK (PRE_PRO BETWEEN 1 AND 100)
```

Crea un campo que solo acepte valores mayores a 0
```sql
SAC_PRO INT NOT NULL CHECK ( SAC_PRO > 0 )
```

Crea un campo que solo acepte: 'BOLSA' o 'CAJA'
```sql
UNI_PRO VARCHAR(30) NOT NULL CHECK ( UNI_PRO IN ( 'BOLSA', 'CAJA' ) )
```

**modificando una tabla**
    
Al campo SAC_PRO le asignamos una regla
```sql
ALTER TABLE PRODUCTO ADD CONSTRAINT CHK_STOCK_ACTUAL CHECK ( SAC_PRO > 0 )
```
## Uso de UNIQUE
Permite o pone la regla que en toda la tabla solo se permite un valor unico 

**creando un campo en una tabla**
```sql
<NOMBRE_CAMPO> <TIPO> NULL | NOT NULL UNIQUE
```
**modificando un campo**
```sql
ALTER TABLE <NOMBRE_TABLA> ADD CONSTRAINT 'NOMBRE_RESTRICION' UNIQUE <CAMPO>
```

##### Ejemplos: 

Creando una un campo TELEFONO donde su valor sea unico
```sql
CREATE TABLE PROVEEDOR (
    TEL_PRV CHAR(15) NULL UNIQUE
)
GO
```
Modificando la el campo TEL_PRV de la tabla PROVEEDOR donde su valor sera unico
```sql
ALTER TABLE PROVEEDOR
    ADD CONSTRAINT UNI_TELEFONO UNIQUE(TEL_PRV)
GO
```


## Visualizar las Restricciones 
Muestra en forma de consulta las restriciones de la base de datos asi como las creadas.
```sql
SELECT * FROM INFORMATION_SCHEMA.TABLE_CONSTRAINTS 
    WHERE TABLE_NAME = '<NOMBRE_TABLA>'
GO
```