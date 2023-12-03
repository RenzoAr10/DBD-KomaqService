## TABLAS
 
 ```sql
CREATE TABLE Cliente (
	id_cliente SERIAL PRIMARY KEY,
	nombre VARCHAR(50),
	apellido_paterno VARCHAR(50),
	apellido_materno VARCHAR(50),
	RUC INTEGER,
	dni VARCHAR(15),
	telefono INTEGER,
	email VARCHAR(100),
	direccion VARCHAR(255),
	NombreEmpresa VARCHAR(50)
);

CREATE TABLE OrdenCompra (
	id_orden_compra SERIAL PRIMARY KEY,
	estado_oc VARCHAR(100),        
	fecha_oc VARCHAR(100),
        id_usuario SERIAL,
        FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

CREATE TABLE Usuario (
	id_usuario SERIAL PRIMARY KEY,
	nombre_usuario VARCHAR(50),
	contrasena_usuario VARCHAR(50),
	id_cliente SERIAL,
	id_orden_compra SERIAL,
	FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente),
);
	
CREATE TABLE Empleado (
	id_empleado SERIAL PRIMARY KEY,
	nombre VARCHAR(50),
	apellido_paterno VARCHAR(50),
	apellido_materno VARCHAR(50),
	dni VARCHAR(15),
	telefono INTEGER,
	email VARCHAR(100),
	especializacion VARCHAR(100),
	cargo VARCHAR(255),
	id_jefe SERIAL,
    FOREIGN KEY (id_jefe) REFERENCES Empleado(id_empleado)
);


CREATE TABLE Factura (
	id_factura SERIAL PRIMARY KEY,
	forma_pago VARCHAR(100),
	fecha_emision VARCHAR(100),
	costo_total DECIMAL(8,2),
        id_usuario SERIAL,
        FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

CREATE TABLE Servicio (
	id_servicio SERIAL PRIMARY KEY,
	nombre_servicio VARCHAR(100),
	fecha_inicio DATE,
	fecha_fin DATE,
	costo DECIMAL(8,2),
	cantidad_servicios INT,
	subtotal_servicios DECIMAL(8,2),
	tecnico_asignado VARCHAR(100),
	id_orden_compra SERIAL,
	id_factura SERIAL,
	FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra),
	FOREIGN KEY (id_factura) REFERENCES Factura(id_factura)
);

CREATE TABLE NomUsuario (
	id_nomusuario SERIAL PRIMARY KEY,
	nombre_usuario VARCHAR(50),
    contrasena_usuario VARCHAR(50),
	id_empleado SERIAL,
	id_servicio SERIAL,
    FOREIGN KEY (id_empleado) REFERENCES Empleado(id_empleado),
	FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio)
);

	
CREATE TABLE Maquina (
	id_maquina SERIAL PRIMARY KEY,
	nombre_maquina VARCHAR(100),
	modelo VARCHAR(100),
	combustible VARCHAR(100),
	motor VARCHAR(100),
	serie_motor VARCHAR(100),
	id_orden_compra SERIAL,
	FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra)
);


CREATE TABLE Problemas (
	id_problema SERIAL PRIMARY KEY,
	tipo_problema VARCHAR(100),
	modelo VARCHAR(100),
	id_maquina SERIAL,
	FOREIGN KEY (id_maquina) REFERENCES Maquina(id_maquina)
);

CREATE TABLE Consumible (
	id_consumible SERIAL PRIMARY KEY,
	nombre_consumible VARCHAR(100),
	fecha_uso DATE,
	cantidad INT,
	costo DECIMAL(8,2),
	id_servicio SERIAL,
	FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio)
);

CREATE TABLE Repuesto (
	id_repuesto SERIAL PRIMARY KEY,
	stock INT,
	precio INT,
	cantidad INT,
	subtotal_repuesto INT,
	id_servicio SERIAL,
	id_factura SERIAL,
        nombrerepuesto VARCHAR(50),
	FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio),
	FOREIGN KEY (id_factura) REFERENCES Factura(id_factura)
);
   
CREATE TABLE Proveedor (
	id_proveedor SERIAL PRIMARY KEY,
	nombre_empresa VARCHAR(100),
	telefono_prov INTEGER,
	direccion_prov VARCHAR(100),
	email VARCHAR(50)
);

CREATE TABLE Proveedor_Repuesto (
    id_proveedor SERIAL,
    id_repuesto SERIAL,
    PRIMARY KEY (id_proveedor, id_repuesto),
    FOREIGN KEY (id_proveedor) REFERENCES Proveedor(id_proveedor),
    FOREIGN KEY (id_repuesto) REFERENCES Repuesto(id_repuesto)
);

CREATE TABLE AccionRecomendada (
    id_accion SERIAL PRIMARY KEY,
	nombre_accion VARCHAR(70),
	costo_asociado DECIMAL(8,2),
	id_orden_compra SERIAL,
	FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra)
);

 ```
