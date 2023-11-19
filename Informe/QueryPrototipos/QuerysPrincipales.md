
# Módulo de Comunicación con Proveedores

R04001
![4](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/616c0aae-cef2-4f1e-a400-a784d9a21096)
 ```sql

```
R04002
![5](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/5fa26fcc-61d6-46eb-a956-f1a436b08f35)

 ```sql
INSERT INTO Solicitudes (Empleado, Proveedor, Fecha, Detalles)
VALUES ('EmpleadoNombre', 'ProveedorNombre', '2023-01-01', 'Detalles de la solicitud');
```
R04003
![6](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/e01181ab-70d8-4c20-aec3-13ae1e6d561a)
 ```sql
SELECT * FROM Pedidos WHERE NumeroPedido = 'PED001';
UPDATE Pedidos SET Estado = 'En proceso', Transportista = 'Pedro Lopez', FechaEstimadaLlegada = '2023-08-05' WHERE NumeroPedido = 'PED001';

```
# Módulo de Reporte de Servicios

R05001
![1](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/07f05f0c-11f3-49b3-a928-06edcd0f163c)
 ```sql
INSERT INTO Servicio (Servicio, Fecha, Tecnico, Maquina, Descripcion, Repuestos)
VALUES ('Nombre del Servicio', '2023-09-21', 'Nombre del Técnico', 'ID o Tipo de la Máquina', 'Descripción del trabajo realizado', 'Lista de repuestos utilizados');
```

R05002
![2](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/06145328-d418-4a01-b0da-78e57b59089d)
 ```sql

```

R05003
![3](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/f804b50c-ffdf-4fc0-a7a2-bacd793b7783)
 ```sql

```

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

**R07001  R07002   R07002**

**PRO7001**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/0796b76f2f0a29e50fef25f8a30936ef6848abc4/Documentacion%20de%20Soporte/querys/FacturacionYPagos/GectionDeVentas.png)

**(1)** 
Si se quiere mostrar las facturas de un cliente especifico:
Se inserta el nombre de la empresa del cliente

 ```sql
SELECT
   F.id_factura, F.estado,
   C.nombreempresa, F.fecha_emision, F.costo_total
FROM
   factura F
JOIN
   usuario U ON F.id_usuario = U.id_usuario
JOIN
   cliente C ON U.id_cliente = C.id_cliente
WHERE
   C.nombreempresa = 'NombreEmpresaEspecifica';
 ```

**(2)** 
Si se quiere mostrar las facturas si estan por cobrar o cancelado, para tomar decisiones:
Se selecciona (por cobrar) o (cancelado)

 ```sql
SELECT
   F.id_factura, F.estado,
   C.nombreempresa, F.fecha_emision, F.costo_total
FROM
   factura F
JOIN
   usuario U ON F.id_usuario = U.id_usuario
JOIN
   cliente C ON U.id_cliente = C.id_cliente
WHERE
   F.estado = 'por cobrar';

 ```

**(3)** 
Si se quiere mostrar las facturas desde una fecha inicial(se selecciona la fecha) hasta la fecha actual:
 ```sql
SELECT
    F.id_factura,
    F.estado,
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
    F.fecha_emision >= '2023-01-01' AND F.fecha_emision <= CURRENT_DATE;
 ```

