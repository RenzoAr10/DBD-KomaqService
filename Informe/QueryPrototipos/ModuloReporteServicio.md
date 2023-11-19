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
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/92390fd5-0967-4eb8-a3c0-aae638fe608f)


--Se reliza un busqueda con los campos en los cuales estan completados , por ello se usa %% al darle al boton BUSCAR
```sql
SELECT idServicio , NombreServicio , IdOrdenCompra, NombreUsuario
FROM Servicio as S
INNER JOIN OrdenCompra as cp ON s. IdOrdenCompra= cp. IdOrdenCompra
INNER JOIN NombreUsuario as un ON s.nombreUsuario= un.nombreUsusario;
WHERE nombreServicio = nombrex AND OrdenCompra =%OC00x% AND NombreCliente=%nombreclientex%;
-- Al seleccionar un Servicio se abre una ventana Deatallando más aspectos de este, basado en su IdServicio
```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/fd5e8281-d0e9-4eac-974f-0d893b4c4c93)

```sql
SELECT NombreServicio , FechaIncio , FechaFin , Costo, TecnicoAsignado , NombreConsumible, NombreRespuesto
From Servicio
SELECT NombreRespuesto FROM Respuesto WHERE idServicio = SER001;
SELECT NombreConsumible FROM Cosnumible WHERE idServicio = SER001; 
```
