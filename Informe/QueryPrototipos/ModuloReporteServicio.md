![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/6b03ba47-295c-4780-b4d3-baae4c427932)


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
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/c16fc45e-5645-48c1-9b7a-8c8962f86b73)

```sql
SELECT idServicio , NombreServicio , IdOrdenCompra, NombreUsuario
FROM Servicio as S
INNER JOIN OrdenCompra as cp ON s. IdOrdenCompra= cp. IdOrdenCompra
INNER JOIN NombreUsuario as un ON s.nombreUsuario= un.nombreUsusario;
-- Al seleccionar un Servicio se abre una ventana Deatallando más aspectos de este, basado en su IdServicio
```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/d01fe164-f115-43e5-943e-d4bdfea671c4)
```sql
SELECT NombreServicio , FechaIncio , FechaFin , Costo, TecnicoAsignado , NombreConsumible, NombreRespuesto
From Servicio
SELECT NombreRespuesto FROM Respuesto WHERE idServicio = SER001;
SELECT NombreConsumible FROM Cosnumible WHERE idServicio = SER001; 
```
