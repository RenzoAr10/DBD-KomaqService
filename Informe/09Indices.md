
# Facturacion y Pagos

**PRO6002**

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
INDICES
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


# Informe de Gestion

**PRO7001**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/0796b76f2f0a29e50fef25f8a30936ef6848abc4/Documentacion%20de%20Soporte/querys/FacturacionYPagos/GectionDeVentas.png)
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

 ```sql
-- Crear un índice en la columna nombreempresa de la tabla cliente
CREATE INDEX idx_nombreempresa ON cliente (nombreempresa);
```
**ANTES**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/DESPUESnombreempresa.png)

**DESPUES**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/ANTESnombreempresa.png)


## Consulta de Empleados y Repuestos:

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/7fe07380-3b13-4a8a-94cf-4c05973d3767)


 ```sql
SELECT IdEmpleado, NombreEmpleado FROM Empleado;
SELECT IdRepuesto, NombreRepuesto FROM Repuesto;

CREATE INDEX idx_empleado_id ON Empleado(IdEmpleado);
CREATE INDEX idx_repuesto_id ON Repuesto(IdRepuesto);

 ```
**ANTES**

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/4d19b946-7214-4e2c-917c-6958b882a136)

 
 
**DESPUES**

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/be9ae2dc-c704-4813-b20b-50d038872479)




![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/c06eecc7-7289-4dd5-be15-d99f328dcf76)

## Consulta con JOIN y Filtros:
 ```sql
SELECT idServicio, NombreServicio, IdOrdenCompra, NombreUsuario 
FROM Servicio as S
INNER JOIN OrdenCompra as cp ON s.IdOrdenCompra = cp.IdOrdenCompra
INNER JOIN NombreUsuario as un ON s.nombreUsuario = un.nombreUsusario
WHERE nombreServicio = nombrex AND OrdenCompra = 'OC00x' AND NombreCliente = 'nombreclientex';

CREATE INDEX idx_servicio_idorden ON Servicio(IdOrdenCompra);
CREATE INDEX idx_servicio_nombre ON Servicio(nombreServicio);
CREATE INDEX idx_ordencompra_id ON OrdenCompra(IdOrdenCompra);
CREATE INDEX idx_nombreusuario_nombre ON NombreUsuario(nombreUsusario);
 ```
**Antes**

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/c21b2248-163f-40f2-ae4d-2b7a1c16b2fb)

**Despues**


![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/d7ae87dc-12ee-4749-a9eb-bc3092918797)


## Cálculo de Porcentaje de Actividades Completadas:
 ```sql
((SELECT COUNT(*) FROM AccionesRecomendada WHERE idOrdenCompra = 'OC001' and Estado = 'COMPLETADO') as CantidadActividadesFinalizadas) / 
((SELECT COUNT(*) FROM AccionesRecomendada WHERE idOrdenCompra = 'OC001') as CantidadActividades) as PorcentajeCompletado;

CREATE INDEX idx_acciones_idorden_estado ON AccionesRecomendada(idOrdenCompra, Estado);
 ```
## Consulta Detallada de Servicio:
 ```sql
SELECT NombreServicio, FechaIncio, FechaFin, Costo, TecnicoAsignado, EstadoServicio, NombreConsumible, NombreRespuesto
FROM Servicio;

SELECT NombreRespuesto FROM Respuesto WHERE idServicio = 'SER001';
SELECT NombreConsumible FROM Cosnumible WHERE idServicio = 'SER001';
SELECT IdAccionRecomendad FROM AccionRecomendad WHERE idOrdenCompra = 'OCP001';

CREATE INDEX idx_servicio_id ON Servicio(idServicio);
CREATE INDEX idx_respuesto_idservicio ON Respuesto(IdServicio);
CREATE INDEX idx_consumible_idservicio ON Cosnumible(IdServicio);
CREATE INDEX idx_accionrecomendada_idorden ON AccionRecomendada(idOrdenCompra);
 ```
**Antes**

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/0d5ea2c0-673c-4de6-afe4-af8d53c30a58)

**Despues**

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/c89f5331-6fb3-4687-8041-6c847912c248)

