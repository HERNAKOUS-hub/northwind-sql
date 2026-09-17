# Sección 1. Fundamentos: filtrado y agregación


## Pregunta 1 — Catálogo comercial activo

**Enunciado:** El equipo de ventas prepara la tarifa de la próxima campaña y necesita el catálogo depurado.

Obtén los productos que **no** están descatalogados y cuyo precio unitario esté entre 10 y 50 euros, ambos incluidos. Muestra el nombre del producto y su precio redondeado a dos decimales, ordenado de mayor a menor precio.

**Consulta:**

```sql
SELECT product_name AS producto,
       ROUND(unit_price::numeric, 2) AS precio
FROM products
WHERE discontinued = 0 
  AND unit_price BETWEEN 10 AND 50
ORDER BY precio DESC;
```

**Resultado:**

!Resultado pregunta 1

**Comentario:** Se ha utilizado discontinued = 0 para asegurar que solo se muestran los productos activos, tal como indicaba la pista. El filtrado de precio se ha resuelto de forma limpia con la cláusula BETWEEN 10 AND 50, y finalmente se ha ordenado de forma descendente (DESC) utilizando directamente el alias de la columna precio.
