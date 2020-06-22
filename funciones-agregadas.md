# FUNCIONES AGREGADAS
Son funciones que especifican un determinado valor sobre las columnas de una tabla; solo contamos con cinco funciones agregadas en SQL. Las cuales son: *suma*, *maximo*, *minimo*, *promedio*, *conteo*.

## COUNT
Perminte devolver total de registros o filas encontradas en una tabla dependiendo de una determinado condicion.
#### Formato:
```sql
SELECT COUNT( CAMPO ) 
    FROM TABLA
        WHERE <CONDICION>
```
##### Ejemplos:
+ Contar el total de registros de la tabla PRODUCTO
```sql
SELECT COUNT(COD_PRO) AS [TOTAL DE PRODUCTOS]
    FROM PRODUCTO
GO
```
+ Ahora usando el operador (*); este representa a cualquier columna de la tabla.
```sql
SELECT COUNT(*) AS [TOTAL DE PRODUCTOS]
    FROM PRODUCTO
GO
```
+ Contar el total de registros cuyo clientes sea del año 2012
```sql
SELECT COUNT(*) AS [TOTAL DE CLIENTES EN EL 2012]
    FROM CLIENTE C 
        WHERE YEAR(C.FEC_REG) = 2012
GO
```

## SUM
Permite devolver el acumulado de una columna de tipo numerico bajo una determinado criterio.
#### Formato:
```sql
SELECT SUM(<CAMPO>) 
    FROM <TABLA>
        WHERE <CONDICION>
```
##### Ejemplos:
+ Mostrar el total acumulado de los precios de los productos
```sql
SELECT SUM(P.PRE_PRO) AS [PRECIO ACULUMLADO]
    FROM PRODUCTO P
GO
```
+ Mostrar el monto acumulado del stock actual solo de aquellos productos importados.
```sql
SELECT SUM(P.SAC_PRO) AS [STOCK ACUMULADO]
    FROM PRODUCTO P
        WHERE IMP_PRO = 'V'
GO
```
+ Mostrar el monto acumulado de producto entre el precio y la cantidad registrada en el detalle de la factura.
```sql
SELECT SUM(D.CAN_VEN * D.PRE_VEN) AS [SUBTOTAL ACUMULADO]
    FROM DETALLE_FACTURA D
GO
```

## MAX
Permite devolver el maximo valor de un campo numerico encontrado en un campo numerico encontrado en una tabla dependiendo de una determinada condicion.
#### Formato:
```sql
SELECT MAX (CAMPO) 
    FROM <TABLA>
        WHERE <CONDICION>
```
##### Ejemplos: 
+ Mostrar el producto mas caro que registrado en la tienda
```sql
SELECT MAX(P.PRE_PRO) AS [PRECIO MAXIMO]
    FROM PRODUCTO P
GO
```
+ Mostrar el producto mas caro que registra la tienda con respecto a los productos importados
```sql
SELECT MAX(P.PRE_PRO) AS [PRECIO MAXIMO]
    FROM PRODUCTO P
        WHERE IMP_PRO = 'V'
GO
```

## MIN
Permite devolver el valor minimo de un campo numerico encontrado en una tabla dependiendo de un determinado condicion.
#### Formato:
```sql
SELECT MIN( CAMPO ) 
    FROM <NOMBRE_TABLA>
        WHERE <CONDICION>
```
##### Ejemplo:
+ Mostrar el producto con el precio mas bajo que registre la tienda.
```sql
SELECT MIN(P.PRE_PRO) AS [PRECIO MINIMO]
    FROM PRODUCTO P
GO
```
+ Mostrar el precio mas bajo que registra la tienda con respecto a los productos no importados.
```sql
SELECT MIN(P.PRE_PRO) AS [PRECIO MINIMO]
    FROM PRODUCTO P
        WHERE IMP_PRO = 'F'
GO
```
## AVG
Permite devolver el **promedio** de una columna de tipo numerico bajo un determinado criterio.
#### Formato:
```sql
SELECT AVG( CAMPO ) 
    FROM <NOMBRE_TABLA>
        WHERE <CONDICION>
```
##### Ejemplos:
+ Mostrar el promedio de precios de los productos
```sql
SELECT AVG(P.PRE_PRO) AS [PROMEDIO PRECIO]
    FROM PRODUCTO P
GO
```
+ Mostrar el promedio de stock actual solo de aquellos productos importados.
```sql
SELECT AVG(P.PRE_PRO) AS [PRECIO PROMEDIO]
    FROM PRODUCTO P
        WHERE P.IMPO_PRO = 'V'
GO
```
