# GROUP BY
Para recuperar informacion agrupada por algun criterio, se debe implementar la clausula **GROUP BY** dentro de la consulta **SELECT**. El **GROUP BY** agrupa un conjunto de registro de acuerdo a los valores de una o mas columnas de una tabla. Para una implementacion de las consultas agrupadas se puede usar las funciones agregadas como son: **MAX, MIN, SUM, AGV o COUNT**
#### Formato:
```sql
SELECT <ALL> <*> <ALIAS.CAMPO AS CAMPO>
    FROM <NOMBRE_TABLA> <AS TABLA>
        <GROUP BY CAMPO>
        <HAVING CONDICION>
```
##### Ejemplos:
+ Mostrar el total de clientes registrados por distritos.
```sql
SELECT D.NOM_DIS AS DISTRITO, COUNT(*) AS [TOTAL]
    FROM CLIENTE C
        JOIN DISTRITO D ON C.COD_DIS = D.COD_DIS
    GROUP BY D.NOM_DIS
GO
```
```
|  DISTRITO  | TOTAL |  
| bellavsita |   1   |  
|   callad   |   1   |  
|    lima    |   1   |  
```
+ Mostrar el total de facturas registradas en un mes:
```sql
SELECT MONTH(F.FEC_FEC) AS MES, COUNT(*) AS TOTAL
    FROM FACTURA F
        GROUP BY MONTH(F.FEC_FAC)
GO
```
```
| MES | TOTAL |
|  1  |   7   |
|  2  |   2   |
|  3  |   1   |
```
+ Mostrar el total de facturas registradas por vendedor
```sql
SELECT V.NOM_VEN+SPACE(1)+V.APE_VEN AS VENDEDOR, COUNT(*) AS [TOTAL DE FACTURAS]
    FROM FACTURA F
        JOIN VENDEDOR V ON V.COD_VEN = F.COD_VEN
    GROUP BY V.NOM_VEN+SPACE(1)+V.APE_VEN
GO
```
+ Se necesita mostrar el total de proveedores por distrito, pero solo para los distrito cuyo numero de proveedores sea mayor o igual a dos:
```sql
SELECT D.NOM_DIS AS DISTRITO, COUNT(*) AS [TOTAL]
    FROM PROVEEDOR P
        JOIN DISTRITO D ON P.COD_DIS = D.COD_DIS
    GROUP BY D.NOM_DIS
    HAVING COUNT(*) > 1
GO
```
+ Se necesita mostrar informacion agrupada sobre los años y meses del registro de las facturas, condicionados a que sean solo del primer semestre 

```sql
SELECT YEAR(F.FEC_FAC) AS [AÑO], MONTH(F.FEC_FAC) AS MES COUNT(*) AS TOTAL 
    FROM FACTURA F
    GROUP BY YEAR(F.FEC_FAC), MONTH(F.FEC_FAC)
    HAVING MONTH(F.FEC_FAC) <= 6
GO
```
## ```GROUP BY``` CON RESUMENES
Los resumenes solo se pueden aplicar a un grupo de informacion; esto permite visualizar montos o conteos realizados sobre un conjunto de informacion agrupada.
#### Formato: 
```sql
SELECT <ALL> <*> <ALIAS.CAMPO AS CAMPO>
    FROM <TABLA AS ALIAS>
    GROUP BY <CAMPO>
    [ROLLUP]
    [CUBE] <CAMPOS>
    HAVING <CONDICION>
```
### ROLLUP 
Genera filas de agregado en la clausula ```GROUP BY``` mas filas de subtotales y, tambien una fila con un total general. El numero de agrupaciones es igual al numero de exoresiones de la lista de elementos compuestos mas uno; aqui justamente muestro los resultados.

### CUBE
Genera filas de agregado en la clausila ```GROUP BY``` mas una fila de super agregado y filas de tabulacion cruzadas. El numero de agrupaciones es igual a 2(n), donde n es el numero de expresiones, algunos casos de uso de ```GROUP BY```

##### Ejemplo con ```ROLLUP```
```sql
SELECT UNI_PRO AS UNIDAD, COUNT(*) AS TOTAL
    FROM PRODUCTO
    GROUP BY UNI_PRO 
    WITH ROLLUP
GO
```

##### Ejemplo con ```CUBE```
```sql
SELECT UNI_PRO AS UNIDAD, COUNT(*) AS TOTAL
    FROM PRODUCTO
    GROUP BY CUBE (UNI_PRO)
GO
```
Si se necesita modificar el valor NULL dentro de la consulta agrupada con resumenes, se podria usar el siguiente codigo:
```sql
SELECT CASE WHEN UNI_PRO IS NULL
                THEN 'TOTAL PRODUCTOS: '
                ELSE UNI_PRO
            END AS UNIDAD,
            COUNT(*) AS TOTAL
    FROM PRODUCTO
    GROUP BY UNI_PRO
    WITH ROLLUP
GO
```
##### Ejemplos:
+ Se necesita mostrar el total de facturas segun el año en un determinado mes, ademas del total de facturas registradas:
```sql
SELECT YEAR(F.FEC_FAC) AS [AÑO], MONTH(F.FEC_FAC) AS MES, COUNT(*) AS TOTAL
    FROM FACTURA F
    GROUP BY YEAR(F.FEC_FAC), MONTH(F.FEC_FAC)
    WITH ROLLUP
GO
```
*Modificando la impresion de NULL en la agrupacion:*
```sql
SELECT CASE WHEN YEAR(F.FEC_FAC) IS NULL
                    THEN 'TOTAL'
                    ELSE CAST(YEAR(F.FEC_FAC) AS CHAR(4))
                END AS [AÑO],
        CASE WHEN MONTH(F.FEC_FAC) IS NULL
                    THEN 'TOTAL POR AÑO'
                    ELSE CAST(MONTH(F.FEC_FAC) AS CHAR(2))
                END AS MES, COUNT(*) AS TOTAL
    FROM FACTURA F
    GROUP BY YEAR(F.FEC_FAC), MONTH(F.FEC_FAC)
    WITH ROLLUP
GO
```
+ Se necesita mostrar el total de facturas segun el año de un determinado mes, ademas del total de facturas registradas:
```sql
SELECT YEAR(F.FEC_FAC) AS [AÑO], MONTH(F.FEC_FAC) AS MES, COUNT(*) AS TOTAL
    FROM FACTURA F
    GROUP BY YEAR(F.FEC_FAC), MONTH(F.FEC_FAC)
    WITH ROLLUP
GO
```
*Modificando el NULL como resultado*
```sql
SELECT CASE WHEN YEAR(F.FEC_FAC) IS NULL
                    THEN 'TOTAL'
                    ELSE CAST(YEAR(F.FEC_FAC) AS CHAR(4))
            END AS AÑO,
        CASE WHEN MONTH(F.FEC_FAC) IS NULL
                    THEN 'TOTAL POR AÑO'
                    ELSE CAST(MONTH(F.FEC_FAC) AS CHAR(2))
            END AS MES, COUNT(*) AS TOTAL
    FROM FACTURA F
    GROUP BY YEAR(F.FEC_FAC), MONTH(F.FEC_FAC)
    WITH ROLLUP
GO
```
+ Implementar una consulta que permita mostrar los proveedores de un determinado distrito:
```sql
SELECT P.*
    FROM PROVEEDOR P
    WHERE P.COD_DIS=(SELECT D.COD_DIS FROM DISTRITO D WHERE D.NOM_DIS='RIMAC')
GO
```


















