# USO DE MERGE
Se usa para sincrinizar informacion entre tablas. Puede usar operaciones de: INSERCION, ACTUALIZACION O ELIMINACION en una misma tabla.

Permite realizar una comparacion entre dos tablas con la misma estructura. Quizas en una copia de seguridad; ya que ```MERGE``` puede igualar los registros entre dos tablas.

##### Ejemplo
Implementar un ```MERGE``` que permita registrar un nuevo producto, si este producto ya se encuentra registrado, solo actualizara sus datos; caso, contrario, lo registra como uno nuevo.

```sql
--Declarando Variables
DECLARE @COD CHAR(4), @DES VARCHAR(60), @PRE MONEY
GO
SELECT @COD = 'P001', @DES = 'Sistema wifi', @PRE = 129.99
GO

--Sentencia MERGE
MERGE PRODUCTO AS TARGET
    USING( SELECT @COD, @DES, @PRO )
    AS SOURCE( COD_PRO, DES_PRO, PRE_PRO )
    ON( TARGET.COD_PRO = SOURCE.COD_PRO )
    WHEN MATCHED THEN 
        UPDATE SET DES_PRO = SOURCE.DES_PRO, PRE_PRO = SOURCE.PRE_PRO
    WHEN NOT MATCHED THEN
        INSERT VALUES( SOURCE.COD_PRO, SOURCE.DES_PRO, SOURCE.PRE_PRO );  
GO
```

