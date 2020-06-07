# SELECT

## Recuperacion de datos

```sql
SELECT <ALL> <*> -- columnas, filas devueltas
    <DISTINCT> -- solo devuelve filas unicas
    <TOP VALOR[PERCENT]> -- porcentaje de fila devuelto
    <ALIAS.CAMPO> -- campo devuelto
    <AS CAMPO> -- titulo para el campo devuelto
    <INTO TABLA_DESTINO> -- crea una nueva tabla y envia la consulta
FROM <TABLA> <AS ALIAS> -- tabla a consultar
    <INNER | LEFT | RIGHT | CROSS JOIN> -- une dos o mas tablas para generar una consulta
    <WHERE CONDICION> -- condicion de la consulta
    <GROUP BY CAMPO> -- Agrupa un conjunto de registros, con valores especificados
    <HAVING CONDICION> -- condicion para GROUP BY
    <ORDER BY CAMPO ASC | DESC> -- ordena los registro por una columna especifica
```

**Consultas Basicas**
#### Formato: 
```sql
SELECT <ALL> <*>
    FROM <TABLA> <AS ALIAS>
GO
```

##### Ejemplos:
Devuelve todas las filas y columnas de la tabla PRODUCTO
```sql
SELECT ALL * 
    FROM PRODUCTO
GO
```
Asignando un alias a la tabla "P"
```sql
SELECT P.* FROM PRODUCTO P
GO
```
Ocupando referencia sin alias
```sql
SELECT PRODUCTO.* FROM PRODUCTO 
GO
```

**Muestra valores no retidos**
#### Formato:
```sql
SELECT <DISTINCT> <CAMPO>
    FROM <TABLA>
GO
```
##### Ejemplo
Mostrar todos los precios de la tabla PRODUCTO
```sql
SELECT UNI_PRO FROM PRODUCTO
GO
```

Mostrar todos los precios sin repetir el valor
#### Formato:
```sql
SELECT <ALL> <*>
    <DISTINCT>
    FROM <TABLA> <AS ALIAS>
    <ORDER BY CAMPO ASC | DESC>
```
Devuelve los valores sin repetir del campo UNI_PRO      
```sql
SELECT DISTINCT UNI_PRO FROM PRODUCTO
GO
```

## USO DE ```ASC``` Y ```DESC```

Muestra los registros de los campos ordenados por la columna seleccionada

#### Ejemplos:

Muestra los registros ordenados por la columna "Razon Social" de forma **acendente**
```sql
SELECT * 
    FROM CLIENTE ORDER BY RSO_CLI ASC
GO
```

Tambien se puede especificar el numero de columnas de la tabla:
```sql
SELECT * 
    FROM CLIENTE ORDER BY 2
GO
```
Ordena de forma **descedente** por año y luego los meses **ascendentes**.
```sql
SELECT * 
    FROM CLIENTE 
        ORDER BY YEAR(FEC_REG) DESC, MONTH(FEC_REG)
GO
```
```sql
SELECT C.*
    FROM CLIENTE C
    ORDER BY YEAR( C.FEC_REG ) DESC,
                MOTH( C.FEC_REG ) ASC
GO
```

## TOP PERCENT
Consulta por cantidad de registros que permite contralar la cantidad de filas mostradas en el resultado.

#### Formato:
```sql 
SELECT <ALL> <*>
    <DISTINCT>
    <TOP VALOR[PERCENT]>
    FROM <TABLA> <AS TABLA>
    <ORDER BY CAMPO ASC | DESC> 
```

##### Ejemplos:

Muestra los 5 primeros productos registrados
```sql
SELECT TOP 5 * FROM PRODUCTO
GO
```
Listar los 3 productos mas caro que se registran en la tabla
```sql 
SELECT TOP 3 *
    FROM PRODUCTO
    ORDER BY PRE_PRO DESC
GO
```

listar el 50% de los primeros productos
```sql
SELECT TOP 50 PERCENT *
    FROM PRODUCTO
GO
```

## CONSULTA ESPECIFICANDO CAMPOS
Permite especificar que columnas se mostraran en el resultado.
#### Formato:
```sql
SELECT <CAMPO_1>, <CAMPO_2>, <CAMPO_N> <ALIAS.CAMPO>
    FROM <TABLA> <AS ALIAS>
```
##### Ejemplos:
Mostrar las columnas: codigo, descripcion, precio, stock de la tabla PRODUCTO
```sql
SELECT P.COD_PRO, P.DES_PRO, P.PRE_PRO, P.SAC_PRO
    FROM PRODUCTO P
GO
```

## CONSULTAS CON CABECERAS
Este tipo de consultas permite asignar una cabecera a las columnas del resultado.

#### Formato:
```sql
SELECT <ALIAS.CAMPO> <AS CAMPO>
    FROM <TABLA> <AS ALIAS>
```
##### Ejemplo:
Mostrar cabeceras a los campos en la consulta.
```sql
SELECT COD_PRO AS CODIGO, SAC_PRO [STOCK ACTUAL]
    FROM PRODUCTO
GO
```

## CONSULTA DE CAMPOS CALCULADOS
Este tipo de consulta permite mostrar columnas adicionales a la tabla. Estàs columnas se pueden obtener apartir de una expresion.

