
![GestiónOC v2](https://github.com/RenzoAr10/DBD-KomaqService/assets/144966624/733e2830-1eb9-4a05-bcc1-695bee6e5817)


```sql

SELECT
    oc.id_orden_compra,
    oc.fecha_orden,
    oc.estado,
    s.cantidad_servicios,
    c.nombre || ' ' || c.apellido_paterno || ' ' || c.apellido_materno || ' ' || c.nombre AS nombre_cliente,
    p.nombre_empresa,
    f.costo_total
FROM
    OrdenCompra oc
    INNER JOIN Servicio s ON oc.id_servicio = s.id_servicio
    INNER JOIN Cliente c ON oc.id_cliente = c.id_cliente
    INNER JOIN Proveedor p ON s.id_proveedor = p.id_proveedor
    INNER JOIN Factura f ON s.id_fatura = f.id_factura;


UPDATE OrdenCompra
SET estado = 'Finalizado'
WHERE estado = 'En proceso' AND id_orden_compra = 'OC002';
```
