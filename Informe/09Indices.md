#INDICES PRO 003 
##Consulta de Empleados y Repuestos:
 ```sql
SELECT IdEmpleado, NombreEmpleado FROM Empleado;
SELECT IdRepuesto, NombreRepuesto FROM Repuesto;

CREATE INDEX idx_empleado_id ON Empleado(IdEmpleado);
CREATE INDEX idx_repuesto_id ON Repuesto(IdRepuesto);

 ```
##Consulta con JOIN y Filtros:
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

##Cálculo de Porcentaje de Actividades Completadas:
 ```sql
((SELECT COUNT(*) FROM AccionesRecomendada WHERE idOrdenCompra = 'OC001' and Estado = 'COMPLETADO') as CantidadActividadesFinalizadas) / 
((SELECT COUNT(*) FROM AccionesRecomendada WHERE idOrdenCompra = 'OC001') as CantidadActividades) as PorcentajeCompletado;

CREATE INDEX idx_acciones_idorden_estado ON AccionesRecomendada(idOrdenCompra, Estado);
 ```
##Consulta Detallada de Servicio:
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