#### Formato:
```sql
SELECT <ALIAS.CAMPO> <[CAMPO ADICIONAL]>
    FROM <TABLA> <AS ALIAS>
```
##### Ejemplo:
Mostrar los productos con precio de venta mas 10%
```sql
SELECT COD_PRO AS CODIGO, DES_PRO AS DESCRIPCION, PRE_PRO AS PRECIO, ( PRE_PRO * 1.1 ) AS [PRECIO VENTA]
    FROM VENDEDOR
GO
```
Muestra los datos del vendedor donde el nombre es la union de dos campos y los separa un espacio en blanco
```sql
SELECT COD_VED AS CODIGO, NOM_VEN+SPACE(1)+APE_VEN AS VENDEDOR, FIN_VEN AS [FECHA DE INICIO]
    FROM VENDEDOR
GO
```

## CONSULTA QUE CREA UNA TABLA DE REGISTRO
Este tipo de consultas permite crear una tabla con informacion resultante de una consuta es decir, el resultado se almacenara en la nueva tabla formando de esta manera su estructura.
#### Formato:
```sql
SELECT <*>
    <ALIAS.CAMPO> <AS CAMPO>
    <INTO TABLA_DESTINO>
    FROM <TABLA> <AS TABLA>
    <ORDER BY CAMPO ASC | DESC>
```

##### Ejemplos:

Hacer una copia de la tabla PRODUCTO
```sql
SELECT * INTO PRODUCTO_BAK
    FROM PRODUCTO
GO
```

Crear una tabla reporte de productos
```sql
SELECT COD_PRO AS CODIGO, DES_PRO AS DESCRIPCION
    INTO REPORTE_PRODUCTO
    FROM PRODUCTO
GO
```

## CONSULTA CONDICIONALES
Filtra registros de una tabla, el filtro mostrara algunos que cumplan con una determinada codicion.

#### Formato:
```sql
SELECT <ALL> <*>
    <ALIAS.CAMPO> <AS CAMPO>
    FROM <TABLA> <AS ALIAS>
    <WHERE CONDICION>
    <ORDER BY CAMPO ASC | DESC>
```


## OPERADORES LOGICOS
```sql
AND -- REPRESENTA LA "Y". Si dos expresiones son True devuele True  
ANY -- Devuelve True si alguna de las expresiones del conjunto es True  
BETWEEN -- Devueve True si el valor se encuentra en el rango(cadena o numero)  
IN -- Devuelve True si el operador se encuentra en la lista de valores especifico
LIKE -- Devuelve True si el operador coincide a lo mas con un patron especifico
    Encontramos:
    %    -- Representa uno o mas caracteres
    _    -- Representa a un solo caracter
    []   -- Cualquier caracter individual dentro de un conjunto o intervalo de caracteres
    [^]  -- Representa cualquier caracter individual fuera del intervalo especificado
    IS NOT NULL -- Representa que el contenido de una columna no esta vacia 
    NOT  -- Invierte el valor Booleano
    OR   -- Representa la "O" logica
    SOME -- Devuelve True si alguna comparacion de un conjunto es True
```

##### Ejemplos:

Busca por codigo y año
```sql
SELECT C.* FROM CLIENTE C
    WHERE COD_CLI = 'D05' AND YEAR(FEC_REG) = 2013
GO
```
Devuelve los clientes donde el codigo de registro tenga por nombre 'SAN MIGUEL'
```sql
SELECT C.* FROM CLIENTE C
    WHERE C.COD_DIS = ANY(SELECT COD_DIS FROM DISTRITO
                                        WHERE NOM_DIS = 'SAN MIGUEL')
GO
```
Clientes registrados en esos años
```sql
SELECT C.* FROM CLIENTE C
    WHERE YEAR(C.FEC_REG) BETWEEN 2008 AND 2011
GO
```
Mostrar los datos de la tabla donde los cliente tengan esos codigos.
```sql
SELECT C.* FROM CLIENTE C 
    WHERE COD_DIS IN ('D01', 'D14', 'D16')
GO
```
Buscar en el campo RSI_CLI donde empice con "M"
```sql
SELECT C.* FROM CLIENTE C
    WHERE RSO_CLI LIKE 'M%'
GO
```
Buscar nombre de contacto cuyo nombre tenga como segunda letra "A"
```sql
SELECT C.* FROM CLIENTE C
    WHERE NOM_CLI LIKE '_A%'
GO
```
Buscar los registro del nombre inice con "M", "C" y "D"
```sql
SELECT C.*FROM CLIENTE C
    WHERE NOM_CLI LIKE '[MCD]%'
GO
```
Muestra los registros cuyo nombre de contacto tenga como segunda letra la "A", "E" o "R"
```sqL
SELECT C.* FROM CLIENTE C
    WHERE COD_CLI LIKE '_[AER]%'
GO
```
Los registros que no empiezen con las letras "F", "M" o "C"
```sql
SELECT C.* FROM CLIENTE C
    WHERE RS_CLI LIKE '[^FMC]%'
GO
```
Muestra los registros que el campo no presenta un valor nulo
```sql
SELECT C.* FROM CLIENTE C
    WHERE RSC_CLI IS NOT NULL
GO
```
Muestra los registros cuyo año sea diferente al 2012
```sql
SELECT C.* FROM CLIENTE C
    WHERE NOT YEAR(FEC_REG) = 2012
GO
```
Mostrar todos los distritos donde aun no se registran clientes
```sql
SELECT * FROM DISTRITO
    WHERE COD_DIS = SOME(SELECT COD_DIS FROM CLIENTE)
GO
```