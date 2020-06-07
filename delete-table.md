# DELETE TABLE

Elimina registros especificos de una tabla. Hay que tener en cuenta que para eliminar registros, estos no deben encontrarse asociados a otra tabla, ya que romperia la regla de **integridad**

#### Formato:

```sql
DELETE <FROM> <NOMBRE_TABLA>
    WHERE <CONDICION>
```

###### Ejemplo
Borra toda la tabla producto
```sql
DELETE PRODUCTO
GO
```

Borra los registros cuyo stock sea menor a 50
```sql
DELETE PRODUCTO
    WHERE SAC_PRO < 50
GO
```