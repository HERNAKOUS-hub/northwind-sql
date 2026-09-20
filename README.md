# Práctica de Análisis de Datos: Northwind Traders

**Autor:** [Hernán Fernández]

---

## Entorno de desarrollo

| Tecnología           | Versión / Herramienta | Descripción                              |
|----------------------|-----------------------|------------------------------------------|
| Motor de base de datos | PostgreSQL 18       | Sistema de gestión de bases de datos     |
| Cliente gráfico      | pgAdmin 4             | Herramienta de administración y consulta |

---

## Instrucciones para reproducir el entorno

Para poder ejecutar las consultas de este repositorio es necesario preparar la base de datos siguiendo estos pasos desde **pgAdmin**:

### 1. Crear la base de datos

Abre la herramienta **Query Tool** en el servidor principal y ejecuta el siguiente comando para garantizar que la codificación acepta correctamente los caracteres especiales del dataset:

```sql
CREATE DATABASE northwind
    WITH ENCODING = 'UTF8'
         TEMPLATE = template0;
```

### 2. Cargar el modelo y los registros

1. Selecciona la base de datos `northwind` recién creada en el árbol de la izquierda (es fundamental para no cargar los datos por error en la base `postgres`).
2. Abre un nuevo **Query Tool**.
3. Carga el archivo `northwind.sql` proporcionado en las prácticas y pulsa ejecutar (**F5**) para generar las 14 tablas, insertar los registros y aplicar las restricciones de integridad referencial.

---

## Diagrama Entidad-Relación

A continuación se muestra el modelo de la base de datos que refleja la estructura exacta de las tablas y sus conexiones físicas (claves ajenas) según constan en el motor tras ejecutar el script de instalación:

![Diagrama](img/diagrama-er.png)

---

## Índice de consultas

El desarrollo completo de la práctica, que incluye el código SQL, el razonamiento técnico y las capturas de pantalla con los resultados para las **20 preguntas de negocio**, se encuentra documentado en el siguiente archivo:

📄 **[Ver las 20 consultas resueltas](respuestas.md)**
