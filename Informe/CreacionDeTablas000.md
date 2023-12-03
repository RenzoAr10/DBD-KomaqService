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
	FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
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
    id_usuario SERIAL,
    FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);


CREATE TABLE MaquinaOrdenCompra (
    id_relacion SERIAL PRIMARY KEY,
    id_maquina INT,
    id_orden_compra INT,
    FOREIGN KEY (id_maquina) REFERENCES Maquina(id_maquina),
    FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra)
);



CREATE TABLE Problemas (
	id_problema SERIAL PRIMARY KEY,
	nombre_problema VARCHAR(100)

);
CREATE TABLE ProblemaMaquina (
    id_relacion SERIAL PRIMARY KEY,
    id_problema INT,
    id_maquina INT,
    FOREIGN KEY (id_problema) REFERENCES Problemas(id_problema),
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
INSERT INTO Cliente (nombre, apellido_paterno, apellido_materno, RUC, dni, telefono, email, direccion, NombreEmpresa)
VALUES
  ('Juan', 'Gomez', 'Perez', 12345678901, '70123456', 975977906, 'juan.gomez@email.com', 'Av. Principal 123, Lima', 'Mminera las bambas s.a.'),
  ('Ana', 'Rodriguez', 'Lopez', 19876543210, '71234567', 912345678, 'ana.rodriguez@email.com', 'Jr. Las Flores 456, Arequipa', 'Compañia minera poderosa s.a.'),
  ('Carlos', 'Diaz', 'Cordova', 17654321098, '72345678', 934567890, 'carlos.diaz@email.com', 'Calle Central 789, Trujillo', 'Minera yanacocha s.r.l.'),
  ('Laura', 'Ramirez', 'Mendoza', 19987654321, '73456789', 945678901, 'laura.ramirez@email.com', 'Av. Independencia 012, Chiclayo', 'Volcan compañía minera s.a.a.'),
  ('Pedro', 'Martinez', 'Santos', 11234567890, '74567890', 956789012, 'pedro.martinez@email.com', 'Jr. Amazonas 345, Huancayo', 'Compañia minera ares s.a.c.'),
  ('Luisa', 'Garcia', 'Flores', 19876543210, '75678901', 967890123, 'luisa.garcia@email.com', 'Av. El Sol 678, Iquitos', 'Nexa resources peru'),
  ('Roberto', 'Sanchez', 'Torres', 12345678901, '76789012', 978901234, 'roberto.sanchez@email.com', 'Calle Primavera 901, Piura', 'Shougang hierro peru s.a.a.'),
  ('Elena', 'Fernandez', 'Luna', 11234567890, '77890123', 989012345, 'elena.fernandez@email.com', 'Jr. Los Pinos 234, Cusco', 'Anglo american quellaveco s.a.'),
  ('Javier', 'Hernandez', 'Luna', 11234567890, '78901234', 990123456, 'javier.hernandez@email.com', 'Av. Las Palmeras 567, Ayacucho', 'Marcobre s.a.c.'),
  ('Carmen', 'Jimenez', 'Cruz', 12345678901, '79012345', 911234567, 'carmen.jimenez@email.com', 'Calle Victoria 890, Tacna', 'Minera chinalco peru s.a.'),
  ('María', 'Lopez', 'Gonzalez', 98765432109, '80123456', 923456789, 'maria.lopez@email.com', 'Av. Libertad 567, Lima', 'Minera San Jorge S.A.C.'),
  ('Alejandro', 'Torres', 'Martinez', 87654321098, '81234567', 934567890, 'alejandro.torres@email.com', 'Jr. Los Pinos 123, Arequipa', 'Inversiones Mineras del Sur S.A.'),
  ('Sofía', 'Gutierrez', 'Paredes', 76543210987, '82345678', 945678901, 'sofia.gutierrez@email.com', 'Calle Sol 789, Trujillo', 'Minería Moderna S.R.L.'),
  ('Gabriel', 'Mendoza', 'Salazar', 65432109876, '83456789', 956789012, 'gabriel.mendoza@email.com', 'Av. Primavera 012, Chiclayo', 'Minerales del Norte S.A.A.'),
  ('Valentina', 'Cruz', 'Herrera', 54321098765, '84567890', 967890123, 'valentina.cruz@email.com', 'Jr. Los Olivos 345, Huancayo', 'Inversiones Mineras del Centro S.A.C.'),
  ('Lucas', 'Castro', 'Silva', 87654321098, '85678901', 978901234, 'lucas.castro@email.com', 'Calle Azul 678, Iquitos', 'Minerales del Amazonas'),
  ('Camila', 'Flores', 'Diaz', 98765432109, '86789012', 989012345, 'camila.flores@email.com', 'Av. Las Palmeras 901, Piura', 'Minera San Miguel S.A.A.'),
  ('Matías', 'Santos', 'Vega', 65432109876, '87890123', 990123456, 'matias.santos@email.com', 'Jr. Los Alamos 234, Cusco', 'Exploraciones Mineras del Sur S.A.C.'),
  ('Isabella', 'Perez', 'Gomez', 65432109876, '88901234', 911234567, 'isabella.perez@email.com', 'Av. Los Pinos 567, Ayacucho', 'Minería del Futuro S.A.C.'),
  ('Martín', 'Hernandez', 'Fernandez', 98765432109, '89012345', 922345678, 'martin.hernandez@email.com', 'Calle Sucre 890, Tacna', 'Minerales del Perú S.A.C.'),
  ('Mariano', 'Jimenez', 'Cabrera', 12345678901, '90123456', 933456789, 'mariano.jimenez@email.com', 'Jr. Arequipa 345, Lima', 'Minerales del Norte S.A.C.'),
  ('Valeria', 'Garcia', 'Mendez', 19876543210, '91234567', 944567890, 'valeria.garcia@email.com', 'Av. Grau 678, Arequipa', 'Minería Moderna S.R.L.'),
  ('Nicolás', 'Martinez', 'Rios', 17654321098, '92345678', 955678901, 'nicolas.martinez@email.com', 'Calle Luna 012, Trujillo', 'Minerales del Centro S.A.A.'),
  ('Martina', 'Diaz', 'Torres', 19987654321, '93456789', 966789012, 'martina.diaz@email.com', 'Jr. Los Laureles 123, Chiclayo', 'Minería del Futuro S.A.C.'),
  ('Ignacio', 'Ramirez', 'Cruz', 11234567890, '94567890', 977890123, 'ignacio.ramirez@email.com', 'Av. Los Robles 456, Huancayo', 'Minera San Miguel S.A.A.'),
  ('Renata', 'Fernandez', 'Luna', 19876543210, '95678901', 988901234, 'renata.fernandez@email.com', 'Calle Sol 789, Iquitos', 'Minerales del Amazonas'),
  ('Santiago', 'Sanchez', 'Mendoza', 12345678901, '96789012', 999012345, 'santiago.sanchez@email.com', 'Av. Las Flores 901, Piura', 'Inversiones Mineras del Sur S.A.C.'),
  ('Delfina', 'Lopez', 'Silva', 11234567890, '97890123', 900123456, 'delfina.lopez@email.com', 'Jr. Los Pinos 234, Cusco', 'Minera San Jorge S.A.C.'),
  ('Facundo', 'Gutierrez', 'Diaz', 11234567890, '98901234', 911234567, 'facundo.gutierrez@email.com', 'Av. Los Olivos 567, Ayacucho', 'Minerales del Norte S.A.A.'),
  ('Antonella', 'Castro', 'Herrera', 12345678901, '99012345', 922345678, 'antonella.castro@email.com', 'Calle Azul 890, Tacna', 'Exploraciones Mineras del Sur S.A.C.');


-- TABLA USUARIO
INSERT INTO Usuario (nombre_usuario, contrasena_usuario, id_cliente) VALUES
('jgomez', 'password1', 1),
('arodriguez', 'password2', 2),
('cdiaz', 'password3', 3),
('lramirez', 'password4', 4),
('pmartinez', 'password5', 5),
('lgarcia', 'password6', 6),
('rsanchez', 'password7', 7),
('efernandez', 'password8', 8),
('jhernandez', 'password9', 9),
('cjimenez', 'password10', 10),
('mlopez', 'password11', 11),
('atorres', 'password12', 12),
('sgutierrez', 'password13', 13),
('gmendoza', 'password14', 14),
('vcruz', 'password15', 15),
('lcastro', 'password16', 16),
('lsilva', 'password17', 17),
('mrios', 'password18', 18),
('vdiaz', 'password19', 19),
('lgonzalez', 'password20', 20),
('cfernandez', 'password21', 21),
('srios', 'password22', 22),
('tdiaz', 'password23', 23),
('mcruz', 'password24', 24),
('iramirez', 'password25', 25);


-- TABLA ORDEN DE COMPRA
INSERT INTO OrdenCompra (estado_oc, fecha_oc, id_usuario) VALUES
  ('Finalizado', '2023-04-20', 14),
  ('En proceso', '2023-04-21', 3),
  ('En proceso', '2023-04-22', 8),
  ('Finalizado', '2023-04-23', 5),
  ('Finalizado', '2023-04-24', 20),
  ('Finalizado', '2023-05-01', 10),
  ('En proceso', '2023-05-02', 18),
  ('En proceso', '2023-05-03', 12),
  ('Finalizado', '2023-05-04', 7),
  ('Finalizado', '2023-05-05', 25),
  ('En proceso', '2023-05-06', 1),
  ('En proceso', '2023-05-07', 16),
  ('Finalizado', '2023-05-08', 22),
  ('Finalizado', '2023-05-09', 9),
  ('En proceso', '2023-05-10', 2),
  ('En proceso', '2023-05-11', 19),
  ('Finalizado', '2023-05-12', 15),
  ('Finalizado', '2023-05-13', 11),
  ('En proceso', '2023-05-14', 6),
  ('En proceso', '2023-05-15', 13),
  ('Finalizado', '2023-05-16', 24),
  ('Finalizado', '2023-05-17', 17),
  ('En proceso', '2023-05-18', 21),
  ('En proceso', '2023-05-19', 23),
  ('Finalizado', '2023-05-20', 4),
  ('Finalizado', '2023-05-21', 8),
  ('En proceso', '2023-05-22', 14),
  ('En proceso', '2023-05-23', 7),
  ('Finalizado', '2023-05-24', 16),
  ('Finalizado', '2023-05-25', 5),
  ('En proceso', '2023-05-26', 12),
  ('En proceso', '2023-05-27', 2),
  ('Finalizado', '2023-05-28', 18),
  ('Finalizado', '2023-05-29', 10),
  ('En proceso', '2023-05-30', 22),
  ('En proceso', '2023-05-31', 9),
  ('Finalizado', '2023-06-01', 1),
  ('Finalizado', '2023-06-02', 25),
  ('En proceso', '2023-06-03', 6),
  ('En proceso', '2023-06-04', 13),
  ('Finalizado', '2023-06-05', 19),
  ('Finalizado', '2023-06-06', 15);


-- TABLA EMPLEADO

INSERT INTO Empleado (nombre, apellido_paterno, apellido_materno, dni, telefono, email, especializacion, cargo, id_jefe) VALUES
--Jefes
('Hector', 'Rojas', 'Gomez', '12345678', '987654321', 'hrojas@komq.com', 'Mecánico', 'Jefe de Departamento', NULL),
('Jefferson', 'Cotrina', 'Lopez', '87654321', '987650123', 'jcotrina@komq.com', 'Mecánico', 'Jefe de Equipo', NULL),
('Gabriel', 'Campos', 'Diaz', '23456789', '987651234', 'gcampos@komq.com', 'Logística', 'Gerente General', NULL),
('Lucia', 'Ramirez', 'Martinez', '34567890', '987652345', 'lramirez@komq.com', 'Administración', 'Directora de Operaciones', NULL),
('Carlos', 'Gonzales', 'Lopez', '45678901', '987653456', 'cgonzales@komq.com', 'Mecánico', 'Jefe de Área', NULL);
--Otros empleados
('Luis', 'Martinez', 'Sanchez', '56789012', '987654322', 'lmartinez@komq.com', 'Mecánico', 'Técnico Senior', 1),
('Alejandra', 'Lopez', 'Gomez', '67890123', '987650124', 'alopez@komq.com', 'Mecánico', 'Técnico Junior', 2),
('Diego', 'Hernandez', 'Ramirez', '78901234', '987651235', 'dhernandez@komq.com', 'Logística', 'Gerente de Operaciones', 3),
('Fernanda', 'Santos', 'Cotrina', '89012345', '987652346', 'fsantos@komq.com', 'Administración', 'Asistente de Gerencia', 4),
('Ana', 'Ramirez', 'Gonzales', '90123456', '987653457', 'aramirez@komq.com', 'Mecánico', 'Especialista de Campo', 1),
('Pablo', 'Gutierrez', 'Sanchez', '12345432', '987654323', 'pgutierrez@komq.com', 'Mecánico', 'Técnico Senior', 1),
('Elena', 'Castro', 'Lopez', '23454543', '987650125', 'ecastro@komq.com', 'Mecánico', 'Técnico Junior', 2),
('Martín', 'Fernandez', 'Hernandez', '34565432', '987651236', 'mfernandez@komq.com', 'Logística', 'Gerente de Operaciones', 3),
('Lorena', 'Diaz', 'Santos', '45654321', '987652347', 'ldiaz@komq.com', 'Administración', 'Asistente de Gerencia', 4),
('Raúl', 'Sanchez', 'Cotrina', '56765432', '987653458', 'rsanchez@komq.com', 'Mecánico', 'Especialista de Campo', 1),
('Patricia', 'Martinez', 'Gutierrez', '67876543', '987654324', 'pmartinez@komq.com', 'Mecánico', 'Técnico Senior', 5),
('Miguel', 'Lopez', 'Castro', '78987654', '987650126', 'mlopez@komq.com', 'Mecánico', 'Técnico Junior', 2),
('Laura', 'Hernandez', 'Fernandez', '89098765', '987651237', 'lhernandez@komq.com', 'Logística', 'Gerente de Operaciones', 3),
('Gonzalo', 'Santos', 'Diaz', '90109876', '987652348', 'gsantos@komq.com', 'Administración', 'Asistente de Gerencia', 5),
('Valeria', 'Ramirez', 'Sanchez', '98765401', '987653459', 'vramirez@komq.com', 'Mecánico', 'Especialista de Campo', 5),
('Roberto', 'Gutierrez', 'Gomez', '10234567', '987654325', 'rgutierrez@komq.com', 'Mecánico', 'Técnico Senior', 5),
('Cecilia', 'Castro', 'Lopez', '11223344', '987650127', 'ccastro@komq.com', 'Mecánico', 'Técnico Junior', 2),
('Jorge', 'Fernandez', 'Hernandez', '44556677', '987651238', 'jfernandez@komq.com', 'Logística', 'Gerente de Operaciones', 3),
('Marina', 'Diaz', 'Santos', '55667788', '987652349', 'mdiaz@komq.com', 'Administración', 'Asistente de Gerencia', 4),
('Oscar', 'Sanchez', 'Cotrina', '66778899', '987653450', 'osanchez@komq.com', 'Mecánico', 'Especialista de Campo', 1),
('Evelyn', 'Ramirez', 'Gutierrez', '77889900', '987654331', 'eramirez@komq.com', 'Mecánico', 'Técnico Senior', 1),
('Ricardo', 'Lopez', 'Castro', '88990011', '987650132', 'rlopez@komq.com', 'Mecánico', 'Técnico Junior', 2),
('Isabel', 'Hernandez', 'Fernandez', '99001122', '987651243', 'ihernandez@komq.com', 'Logística', 'Gerente de Operaciones', 3),
('Pedro', 'Santos', 'Diaz', '00112233', '987652354', 'psantos@komq.com', 'Administración', 'Asistente de Gerencia', 4),
('Carmen', 'Ramirez', 'Sanchez', '11223344', '987653465', 'cramirez@komq.com', 'Mecánico', 'Especialista de Campo', 1);

-- TABLA MAQUINA
INSERT INTO Maquina (nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES
    ('Manipulador Telescópico', 'MT-X 1030', 'Diésel', 'Perkins 1104D-44TA', 'U31540B', 15),
    ('Cargador Frontal Caterpillar', 'CAT 980K', 'Diésel', 'Cat C13 ACERT', 'X3C1234B', 12),
    ('Excavadora Komatsu PC350', 'PC350LC-8', 'Diésel', 'Komatsu SAA6D114E-3', 'KOMEX1234', 7),
    ('Montacargas Hyster H50FT', 'H50FT', 'Gas LP', 'Hyster H5.0FT', 'HYSTF12345', 3),
    ('Retroexcavadora JCB 3CX', '3CX 14', 'Diésel', 'JCB EcoMax T4', 'JCB3CX4045', 22),
    ('Excavadora Hitachi ZX210LC', 'ZX210LC', 'Diésel', 'Isuzu AI-4HK1XYSS', 'HITZX210123', 5),
    ('Bulldozer Caterpillar D6', 'D6', 'Diésel', 'Cat C9.3 ACERT', 'CATD612345', 8),
    ('Grúa Liebherr LTM 1200-5.1', 'LTM 1200-5.1', 'Diésel', 'Liebherr D934S A6', 'LIEBHERR1200', 11),
    ('Palas Eléctricas P&H 4100XPC', '4100XPC', 'Eléctrico', 'ABB AC1600SD', 'PH4100XPC789', 14),
    ('Tractor John Deere 8335R', '8335R', 'Diésel', 'John Deere 9.0L 6-cyl', 'JD8335R123', 17),
    ('Excavadora Volvo EC350E', 'EC350E', 'Diésel', 'Volvo D8J', 'VOLVOEC350E567', 20),
    ('Cargadora Compacta Bobcat S650', 'S650', 'Diésel', 'Bobcat D24NAP', 'BOBCATS650890', 23),
    ('Motoniveladora Caterpillar 140M', '140M', 'Diésel', 'Cat C7 ACERT', 'CAT140M456', 22),
    ('Compactadora Bomag BW120AD-5', 'BW120AD-5', 'Diésel', 'Kubota D1703-M-E3', 'BOMAGBW120AD', 29),
    ('Excavadora Case CX350D', 'CX350D', 'Diésel', 'FPT 6.7L', 'CASECX350D123', 2);
   ('Cargador Frontal Volvo', 'L120H', 'Diésel', 'Volvo D8J', 'VOLVOL120H456', 17),
   ('Compactadora Hamm HD+ 120i VO', 'HD+ 120i VO', 'Diésel', 'Kubota V3800', 'HAMMHD120I789', 6),
   ('Excavadora Caterpillar 320', '320GC', 'Diésel', 'Cat C4.4 ACERT', 'CAT320GC789', 20),
   ('Bulldozer Dressta TD-14M Extra', 'TD-14M Extra', 'Diésel', 'Cummins QSL9', 'DRESSTATD14M789', 11),
   ('Grúa Terex RT555-1', 'RT555-1', 'Diésel', 'Cummins QSB 6.7L', 'TEREXRT555123', 23),
   ('Compactadora Dynapac CA2500PD', 'CA2500PD', 'Diésel', 'Cummins B3.3', 'DYNAPACCA2500', 4),
   ('Motoniveladora Komatsu GD555-5', 'GD555-5', 'Diésel', 'Komatsu SAA6D107E-1', 'KOMGD555678', 8),
   ('Cargador Frontal Case 721G', '721G', 'Diésel', 'FPT 6.7L', 'CASE721G123', 1),
   ('Retroexcavadora Case 590SN', '590SN', 'Diésel', 'FPT 3.4L', 'CASE590SN456', 25),
   ('Tractor New Holland T7.315', 'T7.315', 'Diésel', 'FPT 6.7L', 'NH315123', 15),
   ('Palas Eléctricas Hitachi EX5600-7', 'EX5600-7', 'Eléctrico', 'ABB AC Drive', 'HITACHIEX5600', 7),
   ('Cargadora Compacta Gehl R135', 'R135', 'Diésel', 'Yanmar 4TNV98C', 'GEHLR135789', 18),
   ('Excavadora Hyundai R220LC-9S', 'R220LC-9S', 'Diésel', 'Cummins B5.9-C', 'HYUNDAIR220123', 2),
   ('Retroexcavadora JCB 3CX Eco', '3CX Eco', 'Diésel', 'JCB EcoMax T4F', 'JCBEco123', 16),
   ('Motoniveladora CAT 140K', '140K', 'Diésel', 'Cat C7.1 ACERT', 'CAT140K456', 12),
   ('Grúa Grove GMK6300L-1', 'GMK6300L-1', 'Diésel', 'Mercedes-Benz OM471LA', 'GROVEGMK6300', 21),
   ('Bulldozer John Deere 850K', '850K', 'Diésel', 'John Deere 6068H', 'JD850K789', 10),
   ('Excavadora Doosan DX225LC-5', 'DX225LC-5', 'Diésel', 'Doosan DL06', 'DOOSANDX225567', 3),
   ('Cargadora Compacta Kubota SSV75', 'SSV75', 'Diésel', 'Kubota V3307', 'KUBOTASSV75890', 24),
   ('Tractor Massey Ferguson 7719S', '7719S', 'Diésel', 'AGCO Power 4.9L', 'MF7719S456', 14),
   ('Excavadora Takeuchi TB240', 'TB240', 'Diésel', 'Yanmar 4TNV86', 'TAKEUCHITB240123', 9),
   ('Excavadora Kobelco SK350LC-10', 'SK350LC-10', 'Diésel', 'HINO J05E', 'KOBELCOSK350567', 13),
   ('Palas Eléctricas Caterpillar 7495 HF', '7495 HF', 'Eléctrico', 'ABB AC Drive', 'CAT7495HF789', 22),
   ('Excavadora Kubota U55-4', 'U55-4', 'Diésel', 'Kubota V2403', 'KUBOTAU55456', 5);



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


