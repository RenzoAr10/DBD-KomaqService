**R06001**

**PRO6001**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/e71deff2e181024cac1d58c5e07b5a90572862f1/Documentacion%20de%20Soporte/querys/FacturacionYPagos/facturasgeneradas.png)

 ```sql
SELECT id_factura , forma_pago , fecha_emision FROM factura
 ```
**R06001**

**PRO6002**

Al presionar el el IDFACTURA, se ira a otra pestaña, mostrando los datos de esa IDFACTURA

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/e71deff2e181024cac1d58c5e07b5a90572862f1/Documentacion%20de%20Soporte/querys/FacturacionYPagos/vistaFactura.png)
 ```sql
WITH SubqueryServicios AS (
    SELECT
        S.nombre_servicio,
        S.costo,
        COUNT(*) AS cantidad_servicios,
        S.costo * COUNT(*) AS subtotal_servicio
    FROM
        factura F
    JOIN
        servicio S ON F.id_factura = S.id_factura
    WHERE
        F.id_factura = 'FAC003'
    GROUP BY
        F.id_factura, S.nombre_servicio, S.costo
),
SubqueryRepuestos AS (
    SELECT
        R.nombrerepuesto,
        R.precio,
        COUNT(*) AS cantidad_repuestos,
        R.precio * COUNT(*) AS subtotal_repuesto
    FROM
        repuesto F
    JOIN
        repuesto R ON F.id_factura = R.id_factura
    WHERE
        F.id_factura = 'FAC003'
    GROUP BY
        F.id_factura, R.nombrerepuesto, R.precio
)
SELECT
    'Servicio' AS tipo,
    nombre_servicio AS nombre,
    COUNT(*) AS cantidad,
    TRUNC(AVG(costo), 2) AS costo_unitario,
    TRUNC(SUM(subtotal_servicio), 2) AS subtotal
FROM SubqueryServicios
GROUP BY
    nombre_servicio

UNION ALL

SELECT
    'Repuesto' AS tipo,
    nombrerepuesto AS nombre,
    COUNT(*) AS cantidad,
    TRUNC(AVG(precio), 2) AS costo_unitario,
    TRUNC(SUM(subtotal_repuesto), 2) AS subtotal
FROM SubqueryRepuestos
GROUP BY
    nombrerepuesto

UNION ALL

SELECT
    'Total' AS tipo,
    NULL AS nombre,
    COUNT(*) AS cantidad,
    NULL AS costo_unitario,
    TRUNC(SUM(subtotal), 2) AS subtotal
FROM (
    SELECT
        subtotal_servicio AS subtotal
    FROM SubqueryServicios

    UNION ALL

    SELECT
        subtotal_repuesto AS subtotal
    FROM SubqueryRepuestos
) AS TotalSubtotales;

 ```


# EMPLEADO

**R06003**   **R06004** 

**PRO6003**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/60a1d4fd0b998af08f7f97751724bb9ff8d63eda/Documentacion%20de%20Soporte/querys/FacturacionYPagos/REPORTE%20DE%20VENTAS.png)

Cuando se haga click en reporte de ventas se tiene una vista de las facturas y sus caracteristicas
 ```sql
  
SELECT
    F.id_factura,F.estado,
    C.nombreempresa, F.fecha_emision, F.costo_total
FROM
    factura F
JOIN
    usuario U ON F.id_usuario = U.id_usuario
JOIN
    cliente C ON U.id_cliente = C.id_cliente;
	
 ```
Luego si se hace click en AÑADIR NUEVA VENTA, se va insertar nuevos valores:

 ```sql
INSERT INTO factura (id_factura, estado, id_usuario, fecha_emision, costo_total)
VALUES ('FAC002', 'Pagada', 'UR001', '2023-01-01', 100.00),

 ```

# INDICES

 ```sql
CREATE INDEX idx_factura_id_factura ON factura (id_factura);

CREATE INDEX idx_servicio_id_factura ON servicio (id_factura);

CREATE INDEX idx_repuesto_id_factura ON repuesto (id_factura);

 ```
**ANTES**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/ANTESfactura(id_factura).png)
![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/ANTESservicio(id_factura).png)
![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/ANTESrepuesto(id_factura).png)

**DESPUES**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/DESPUESfactura(id_factura).png)
![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/DESPUESservicio(id_factura).png)
![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/DESPUESrepuesto(id_factura).png)

# Proceso BATCH

 ```sql
DO $$ 
BEGIN
    INSERT INTO factura (id_factura, estado, id_usuario, fecha_emision, costo_total)
    VALUES ('FAC002', 'Pagada', 'UR001', '2023-01-01', 100.00);
END $$;

 ```
