## TABLAS
 
 ```sql
CREATE TABLE Cliente (
	id_cliente VARCHAR(10) PRIMARY KEY,
	nombre VARCHAR(50),
    apellido_paterno VARCHAR(50),
	apellido_materno VARCHAR(50),
	RUC INT,
	dni VARCHAR(15),
	telefono INT,
	email VARCHAR(100),
	direccion VARCHAR(255)
);

CREATE TABLE Usuario (
	id_usuario VARCHAR(10) PRIMARY KEY,
	nombre_usuario VARCHAR(50),
    contrasena_usuario VARCHAR(50),
	id_cliente VARCHAR(10),
	id_orden_compra VARCHAR(10),
	FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente),
	FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra)
);
	
CREATE TABLE Empleado (
	id_empleado VARCHAR(10) PRIMARY KEY,
	nombre VARCHAR(50),
    apellido_paterno VARCHAR(50),
	apellido_materno VARCHAR(50),
	dni VARCHAR(15),
	telefono INT,
	email VARCHAR(100),
	especializacion VARCHAR(100),
	cargo VARCHAR(255),
	id_jefe VARCHAR(10),
    FOREIGN KEY (id_jefe) REFERENCES Empleado(id_empleado)
);

CREATE TABLE NomUsuario (
	id_nomusuario VARCHAR(10) PRIMARY KEY,
	nombre_usuario VARCHAR(50),
    contrasena_usuario VARCHAR(50),
	id_empleado VARCHAR(10),
	id_servicio VARCHAR(10),
    FOREIGN KEY (id_empleado) REFERENCES Empleado(id_empleado),
	FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio)
);

	
CREATE TABLE Maquina (
	id_maquina VARCHAR(10) PRIMARY KEY,
	nombre_maquina VARCHAR(100),
	modelo VARCHAR(100),
	combustible VARCHAR(100),
	motor VARCHAR(100),
	serie_motor VARCHAR(100),
	id_usuario VARCHAR(10),
	FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

CREATE TABLE OrdenCompra (
	id_orden_compra VARCHAR(10) PRIMARY KEY,
	fecha_orden VARCHAR(100)
);

CREATE TABLE Problemas (
	id_problema VARCHAR(10) PRIMARY KEY,
	tipo_problema VARCHAR(100),
	modelo VARCHAR(100),
	id_maquina VARCHAR(10),
	FOREIGN KEY (id_maquina) REFERENCES Maquina(id_maquina)
);
-- Modelo 2 veces?

CREATE TABLE Servicio (
	id_servicio VARCHAR(10) PRIMARY KEY,
	nombre_servicio VARCHAR(100),
	fecha_inicio DATE,
	fecha_fin DATE,
	costo INT,
	cantidad_servicios INT,
	subtotal_servicios INT,
	tecnico_asignado VARCHAR(100),
	id_orden_compra VARCHAR(10),
	id_factura VARCHAR(10),
	FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra),
	FOREIGN KEY (id_factura) REFERENCES Factura(id_factura)
);

CREATE TABLE Factura (
	id_factura VARCHAR(10) PRIMARY KEY,
	forma_pago VARCHAR(100),
	fecha_emision VARCHAR(100),
	costo_total INT
);

CREATE TABLE Consumible (
	id_consumible VARCHAR(10) PRIMARY KEY,
	nombre_consumible VARCHAR(100),
	fecha_uso DATE,
	cantidad INT,
	costo INT,
	id_servicio VARCHAR(10),
	FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio)
);

CREATE TABLE Repuesto (
	id_repuesto VARCHAR(10) PRIMARY KEY,
	stock INT,
	precio INT,
	cantidad INT,
	subtotal_repuesto INT,
	id_servicio VARCHAR(10),
	id_factura VARCHAR(10),
	FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio),
	FOREIGN KEY (id_factura) REFERENCES Factura(id_factura)
);
   
CREATE TABLE Proveedor (
	id_proveedor VARCHAR(10) PRIMARY KEY,
	nombre_empresa VARCHAR(10),
	telefono_prov INT,
	direccion_prov INT,
	email VARCHAR(10)
);

CREATE TABLE Proveedor_Repuesto (
    id_proveedor VARCHAR(10),
    id_repuesto VARCHAR(10),
    PRIMARY KEY (id_proveedor, id_repuesto),
    FOREIGN KEY (id_proveedor) REFERENCES Proveedor(id_proveedor),
    FOREIGN KEY (id_repuesto) REFERENCES Repuesto(id_repuesto)
);

CREATE TABLE AccionRecomendada (
    id_accion VARCHAR(10) PRIMARY KEY,
	nombre_accion VARCHAR(10),
	costo_asociado INT,
	id_orden_compra VARCHAR(10),
	FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra)
);

 ```
