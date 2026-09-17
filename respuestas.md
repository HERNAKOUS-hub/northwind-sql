
Una sección por pregunta, las 20, en orden. Cada una con esta estructura:

```markdown
## Pregunta 7 — Clientes sin actividad comercial

**Enunciado:** Lista todos los clientes con el número de pedidos que ha
realizado cada uno...

**Consulta:**

```sql
-- Clientes con su volumen de pedidos, incluidos los que nunca han comprado
SELECT c.company_name AS cliente,
       c.country      AS pais,
       COUNT(o.order_id) AS num_pedidos
FROM customers c
LEFT JOIN orders o ON o.customer_id = c.customer_id
GROUP BY c.company_name, c.country
ORDER BY num_pedidos;
```

**Resultado:**

!Resultado pregunta 7

**Comentario:** He usado `COUNT(o.order_id)` en lugar de `COUNT(*)` porque...
```
