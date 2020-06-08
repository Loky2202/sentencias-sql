# CONSULTAS AGRUPADAS.
Este tipode consultas permite mostrar informacion en forma de grupos con uno o mas propositos. Hay que tener en cuenta que las consultas agrupadas aumentan su productividad cuando se usan con funciones agregadas.
#### Formato:
```sql
SELECT <ALL> <*>
    <ALIAS.CAMPO AS CAMPO>
    FROM <TABLA> <AS ALIAS>
        <INNER | LEFT | RIGHT | CROSS JOIN>
    <WHERE CONDICION>
    <GROUP BY CAMPO>
    <HAVING CONDICION>
    <ORDER BY CAMPO ASC | DESC>
```