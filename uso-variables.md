# USO DE VARIABLES

**Declarando variables**
```sql 
DECLARE @VAR_1 <TIPO>, @VAR_2 <TIPO>, @VAR_3 <TIPO>
```

**Asigando valor**
```sql
SELECT @VAR_1 = 'VALOR', @VAR_2 = VALOR, @VAR_3 = VALOR
```
Ò
```sql
SET @VAR_1 = 'VALOR', @VAR_2 = VALOR, @VAR_3 = VALOR
```

**Llenado de una tabla con variables**
```sql
INSERT INTO <NOMBRE_TABLA> VALUES ( @VAR_1, @VAR_2, @VAR_3 )
```