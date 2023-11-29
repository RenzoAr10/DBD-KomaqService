# INDICES PRO 003 
##Consulta de Empleados y Repuestos:
 ```sql
SELECT IdEmpleado, NombreEmpleado FROM Empleado;
SELECT IdRepuesto, NombreRepuesto FROM Repuesto;

CREATE INDEX idx_empleado_id ON Empleado(IdEmpleado);
CREATE INDEX idx_repuesto_id ON Repuesto(IdRepuesto);

 ```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/4d19b946-7214-4e2c-917c-6958b882a136)

 Despues de crear los indices
 

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/be9ae2dc-c704-4813-b20b-50d038872479)


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
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/c369dfa0-e560-411c-a51c-c4e40acc3203)


![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/72f60bf7-8632-40b0-ac6f-51ae96f80486)


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

# Facturacion y Pagos

**PRO6002**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/e71deff2e181024cac1d58c5e07b5a90572862f1/Documentacion%20de%20Soporte/querys/FacturacionYPagos/vistaFactura.png)

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
-- Crear un índice en la columna nombreempresa de la tabla cliente
CREATE INDEX idx_nombreempresa ON cliente (nombreempresa);
```

