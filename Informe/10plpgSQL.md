# Informe de gestion 

**PRO7001**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/0796b76f2f0a29e50fef25f8a30936ef6848abc4/Documentacion%20de%20Soporte/querys/FacturacionYPagos/GectionDeVentas.png)

 ```sql
CREATE OR REPLACE FUNCTION generar_reporte_ventas()
RETURNS TABLE (
    id_factura VARCHAR(10),
    estado VARCHAR(100),
    nombreempresa VARCHAR(50),
    fecha_emision VARCHAR(100),
    costo_total DECIMAL(8,2)
) AS
$$
BEGIN
    RETURN QUERY
    SELECT
        F.id_factura,
        F.forma_pago,
        C.nombreempresa,
        F.fecha_emision,
        F.costo_total
    FROM
        factura F
    JOIN
        usuario U ON F.id_usuario = U.id_usuario
    JOIN
        cliente C ON U.id_cliente = C.id_cliente
    WHERE
        C.nombreempresa = 'Mminera las bambas s.a.';
END;
$$ LANGUAGE plpgsql;

---------

SELECT * FROM generar_reporte_ventas();
 ```



# Modulo facturacion y pagos

**PRO6003**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/60a1d4fd0b998af08f7f97751724bb9ff8d63eda/Documentacion%20de%20Soporte/querys/FacturacionYPagos/REPORTE%20DE%20VENTAS.png)

Cuando se haga click en reporte de ventas se tiene una vista de las facturas y sus caracteristicas

 ```sql
DO $$ 
BEGIN
    INSERT INTO factura (id_factura, estado, id_usuario, fecha_emision, costo_total)
    VALUES ('FAC002', 'Pagada', 'UR001', '2023-01-01', 100.00);
END $$;
```



# Modulo de Gestion de Ordenes de compras

![GestiónOC v2](https://github.com/RenzoAr10/DBD-KomaqService/assets/144966624/cb6016a7-22ea-4728-a190-ac7828a50c05)

```sql
CREATE OR REPLACE FUNCTION info_orden_compra()
RETURNS TABLE (
    id_orden_compra VARCHAR(10),
    fecha_oc VARCHAR(100),
    estado_oc VARCHAR(100),
    cantidad_servicios INT,
    nombre_cliente TEXT,
    proveedor VARCHAR(100),
    costo_total DECIMAL(8,2)
) AS $$
BEGIN
    RETURN QUERY
    SELECT
        OC.id_orden_compra,
        OC.fecha_oc,
        OC.estado_oc,
        S.cantidad_servicios,
        CONCAT(C.apellido_paterno, ' ', C.apellido_materno, ' ', C.nombre) AS nombre_cliente,
        P.nombre_empresa AS proveedor,
        F.costo_total
    FROM OrdenCompra OC
    JOIN Usuario U ON OC.id_orden_compra = U.id_orden_compra
    JOIN Cliente C ON U.id_cliente = C.id_cliente
    JOIN Servicio S ON OC.id_orden_compra = S.id_orden_compra
    JOIN Repuesto R ON R.id_servicio = S.id_servicio
    JOIN Proveedor_Repuesto PR ON R.id_repuesto = PR.id_repuesto
    JOIN Proveedor P ON PR.id_proveedor = P.id_proveedor
    LEFT JOIN Factura F ON S.id_factura = F.id_factura;
    RETURN;
END;
$$ LANGUAGE plpgsql;

SELECT * FROM info_orden_compra();
```
```sql
--Actualizando estado de orden de compra

CREATE OR REPLACE FUNCTION actualizar_estado_orden_compra(
    p_id_orden_compra INT)
RETURNS VARCHAR(100) AS $$
DECLARE nuevo_estado VARCHAR(100);
BEGIN
    UPDATE OrdenCompra
    SET estado_oc = 'Finalizado'
    WHERE id_orden_compra = p_id_orden_compra
    RETURNING estado_oc INTO nuevo_estado;

    RETURN nuevo_estado;
END;
$$ LANGUAGE plpgsql;
```
