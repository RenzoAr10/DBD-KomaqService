
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


AJUSTE DE INDICES

```sql

--Mas que todo recomendacion en caso de  eliminar un índice de clave primaria, no se hace a menos que se este rediseñando cómo se manejan las claves en la base de datos

--Eliminar indices
DROP INDEX IF EXISTS idx_factura_id_factura ON factura;
DROP INDEX IF EXISTS idx_servicio_id_factura ON servicio;
DROP INDEX IF EXISTS idx_repuesto_id_factura ON repuesto;

-- Ejemplo de índice filtrado para registros activos en una tabla de facturas
CREATE INDEX idx_factura_activa ON factura (id_factura) WHERE estado = 'Activa';

-- Ejemplo de índice compuesto basado en el id de factura y otra columna comúnmente usada
CREATE INDEX idx_factura_composite ON factura (id_factura, otra_columna);

-- Los índices estan en las columnas utilizadas en las cláusulas JOIN
CREATE INDEX idx_servicio_join ON servicio (id_factura, id_otro_campo);

-- Reconstruir un índice
ALTER INDEX idx_factura_id_factura ON factura REBUILD;

-- Actualizar estadísticas
UPDATE STATISTICS factura idx_factura_id_factura;

 ```

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






![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/c06eecc7-7289-4dd5-be15-d99f328dcf76)

## Consulta con JOIN y Filtros:
 ```sql
SELECT 
    S.id_servicio AS idServicio,
    S.nombre_servicio AS NombreServicio,
    cp.id_orden_compra AS IdOrdenCompra,
    un.nombre_usuario AS NombreUsuario
FROM 
    Servicio AS S
    INNER JOIN OrdenCompra AS cp ON S.id_orden_compra = cp.id_orden_compra
    INNER JOIN NomUsuario AS un ON S.tecnico_asignado = un.nombre_usuario
WHERE 
    S.nombre_servicio = 'nombrex'
    AND cp.id_orden_compra = 'OC00x'
    AND NombreUsuario = 'nombreclientex';

CREATE INDEX idx_servicio_idorden ON Servicio(id_orden_compra);
CREATE INDEX idx_servicio_nombre ON Servicio(nombre_servicio);
CREATE INDEX idx_ordencompra_id ON OrdenCompra(Id_orden_Compra);
CREATE INDEX idx_nombreusuario_nombre ON NombreUsuario(nombre_ususario);
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


```sql

--Mas que todo recomendacion en caso de  eliminar un índice de clave primaria, no se hace a menos que se este rediseñando cómo se manejan las claves en la base de datos

--Eliminar indices
DROP INDEX idx_nombreempresa ON cliente;

-- si SE quiere indexar clientes activos
CREATE INDEX idx_nombreempresa_active ON cliente(nombreempresa)
WHERE estado = 'Activo';


-- crear un índice compuesto que incluya ambas columnas : nombreempresa y  id_cliente
CREATE INDEX idx_nombreempresa_idcliente ON cliente(nombreempresa, id_cliente);


-- Si un índice se ha fragmentado mucho con el tiempo, se reconstruye para mejorar el rendimiento
ALTER INDEX idx_nombreempresa ON cliente REBUILD;


-- Reconstruir un índice
ALTER INDEX idx_factura_id_factura ON factura REBUILD;

-- Actualizar estadísticas
UPDATE STATISTICS cliente idx_nombreempresa;


 ```
# Informe de Gestion Ordenes de Compra
![GestiónOC v2](https://github.com/RenzoAr10/DBD-KomaqService/assets/144966624/416dec14-824e-4bfd-85eb-06db51b5ba18)


 ```sql
SELECT
   OC.id_orden_compra,
   OC.fecha_oc,
   OC.estado_oc,
   S.cantidad_servicios,
   CONCAT(C.apellido_paterno, ' ', C.apellido_materno, ' ', C.nombre) AS nombre_cliente,
   P.nombre_empresa AS Proveedor,
   F.costo_total
FROM OrdenCompra OC
JOIN  Usuario U ON OC.id_orden_compra =U.id_orden_compra
JOIN  Cliente C ON U.id_cliente = C.id_cliente
JOIN  Servicio S ON OC.id_orden_compra = S.id_orden_compra
JOIN  Repuesto R ON R.id_servicio = S.id_servicio
JOIN  Proveedor_Repuesto PR ON R.id_repuesto = PR.id_repuesto
JOIN  Proveedor P ON PR.id_proveedor = P.id_proveedor
LEFT JOIN  Factura F ON S.id_factura = F.id_factura;
```

```sql
CREATE INDEX idx_nombre_cliente
ON (
    SELECT
        OC.id_orden_compra,
        OC.fecha_oc,
        OC.estado_oc,
        S.cantidad_servicios,
        CONCAT(C.apellido_paterno, ' ', C.apellido_materno, ' ', C.nombre) AS nombre_cliente,
        P.nombre_empresa AS proveedor,
        F.costo_total
    FROM
        OrdenCompra OC
    JOIN
        Usuario U ON OC.id_orden_compra = U.id_orden_compra
    JOIN
        Cliente C ON U.id_cliente = C.id_cliente
    JOIN
        Servicio S ON OC.id_orden_compra = S.id_orden_compra
    JOIN
        Repuesto R ON R.id_servicio = S.id_servicio
    JOIN
        Proveedor_Repuesto PR ON R.id_repuesto = PR.id_repuesto
    JOIN
        Proveedor P ON PR.id_proveedor = P.id_proveedor
    LEFT JOIN
        Factura F ON S.id_factura = F.id_factura
);
```
Antes

![OCantes01](https://github.com/RenzoAr10/DBD-KomaqService/assets/144966624/0ca59574-8f3b-4afb-9f82-c1d1007342e1)


Después

![OCdespues01](https://github.com/RenzoAr10/DBD-KomaqService/assets/144966624/e24b82f9-c1ca-4285-97b7-bcfffdb3972e)
