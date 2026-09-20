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

![Resultado pregunta 2](img/p01.png)

**Comentario:** Para resolver esto, usé ``` WHERE discontinued = 0 ``` para asegurarme de filtrar solo los productos que siguen activos (0 = false; 1 = true). Para el "precio unitario esté entre 10 y 50 euros" lo mejor es usar el operador ```BETWEEN```. Al final simplemente hay que ordenar de mayor a menor precio usando el as que asignamos antes ```ROUND(unit_price::numeric, 2) AS precio```.

***
## Pregunta 2 — Concentración geográfica de la cartera

**Enunciado:** Dirección quiere saber en qué mercados está realmente concentrada la base de clientes antes de decidir dónde abrir delegación.

Cuenta cuántos clientes hay en cada país y muestra únicamente aquellos países con **5 o más clientes**, ordenados de mayor a menor. Indica también cuántas ciudades distintas hay en cada uno de esos países.

**Consulta:**

```sql
SELECT country AS pais,
       COUNT(customer_id) AS num_clientes,
       COUNT(DISTINCT city) AS num_ciudades
FROM customers
GROUP BY country
HAVING COUNT(customer_id) >= 5
ORDER BY num_clientes DESC;
```

**Resultado:**

![Resultado pregunta 2](img/p02.png)

**Comentario:** Para resolver esto, usé `GROUP BY country` para agrupar los registros por país. Para no contar la misma ciudad dos veces lo mejor es usar `COUNT(DISTINCT city)`. Al final simplemente hay que filtrar los que tienen 5 o más clientes usando `HAVING COUNT(customer_id) >= 5` porque la condición se aplica después de haber contado.

## Pregunta 3 — Alerta de reposición

**Enunciado:** Logística necesita detectar qué referencias están en riesgo de rotura de stock.

Localiza los productos activos cuyas unidades en stock sean **inferiores o iguales** a su nivel de reposición. Muestra el nombre, las unidades en stock, el nivel de reposición, las unidades ya pedidas al proveedor y una columna de texto que indique `'CRÍTICO'` cuando el stock sea 0 y `'AVISO'` en el resto de casos.

**Consulta:**

```sql
SELECT product_name AS producto,
       units_in_stock AS stock,
       reorder_level AS nivel_reposicion,
       units_on_order AS pedido_a_proveedor,
       CASE 
           WHEN units_in_stock = 0 THEN 'CRÍTICO'
           ELSE 'AVISO'
       END AS situacion
FROM products
WHERE discontinued = 0 
  AND units_in_stock <= reorder_level;
```

**Resultado:**

![Resultado pregunta 3](img/p03.png)

**Comentario:** Para resolver esto, usé `WHERE discontinued = 0 AND units_in_stock <= reorder_level` para asegurarme de filtrar los productos activos que están bajo mínimos. Para crear la columna de "situación" lo mejor es usar el condicional `CASE WHEN`(Funciona igual que un if - else) devolviendo 'CRÍTICO' si es 0, y 'AVISO' con el `ELSE`. Al final simplemente hay que mostrar los campos solicitados en el SELECT.
