# CONSULTAS INTERNAS
Conocidas como combinacion equivalente en la cual los valores de las columnas de una tabla se comparan mediante el operador de igualdad a los otros valores de una segunda tabla. 

#### Formato:
```sql
SELECT <ALL> <*>
    <ALIAS.CAMPO AS CAMPO>
    FROM <TABLA A> <AS ALIAS>
        <INNER JOIN TABLA B ON CAMPO_A = CAMPO_B>
    <ORDER BY CAMPO ASC | DESC>
```

##### Ejemplo:
+ Usando la tablas: VENDEDOR y DISTRITO
```sql
SELECT V.COD_VEN AS CODIGO, V.NOM_VEN+SPACE(1)+V.APE_VEN AS VENDEDOR, V.SUE_VEN AS SUELDO, V.FIN_VEN AS [FECHA DE INICIO], D.NOMB_DIS AS DISTRITO
    FROM VENDEDOR V
        INNER JOIN DISTRITO D ON V.COD_DIS = D.COD_DIS
GO
```
*Funciona igual si invertimos las tablas.*

+ Usando 3 tablas: FACTURA, VENDEDOR Y CLIENTE.
```sql
SELECT F.NOM_FAC AS FACTURA, F.FEC_FAC AS [FECHA FACTURA], V.NOM_VEN+SPACE(1)+V.APE_VEN AS VENDEDOR, C.RSO_CLI AS CLIENTE 
    FROM FACTURA F
    INNER JOIN VENDEDOR V ON V.COD_VEN = F.COD_VEN
    INNER JOIN CLIENTE C ON C.COD_CLI = F.COD_CLI
GO
```
*Se usa la tabla que relaciona o tiene en comun la mayor cantidad de campos relacionados*