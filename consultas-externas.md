# CONSULTAS EXTERNAS

Se llaman asi a una combinacion en la cual se toma importancia a los valores que son equivalentes. Las combinaciones externas se especifican en las clausulas ```FROM``` con uno de los siguientes conjuntos:
+ LEFT JOIN o LEFT OUTER JOIN
+ RIGHT JOIN o RIGHT OUTER JOIN

#### Formato:
```sql 
SELECT <ALL> <*> <ALIAS.CAMPO AS CAMPO>
    FROM <TABLA> <AS ALIAS>
    <LEFT | RIGHT JOIN>
    <ORDER BY CAMPO ASC | DESC>
```

## ```LEFT JOIN```
MUestra todas las filas de la tabla ubicada a la izquierda de la consulta, forzando a la otra tabla a mostrar valores tipo **NULL** para realizar una equivalencia entre tabla
#### Formato:
```sql
SELECT <ALL> <*>
    <ALIAS.CAMPO AS CAMPO>
    FROM <TABLA> <AS ALIAS>
        <LEFT JOIN>
    <ORDER BY CAMPO ASC | DESC>
```
##### Ejemplo:
+ Muestra todos los valores de DISTRITO y donde no hay vendedor asignado lo representa con **NULL**
```sql
SELECT D.* 
    FROM DISTRITO D
        LEFT JOIN VENDEDOR V ON D.COD_DIS = V.COD_DIS
GO
```
+ Mostrar los distritos que no registran vendedor
```sql
SELECT D.*
    FROM DISTRITO D
        LEFT JOIN VENDEDOR V ON D.COD_DIS = V.COD_DIS
    WHERE V.COD_DIS IS NULL
GO
```
+ Tambien condicionando cualquier campo de VENDEDOR
```sql
SELECT D.*
    FROM DISTRITO D
        LEFT JOIN VENDEDOR V ON D.COD_DIS = V.COD_DIS
    WHERE V.SUE_VEN IS NULL
GO
```

## ```RIGHT JOIN```
Muestra todas las filas de la tabla ubicada en la derecha de la consulta, forzando a la otra tabla a mostrar valores tipo **NULL** para realizar una equivalencia entre las tablas.
#### Formato:
```sql
SELECT <ALL> <*>
    <ALIAS.CAMPO AS CAMPO>
    FROM <TABLA> <AS ALIAS>
        <RIGHT JOIN>
    <ORDER BY CAMPO ASC | DESC>
```
##### Ejemplo:
+ Muestra todos las columnas de la tabla VENDEDOR por estar del lado izquierdo, muestra valores tipo **NULL** ya que la tabla DISTRITO esta del lado derecho, forzando a la tabla de la izquierda a mostrar todo los registros y rellenar con nulos.
```sql
SELECT * 
    FROM VENDEDOR V
        RIGHT JOIN DISTRITO D ON D.COD_DIS = V.COD_DIS
GO
```
+ Mostrar los registros que no registran vendedor
```sql
SELECT D.* 
    FROM VENDEDOR V
        RIGHT JOIN DISTRITO D ON D.COD_DIS = V.COD_DIS
    WHERE V.COD_DIS IS NULL
GO
```
## ```FULL JOIN```
Combina los valores de la primera tabla con los valores de la segunda tabla, de la forma que siempre devuelva filas de ambas tablas, aunque no cumpla la condicion de correspondencia.
#### Formato: 
```sql
SELECT <ALL> <*>
    <ALIAS.CAMPO AS CAMPO>
    FROM <TABLA> <AS ALIAS>
        <FULL JOIN>
    <ORDER BY CAMPO ASC | DESC>
```
##### Ejemplo:
+ Este tipo de union mostrara las filas de VENDEDOR y DISTRITO, asi no tengan asociacion
```sql
SELECT * 
    FROM VENDEDOR V
        FULL JOIN DISTRITO D ON D.COD_DIS = V.COD_DIS
GO
```
+ Mostrar las distritos que no registran vendedor
```sql
SELECT D.*
    FROM VENDEDOR V
        FULL JOIN DISTRITO D ON V.COD_DIS = D.COD_DIS
    WHERE V.APE_VEN IS NULL
GO
```