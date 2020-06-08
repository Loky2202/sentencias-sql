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