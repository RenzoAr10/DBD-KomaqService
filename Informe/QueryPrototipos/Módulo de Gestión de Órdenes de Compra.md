


```sql

SELECT oc.id_orden_compra, oc.estado_oc, oc.fecha_orden, f.costo_total
FROM OrdenCompra oc
INNER JOIN Cliente c ON oc.id_cliente = c.id_cliente
INNER JOIN Servicio s ON oc.id_servicio = s.id_servicio,
INNER JOIN Factura f ON f.id_factura = s.id_factura,
WHERE c.id_cliente = 'CL001';

```
