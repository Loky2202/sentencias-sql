# BULK INSERT 

Instrucion de **Transact SQL** que importa datos basicamente de un archivo de datos de una tabla de una base de datos. Esta instruccion no permite la exportacion de datos 

**Importar un archivo de datos en una tabla con un formato definido por el usuario**

#### Formato 
```sql 
BULK INSERT <NOMBRE_TABLA>
    FROM 'ARCHIVO_DATOS'
    WITH (
        FIELDTERMINATOR = <SIMBOLO_CAMPO_TERMINADOR>,
        FIRSTROW = <NUMERO_FILA>,
        ROWTERMINATOR = <SIMBOLO_FILA_TERMINADOR>
    )
```

##### Ejemplo
Se tiene una tabla PRODUCTO y los datos en un archivo txt

```sql
BULK INSERT PRODUCTO
    FROM 'C:\PRODUCTO.TXT'
    WITH (
        FIELDTERMINATOR = ',',
        ROWTERMINATOR = '\n',
        FIRSTROW = 1
    )
GO
```