## INSERCION DE VALORES
 ```sql
-- TABLA CLIENTE
INSERT INTO Cliente (id_cliente, nombre, apellido_paterno, apellido_materno, RUC, dni, telefono, email, direccion, NombreEmpresa)
VALUES
   ('CL001', 'Juan', 'Gomez', 'Perez', 12345678901, '70123456', 975977906, 'juan.gomez@email.com', 'Av. Principal 123, Lima', 'Mminera las bambas s.a.'),
   ('CL002', 'Ana', 'Rodriguez', 'Lopez', 19876543210, '71234567', 912345678, 'ana.rodriguez@email.com', 'Jr. Las Flores 456, Arequipa', 'Compañia minera poderosa s.a.'),
   ('CL003', 'Carlos', 'Diaz', 'Cordova', 17654321098, '72345678', 934567890, 'carlos.diaz@email.com', 'Calle Central 789, Trujillo', 'Minera yanacocha s.r.l.'),
   ('CL004', 'Laura', 'Ramirez', 'Mendoza', 19987654321, '73456789', 945678901, 'laura.ramirez@email.com', 'Av. Independencia 012, Chiclayo', 'Volcan compañía minera s.a.a.'),
   ('CL005', 'Pedro', 'Martinez', 'Santos', 11234567890, '74567890', 956789012, 'pedro.martinez@email.com', 'Jr. Amazonas 345, Huancayo', 'Compañia minera ares s.a.c.'),
   ('CL006', 'Luisa', 'Garcia', 'Flores', 19876543210, '75678901', 967890123, 'luisa.garcia@email.com', 'Av. El Sol 678, Iquitos', 'Nexa resources peru'),
   ('CL007', 'Roberto', 'Sanchez', 'Torres', 12345678901, '76789012', 978901234, 'roberto.sanchez@email.com', 'Calle Primavera 901, Piura', 'Shougang hierro peru s.a.a.'),
   ('CL008', 'Elena', 'Fernandez', 'Luna', 11234567890, '77890123', 989012345, 'elena.fernandez@email.com', 'Jr. Los Pinos 234, Cusco', 'Anglo american quellaveco s.a.'),
   ('CL009', 'Javier', 'Hernandez', 'Luna', 11234567890, '78901234', 990123456, 'javier.hernandez@email.com', 'Av. Las Palmeras 567, Ayacucho', 'Marcobre s.a.c.'),
   ('CL010', 'Carmen', 'Jimenez', 'Cruz', 12345678901, '79012345', 911234567, 'carmen.jimenez@email.com', 'Calle Victoria 890, Tacna', 'Minera chinalco peru s.a.');


-- TABLA USUARIO
INSERT INTO Usuario (id_usuario, nombre_usuario, contrasena_usuario, id_cliente, id_orden_compra) VALUES
('US001', 'jcustodio', 'password1', 'CL001', 'OC001'),
('US002', 'hrojas', 'password2', 'CL002', 'OC002'),
('US003', 'jcotrina', 'password3', 'CL003', 'OC003'),
('US004', 'gcampos', 'password4', 'CL004', 'OC004'),
('US005', 'lramirez', 'password5', 'CL005', 'OC005');

-- TABLA EMPLEADO
INSERT INTO Empleado (id_empleado, nombre, apellido_paterno, apellido_materno, dni, telefono, email, especializacion, cargo, id_jefe) VALUES
('EMP001', 'Hector', 'Rojas', '', '12345678', '987654321', 'hrojas@komq.com', 'Mecánico', 'Técnico Senior', NULL),
('EMP002', 'Jefferson', 'Cotrina', '', '87654321', '987650123', 'jcotrina@komq.com', 'Mecánico', 'Técnico Junior', 'EMP001'),
('EMP003', 'Gabriel', 'Campos', '', '23456789', '987651234', 'gcampos@komq.com', 'Logística', 'Gerente de Operaciones', NULL),
('EMP004', 'Lucia', 'Ramirez', '', '34567890', '987652345', 'lramirez@komq.com', 'Administración', 'Asistente de Gerencia', 'EMP003'),
('EMP005', 'Carlos', 'Gonzales', '', '45678901', '987653456', 'cgonzales@komq.com', 'Mecánico', 'Especialista de Campo', 'EMP001');

-- TABLA MAQUINA
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ001', 'Telehandler Manitou', 'MT-X 1030', 'Diésel', 'Perkins 1104D-44TA', 'U31540B', 'US001');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ002', 'Cargador Frontal Cat', 'CAT 980K', 'Diésel', 'Cat C13 ACERT', 'X3C1234B', 'US002');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ003', 'Excavadora Komatsu', 'PC350LC-8', 'Diésel', 'Komatsu SAA6D114E-3', 'KOMEX1234', 'US003');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ004', 'Montacargas Hyster', 'H50FT', 'Gas LP', 'Hyster H5.0FT', 'HYSTF12345', 'US004');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ005', 'Retroexcavadora JCB', '3CX 14', 'Diésel', 'JCB EcoMax T4', 'JCB3CX4045', 'US005');

-- TABLA ORDEN DE COMPRA
INSERT INTO OrdenCompra (id_orden_compra, fecha_orden) VALUES
('OC001', 'Finalizado', '2023-04-20'),
('OC002', 'En proceso', '2023-04-21'),
('OC003', 'En proceso', '2023-04-22'),
('OC004', 'Finalizado', '2023-04-23'),
('OC005', 'Finalizado', '2023-04-24');

-- TABLA PROBLEMAS
INSERT INTO Problemas (id_problema, tipo_problema, modelo, id_maquina) VALUES
('PROB001', 'Fallo del sistema hidráulico', 'MT-X 1030', 'MAQ001'),
('PROB002', 'Desgaste de neumáticos', 'CAT 980M', 'MAQ002'),
('PROB003', 'Problemas de arranque en frío', 'ZX350LC-6', 'MAQ003'),
('PROB004', 'Fallo en la transmisión', '3CX', 'MAQ004'),
('PROB005', 'Sobrecalentamiento del motor', 'H60FT', 'MAQ005');

-- TABLA SERVICIO
INSERT INTO Servicio (id_servicio, nombre_servicio, fecha_inicio, fecha_fin, costo, cantidad_servicios, subtotal_servicios, tecnico_asignado, id_orden_compra, id_factura) VALUES
('SERV001', 'Mantenimiento Preventivo', '2023-04-20', '2023-04-21', 500, 1, 500, 'Hector Rojas', 'OC001', 'FAC001'),
('SERV002', 'Reparación del Sistema Hidráulico', '2023-04-22', '2023-04-23', 1200, 2, 2400, 'Jefferson Cotrina', 'OC002', 'FAC002'),
('SERV003', 'Cambio de Neumáticos', '2023-04-24', '2023-04-25', 300, 4, 1200, 'Gabriel Campos', 'OC003', 'FAC003'),
('SERV004', 'Servicio de Transmisión', '2023-04-26', '2023-04-27', 800, 1, 800, 'Lucia Ramirez', 'OC004', 'FAC004'),
('SERV005', 'Inspección Técnica', '2023-04-28', '2023-04-29', 200, 3, 600, 'Carlos Gonzales', 'OC005', 'FAC005');

-- TABLA FACTURA
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC001', 'Tarjeta de Crédito', '2023-11-17', 1000);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC002', 'Efectivo', '2023-11-18', 500);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC003', 'Transferencia Bancaria', '2023-11-19', 750);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC004', 'Pago Móvil', '2023-11-20', 1250);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC005', 'Cheque', '2023-11-21', 3000);

-- TABLA CONSUMIBLE
INSERT INTO Consumible (id_consumible, nombre_consumible, fecha_uso, cantidad, costo, id_servicio) VALUES
('CONS001', 'Aceite Hidráulico', '2023-04-20', 10, 50, 'SERV001'),
('CONS002', 'Filtro de Aire', '2023-04-22', 5, 30, 'SERV002'),
('CONS003', 'Neumáticos', '2023-04-24', 4, 300, 'SERV003'),
('CONS004', 'Aceite de Transmisión', '2023-04-26', 20, 40, 'SERV004'),
('CONS005', 'Batería', '2023-04-28', 2, 100, 'SERV005');

-- TABLA REPUESTO
INSERT INTO Repuesto (id_repuesto, stock, precio, cantidad, subtotal_repuesto, id_servicio, id_factura,nombrerepuesto) VALUES
('REP001', 15, 100, 1, 100, 'SERV001', 'FAC001','Llave de arranque'),
('REP002', 10, 250, 2, 500, 'SERV002', 'FAC002','Llave maestra'),
('REP003', 20, 150, 4, 600, 'SERV003', 'FAC003','Cilendro hidraulico de inclinacion'),
('REP004', 5, 300, 1, 300, 'SERV004', 'FAC004','Motor hidraulico de traslacion original'),
('REP005', 8, 200, 3, 600, 'SERV005', 'FAC005','Turbocompresor'	);

-- TABLA PROVEEDOR
INSERT INTO Proveedor (id_proveedor, nombre_empresa, telefono_prov, direccion_prov, email) VALUES
('PROV001', 'Ferreyros', '01 712 3000', 'Av. Arequipa 1067, Lima, Perú', 'contacto@ferreyros.com'),
('PROV002', 'Repuestos Maquinaria Pesada - Mining Corp.', '999 123 456', 'Av. Los Próceres 123, San Juan de Lurigancho, Perú', 'ventas@miningcorp.com'),
('PROV003', 'GC SERVICE & PARTS SAC', '999 687 090', 'Av. Universitaria 123, San Martín de Porres, Perú', 'ventas@gcserparts.com'),
('PROV004', 'M.LL.V. Ventas y Servicios Empresariales', '(01) 523 7420', 'Av. Los Olivos 123, Los Olivos, Perú', 'ventas@mllv.com'),
('PROV005', 'Técnica Repuestos', '987 654 321', 'Av. Panamericana Norte 123, Callao, Perú', 'ventas@tecnicarepuestos.com');

-- TABLA PROVEEDORREPUESTO
INSERT INTO Proveedor_Repuesto (id_proveedor, id_repuesto ) VALUES
('PROV001', 'REP001'),
('PROV001', 'REP002'),
('PROV001', 'REP003'),
('PROV002', 'REP004'),
('PROV003', 'REP004');

-- TABLA ACCION RECOMENDADA
INSERT INTO AccionRecomendada (id_accion, nombre_accion, costo_asociado, id_orden_compra)
VALUES
  ('ACC001', 'Lavado de cada componente', 600, 'OC003'),
  ('ACC002', 'Reemplazo y Armado de piñón de ataque', 1200, 'OC003'),
  ('ACC003', 'Montaje de eje propulsor', 800, 'OC004'),
  ('ACC004', 'Armado del housing de pistón de freno Lh y Rh', 700, 'OC004'),
  ('ACC005', 'Reemplazo de resortes y pernos de pistón de servicio', 550, 'OC005'),
  ('ACC006', 'Reemplazo de tapa de bocamasa', 900, 'OC005'),
  ('ACC007', 'Montaje de fundas', 600, 'OC002'),
  ('ACC008', 'Reemplazo de bocina de bocamasa', 550, 'OC002'),
  ('ACC009', 'Reemplazo de reten, rodajes y pistas de bocamasa (Mandos finales)', 1000, 'OC005'),
  ('ACC010', 'Reemplazo de pernos de tapa de bocamasa', 700, 'OC001'),
  ('ACC011', 'Armado de diferencial', 1100, 'OC003'),
  ('ACC012', 'Se midió juego de Backlash', 600, 'OC003'),
  ('ACC013', 'Montaje de tapa de cubos reductores', 800, 'OC004'),
  ('ACC014', 'Reemplazo de todos los o-ring', 500, 'OC004'),
  ('ACC015', 'Metalización de eje propulsor', 700, 'OC004'),
  ('ACC016', 'Reemplazo de bocinas de tapas de bocamasa', 550, 'OC005'),
  ('ACC017', 'Reemplazo de 4 arandelas de los espárragos', 600, 'OC005'),
  ('ACC018', 'Reemplazo de respiradero', 650, 'OC005'),
  ('ACC019', 'Montaje de housing de freno Lh y Rh', 750, 'OC004'),
  ('ACC020', 'Se verificó pisada de los dientes de piñón de ataque y la corona', 900, 'OC004');

```


