


```sql

SELECT
    oc.id_orden_compra,
    oc.fecha_orden,
    c.nombre_cliente,
    s.descripcion_servicio,
    oc.estado
FROM
    OrdenCompra oc
    INNER JOIN Cliente c ON oc.id_cliente = c.id_cliente
    INNER JOIN Servicio s ON oc.id_servicio = s.id_servicio,
WHERE
    c.id_cliente = 'CL001';

```