## INSERCION DE VALORES
 ```
--TABLA CLIENTE
INSERT INTO Cliente (id_cliente, nombre, apellido_paterno, apellido_materno, RUC, dni, telefono, email, direccion) VALUES
('CL001', 'Empresa', 'Andina', '', 20123456789, '12345678', 987654321, 'contacto@andina.com', 'Av. Industrial 123'),
('CL002', 'Servicios', 'Industriales', 'Garcia', 20123456780, '87654321', 987650123, 'info@servind.com', 'Calle Comercio 456'),
('CL003', 'Construcciones', 'Rojas', 'S.A.', 20123456781, '23456789', 987651234, 'ventas@rojascons.com', 'Av. Los Constructores 789'),
('CL004', 'Agro', 'Campo', 'Lopez', 20123456782, '34567890', 987652345, 'soporte@agrocampo.com', 'Av. Agricultura 012'),
('CL005', 'Textiles', 'Morales', 'EIRL', 20123456783, '45678901', 987653456, 'admin@textmor.com', 'Jr. Algodón 345');

--TABLA USUARIO
INSERT INTO Usuario (id_usuario, nombre_usuario, contrasena_usuario, id_cliente, id_orden_compra) VALUES
('US001', 'jcustodio', 'password1', 'CL001', 'OC001'),
('US002', 'hrojas', 'password2', 'CL002', 'OC002'),
('US003', 'jcotrina', 'password3', 'CL003', 'OC003'),
('US004', 'gcampos', 'password4', 'CL004', 'OC004'),
('US005', 'lramirez', 'password5', 'CL005', 'OC005');

--TABLA EMPLEADO
INSERT INTO Empleado (id_empleado, nombre, apellido_paterno, apellido_materno, dni, telefono, email, especializacion, cargo, id_jefe) VALUES
('EMP001', 'Hector', 'Rojas', '', '12345678', 987654321, 'hrojas@komq.com', 'Mecánico', 'Técnico Senior', NULL),
('EMP002', 'Jefferson', 'Cotrina', '', '87654321', 987650123, 'jcotrina@komq.com', 'Mecánico', 'Técnico Junior', 'EMP001'),
('EMP003', 'Gabriel', 'Campos', '', '23456789', 987651234, 'gcampos@komq.com', 'Logística', 'Gerente de Operaciones', NULL),
('EMP004', 'Lucia', 'Ramirez', '', '34567890', 987652345, 'lramirez@komq.com', 'Administración', 'Asistente de Gerencia', 'EMP003'),
('EMP005', 'Carlos', 'Gonzales', '', '45678901', 987653456, 'cgonzales@komq.com', 'Mecánico', 'Especialista de Campo', 'EMP001');

--TABLA MAQUINA
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ001', 'Telehandler Manitou', 'MT-X 1030', 'Diésel', 'Perkins 1104D-44TA', 'U31540B', 'USR001');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ002', 'Cargador Frontal Cat', 'CAT 980K', 'Diésel', 'Cat C13 ACERT', 'X3C1234B', 'USR002');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ003', 'Excavadora Komatsu', 'PC350LC-8', 'Diésel', 'Komatsu SAA6D114E-3', 'KOMEX1234', 'USR003');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ004', 'Montacargas Hyster', 'H50FT', 'Gas LP', 'Hyster H5.0FT', 'HYSTF12345', 'USR004');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ005', 'Retroexcavadora JCB', '3CX 14', 'Diésel', 'JCB EcoMax T4', 'JCB3CX4045', 'USR005');

--TABLA ORDEN DE COMPRA
INSERT INTO OrdenCompra (id_orden_compra, fecha_orden) VALUES
('OC001', '2023-04-20'),
('OC002', '2023-04-21'),
('OC003', '2023-04-22'),
('OC004', '2023-04-23'),
('OC005', '2023-04-24');

--TABLA PROBLEMAS
INSERT INTO Problemas (id_problema, tipo_problema, modelo, id_maquina) VALUES
('PROB001', 'Fallo del sistema hidráulico', 'MT-X 1030', 'MAQ001'),
('PROB002', 'Desgaste de neumáticos', 'CAT 980M', 'MAQ002'),
('PROB003', 'Problemas de arranque en frío', 'ZX350LC-6', 'MAQ003'),
('PROB004', 'Fallo en la transmisión', '3CX', 'MAQ004'),
('PROB005', 'Sobrecalentamiento del motor', 'H60FT', 'MAQ005');


--TABLA SERVICIO
INSERT INTO Servicio (id_servicio, nombre_servicio, fecha_inicio, fecha_fin, costo, cantidad_servicios, subtotal_servicios, tecnico_asignado, id_orden_compra, id_factura) VALUES
('SERV001', 'Mantenimiento Preventivo', '2023-04-20', '2023-04-21', 500, 1, 500, 'Hector Rojas', 'OC001', 'FAC001'),
('SERV002', 'Reparación del Sistema Hidráulico', '2023-04-22', '2023-04-23', 1200, 2, 2400, 'Jefferson Cotrina', 'OC002', 'FAC002'),
('SERV003', 'Cambio de Neumáticos', '2023-04-24', '2023-04-25', 300, 4, 1200, 'Gabriel Campos', 'OC003', 'FAC003'),
('SERV004', 'Servicio de Transmisión', '2023-04-26', '2023-04-27', 800, 1, 800, 'Lucia Ramirez', 'OC004', 'FAC004'),
('SERV005', 'Inspección Técnica', '2023-04-28', '2023-04-29', 200, 3, 600, 'Carlos Gonzales', 'OC005', 'FAC005');


--TABLA FACTURA
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC001', 'Tarjeta de Crédito', '2023-11-17', 1000);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC002', 'Efectivo', '2023-11-18', 500);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC003', 'Transferencia Bancaria', '2023-11-19', 750);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC004', 'Pago Móvil', '2023-11-20', 1250);
INSERT INTO Factura (id_factura, forma_pago, fecha_emision, costo_total) VALUES ('FAC005', 'Cheque', '2023-11-21', 3000);

--TABLA CONSUMIBLE
INSERT INTO Consumible (id_consumible, nombre_consumible, fecha_uso, cantidad, costo, id_servicio) VALUES
('CONS001', 'Aceite Hidráulico', '2023-04-20', 10, 50, 'SERV001'),
('CONS002', 'Filtro de Aire', '2023-04-22', 5, 30, 'SERV002'),
('CONS003', 'Neumáticos', '2023-04-24', 4, 300, 'SERV003'),
('CONS004', 'Aceite de Transmisión', '2023-04-26', 20, 40, 'SERV004'),
('CONS005', 'Batería', '2023-04-28', 2, 100, 'SERV005');

--TABLA REPUESTO
INSERT INTO Repuesto (id_repuesto, stock, precio, cantidad, subtotal_repuesto, id_servicio, id_factura) VALUES
('REP001', 15, 100, 1, 100, 'SERV001', 'FAC001'),
('REP002', 10, 250, 2, 500, 'SERV002', 'FAC002'),
('REP003', 20, 150, 4, 600, 'SERV003', 'FAC003'),
('REP004', 5, 300, 1, 300, 'SERV004', 'FAC004'),
('REP005', 8, 200, 3, 600, 'SERV005', 'FAC005');

--TABLA PROVEEDOR
INSERT INTO Proveedor (id_proveedor, nombre_empresa, telefono_prov, direccion_prov, email) VALUES
('PROV001', 'Proveedora A', 123456789, 123, 'contacto@proveedora.com'),
('PROV002', 'Proveedora B', 987654321, 456, 'ventas@proveedora.com'),
('PROV003', 'Proveedora C', 123123123, 789, 'soporte@proveedora.com'),
('PROV004', 'Proveedora D', 321321321, 012, 'info@proveedora.com'),
('PROV005', 'Proveedora E', 654654654, 345, 'admin@proveedora.com');

--TABLA PROVEEDORREPUESTO
INSERT INTO Proveedor (id_proveedor, nombre_empresa, telefono_prov, direccion_prov, email) VALUES
('PROV001', 'Proveedora A', 123456789, 123, 'contacto@proveedora.com'),
('PROV002', 'Proveedora B', 987654321, 456, 'ventas@proveedora.com'),
('PROV003', 'Proveedora C', 123123123, 789, 'soporte@proveedora.com'),
('PROV004', 'Proveedora D', 321321321, 012, 'info@proveedora.com'),
('PROV005', 'Proveedora E', 654654654, 345, 'admin@proveedora.com');

--TABLA ACCION RECOMENDADA
INSERT INTO AccionRecomendada (id_accion, nombre_accion, costo_asociado, id_orden_compra) VALUES
('ACC001', 'Ajuste', 50, 'OC001'),
('ACC002', 'Revisión', 0, 'OC002'),
('ACC003', 'Sustitución', 150, 'OC003'),
('ACC004', 'Reparación', 300, 'OC004'),
('ACC005', 'Mantenimiento', 200, 'OC005');
```


