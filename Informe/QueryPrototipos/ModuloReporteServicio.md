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

AJUSTE DE INDICES

```sql
-- Índices en las claves foráneas
CREATE INDEX idx_servicio_id_orden_compra ON Servicio(id_orden_compra);
CREATE INDEX idx_servicio_id_factura ON Servicio(id_factura);
CREATE INDEX idx_consumible_id_servicio ON Consumible(id_servicio);
CREATE INDEX idx_respuesto_id_servicio ON Respuesto(IdServicio);

-- Índice en las columnas utilizadas en búsquedas por texto
CREATE INDEX idx_servicio_nombre ON Servicio(nombre_servicio);

 --Índices para Consultas de Porcentaje de Actividades Completadas:
CREATE INDEX idx_acciones_orden_compra_estado ON AccionesRecomendada(idOrdenCompra, Estado);

```
