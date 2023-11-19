R01001 R01002

PR01001

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/24255496-932a-490a-83ff-701b7602dbd9)
```sql
SELECT *
FROM Usuarios
WHERE nombreUsuario = @user1 AND contrasenaUsuario = @pass1;
```

R01003

PR01002

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/969f03f9-3019-411e-b4fa-ad67c435cb57)
```sql
--Al presionar el boton Registrar
INSERT INTO Usuario (nombreUsuario, contraseñaUsuario , IdCliente)
VALUES (‘hrojas’, ‘password2’ , ‘CL002’)
INSERT INTO Cliente (id_cliente, nombre, apellido_paterno, apellido_materno, RUC, dni, telefono, email, direccion, NombreEmpresa)
VALUES
  ('CL002', 'Ana', 'Rodriguez', 'Lopez', 19876543210, '71234567', 912345678, 'ana.rodriguez@email.com', 'Jr. Las Flores 456, Arequipa', 'Compañia minera poderosa s.a.'),
```

R01004

PR01003

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/d49ed786-4f8c-427e-a0d9-6a3e7ed4159b)
```sql
SELECT *
FROM Usuarios
WHERE nombreUsuario = @user2 AND contrasenaUsuario = @pass2;
```

R01005

PR01004

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/e5f3c62f-ca80-4b80-a9f0-df9146ad3783)
```sql
--Al presionar el botón REGISTRAR
INSERT INTO Usuario (nombreUsuario, contraseñaUsuario , IdEmpleado)
VALUES (‘jcustodio’ , ‘password1’, ‘EMP001’)

INSERT INTO Empleado (id_empleado, nombre, apellido_paterno, apellido_materno, dni, telefono, email, especializacion, cargo, id_jefe) VALUES
('EMP001', 'Hector', 'Rojas', 'Cotrina', '12345678', '987654321', 'hrojas@komq.com', 'Mecánico', 'Técnico Senior', NULL),
```
PRO02001

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
R03001 R03002 R03003

PR03001

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/df96d4f8-bcfe-4c7a-b1ee-f30b68563a14)
```sql
INSERT INTO Servicio (id_servicio, nombre_servicio, fecha_inicio, tecnico_asignado, id_orden_compra, id_factura) 
VALUES ('SERV001', 'Reparación de motor', '2023-04-15', 'Juan Pérez', 'OC123', 'FAC456');

```

R03004

PR03002

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/545fba8f-899a-4344-b45a-1f2de1e94130)
```sql
SELECT id_solicitud, estado_revision, fecha_revision, detalles
FROM EstadoServicios
WHERE usuario_id = 'id_del_cliente';
```

R03005

PR03003

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/54ca6118-eee3-4200-8678-fc18cbb19b30)
```sql
INSERT INTO Comentarios (id_servicio, comentario, fecha_comentario, usuario_id) 
VALUES ('SOL002', 'El servicio fue excelente y en tiempo.', CURRENT_DATE, 'usuario_cliente');
```


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
# PRO4001
## R05001 R05002 R05003 R05004
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/1eb93670-40b8-4d35-a902-30d46bf98abb)



```sql
SELECT IdEmpelado, nombreEmpleado 
FROM empleado;
SELECT IdRepuesto , NombreRepuesto
FROM Respuesto;
--Insertar los valores al darle al boton
INSERT INTO Servicio (id_servicio, nombre_servicio, fecha_inicio, fecha_fin, costo, cantidad_servicios, subtotal_servicios, tecnico_asignado, id_orden_compra, id_factura) 
VALUES
('SERV001', 'Mantenimiento Preventivo', '2023-04-20', '2023-04-21', 500, 1, 500, 'Hector Rojas', 'OC001', 'FAC001'),
INSERT INTO Consumible (id_consumible, nombre_consumible, fecha_uso, cantidad, costo, id_servicio) VALUES
('CONS001', 'neumático', '2023-04-20', 10, 80, 'SERV001'),
('CONS003', 'Batería', '2023-04-20', 2, 340, 'SERV001');
INSERT INTO Respuesto ( NombreRespuesto, CantidadUtilizada, IdServicio)
VALUES ('REP002', '17', ' SERV001')
VALUES ('REP004', '21', 'SERV001')

```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/a7e137f9-0211-472e-8cad-efb7f5fdc91a)



--Se reliza un busqueda con los campos en los cuales estan completados , por ello se usa %% al darle al boton BUSCAR
```sql
SELECT idServicio , NombreServicio , IdOrdenCompra, NombreUsuario 
FROM Servicio as S
INNER JOIN OrdenCompra as cp ON s. IdOrdenCompra= cp. IdOrdenCompra
INNER JOIN NombreUsuario as un ON s.nombreUsuario= un.nombreUsusario;
WHERE nombreServicio = nombrex AND OrdenCompra =%OC00x% AND NombreCliente=%nombreclientex%;
-- Se genera el porcentaje de activades compeltadas , para esto los estados de cada actidades son definidos , es decir solo hay una lista disponible de estados  lo caules son INCOMPLETA y COMPLETADO
((SELECT COUNT(*) FROM AccionesRecomendada WHERE idOrdenCompra= 'OC001' and Estado='COMPLETADO') as CantidadActividadesFinalizadas) / ((SELECT COUNT(*) FROM AccionesRecomendada WHERE idOrdenCompra= 'OC001' ) as CantidadActividades) as PorcentajeCompletado;
-- Al seleccionar un Servicio se abre una ventana Deatallando más aspectos de este, basado en su IdServicio


```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/c06eecc7-7289-4dd5-be15-d99f328dcf76)



```sql
SELECT NombreServicio , FechaIncio , FechaFin , Costo, TecnicoAsignado, EstadoServicio , NombreConsumible, NombreRespuesto
From Servicio
SELECT NombreRespuesto FROM Respuesto WHERE idServicio = SER001;
SELECT NombreConsumible FROM Cosnumible WHERE idServicio = SER001;
SELECT IdAccionRecomendad FROM AccionRecomendad WHERE idOrdenCompra= OCP001;
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

