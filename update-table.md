# UPDATE TABLE
La sentecencia ```UPDATE``` permite la modificacion o actualizacion a un conjunto de registros de una tablao vista. Dependiendo de la condicion.

#### Formato:
```sql
UPDATE <NOMBRE_TABLA> 
    SET <CAMPO = VALOR>, <CAMPO_2 = VALOR>
        WHERE <CONDICION>
```

##### Ejemplo: 
```UPDATE``` a la tabla PRODUCTO  
Al campo ```PRE_PRO``` le sumaremos 2 al valor que ya tiene.
```sql
UPDATE PRODUCTO
    SET PRE_PRO += 2
GO
```

Actualizar el Stock por dos, si el stock es menos a 50
```sql
UPDATE PRODUCTO
    SET SAC_PRO *= 2
        WHERE SAC_PRO <= 50
GO
```

Actualizar el precio de los productos descontando un 50% del precio actual solo para prodcutos con còdigo "P001, P005, P010".
```sql
UPDATE PRODUCTO
    SET PRE_PRO *= 0.5
        WHERE COD_PRO IN ( 'P001', 'P005', 'P010' )
GO
```

Actualizar descripcion del producto codigo 'P004'
```sql
UPDATE PRODUCTO
    SET DES_PRO = 'Papel 75'
        WHERE = COD_PRO = 'P004'
GO
```

## Actualizar Dos Tablas

#### Ejemplo:
Actualizar de la tabla PROVEEDOR el campo TEL_PRV **Donde el nombre de distrito sea 'RIMAC'**
```sql
UPDATE PROVEEDOR 
    SET TEL_PRV = '0000-00'
    FROM PROVEEDOR AS P
    JOIN DISTRITO AS D ON P.COD_DIS = D.COD_DIS
    AND COD_DIS = ( SELECT COD_DIS FROM DISTRITO WHERE NOM_DIS = 'RIMAC' )
```
*Consultamos en la tabla DISTRITO CUAL ES CODIGO PARA EL NOMBRE DE DISTRITO 'RIMAC' Y AL OBTENERLO ACTUALIZAMOS EL CAMPO DE LA TABLA PROVEEDOR*

Otra forma:

```sql
UPDATE PROVEEDOR
    SET TEL_PRV = '0000-00'
    WHERE COD_DIS = ( SELECT COD_DIS FROM DISTRITO WHERE NOM_DIS = 'RIMAC' )
GO
```
## Actualizando Usando Variables

```sql
DECLARE @IMPORTADO CHAR(1) = 'F'

UPDATE PRODUCTO 
    SET IMP_PRO = @IMPORTADO
        WHERE UNI_PRO = 'Doc'
GO
```