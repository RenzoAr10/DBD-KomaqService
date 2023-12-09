## TABLAS
 
 ```sql
CREATE TABLE Cliente (
   id_cliente VARCHAR(20) PRIMARY KEY,
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
   id_orden_compra VARCHAR(20) PRIMARY KEY,
   estado_oc VARCHAR(100),
   fecha_oc DATE
);

CREATE TABLE MaquinaOrdenCompra (
   id_relacion VARCHAR(20) PRIMARY KEY,
   id_maquina VARCHAR(20),
   id_orden_compra VARCHAR(20),
   FOREIGN KEY (id_maquina) REFERENCES Maquina(id_maquina),
   FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra)
);

CREATE TABLE Usuario (
   id_usuario VARCHAR(20) PRIMARY KEY,
   nombre_usuario VARCHAR(50),
   contrasena_usuario VARCHAR(50),
   id_cliente VARCHAR(20),
   FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);

CREATE TABLE Empleado (
   id_empleado VARCHAR(20) PRIMARY KEY,
   nombre VARCHAR(50),
   apellido_paterno VARCHAR(50),
   apellido_materno VARCHAR(50),
   dni VARCHAR(15),
   telefono INTEGER,
   email VARCHAR(100),
   especializacion VARCHAR(100),
   cargo VARCHAR(255),
   id_jefe VARCHAR(20),
   FOREIGN KEY (id_jefe) REFERENCES Empleado(id_empleado)
);

CREATE TABLE NomUsuario (
   id_nomusuario VARCHAR(20) PRIMARY KEY,
   nombre_usuario VARCHAR(50),
   contrasena_usuario VARCHAR(50),
   id_empleado VARCHAR(20),
   id_servicio VARCHAR(20),
   FOREIGN KEY (id_empleado) REFERENCES Empleado(id_empleado),
   FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio)
);

CREATE TABLE Factura (
   id_factura VARCHAR(20) PRIMARY KEY,
   forma_pago VARCHAR(100),
   fecha_emision DATE,
   costo_total DECIMAL(8,2),
   id_usuario VARCHAR(20),
   FOREIGN KEY (id_usuario) REFERENCES Usuario(id_usuario)
);

CREATE TABLE Servicio (
   id_servicio VARCHAR(20) PRIMARY KEY,
   nombre_servicio VARCHAR(100),
   fecha_inicio DATE,
   fecha_fin DATE,
   costo DECIMAL(8,2),
   cantidad_servicios INT,
   subtotal_servicios DECIMAL(8,2),
   id_orden_compra VARCHAR(20),
   id_factura VARCHAR(20),
   id_nomusuario VARCHAR(20),
   FOREIGN KEY (id_orden_compra) REFERENCES OrdenCompra(id_orden_compra),
   FOREIGN KEY (id_factura) REFERENCES Factura(id_factura),
   FOREIGN KEY (id_nomusuario) REFERENCES NomUsuario(id_nomusuario)
);

CREATE TABLE Maquina (
   id_maquina VARCHAR(20) PRIMARY KEY,
   nombre_maquina VARCHAR(100),
   modelo VARCHAR(100),
   combustible VARCHAR(100),
   motor VARCHAR(100),
   serie_motor VARCHAR(100)
);

CREATE TABLE ProblemaMaquina (
   id_relacion VARCHAR(20) PRIMARY KEY,
   id_problema VARCHAR(20),
   id_maquina VARCHAR(20),
   FOREIGN KEY (id_problema) REFERENCES Problemas(id_problema),
   FOREIGN KEY (id_maquina) REFERENCES Maquina(id_maquina)
);

CREATE TABLE Problemas (
   id_problema VARCHAR(20) PRIMARY KEY,
   nombre_problema VARCHAR(100)
);

CREATE TABLE Consumible (
   id_consumible VARCHAR(20) PRIMARY KEY,
   nombre_consumible VARCHAR(100),
   fecha_uso DATE,
   cantidad INT,
   costo DECIMAL(8,2),
   id_servicio VARCHAR(20),
   FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio)
);

CREATE TABLE Repuesto (
   id_repuesto VARCHAR(20) PRIMARY KEY,
   nombrerepuesto VARCHAR(50),
   stock INT,
   precio INT,
   cantidad INT,
   subtotal_repuesto INT,
   id_servicio VARCHAR(20),
   id_factura VARCHAR(20),
   FOREIGN KEY (id_servicio) REFERENCES Servicio(id_servicio),
   FOREIGN KEY (id_factura) REFERENCES Factura(id_factura)
);

CREATE TABLE Proveedor (
   id_proveedor VARCHAR(20) PRIMARY KEY,
   nombre_empresa VARCHAR(100),
   telefono_prov INTEGER,
   direccion_prov VARCHAR(100),
   email VARCHAR(50)
);

CREATE TABLE Proveedor_Repuesto (
   id_proveedor VARCHAR(20),
   id_repuesto VARCHAR(20),
   PRIMARY KEY (id_proveedor, id_repuesto),
   FOREIGN KEY (id_proveedor) REFERENCES Proveedor(id_proveedor),
   FOREIGN KEY (id_repuesto) REFERENCES Repuesto(id_repuesto)
);

CREATE TABLE AccionRecomendada (
   id_accion VARCHAR(20) PRIMARY KEY,
   nombre_accion VARCHAR(70),
   costo_asociado DECIMAL(8,2),
   id_orden_compra VARCHAR(20),
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


INSERT INTO NomUsuario (nombre_usuario, contrasena_usuario, id_empleado) VALUES
('hrojas', 'contrasena1', 1),
('jcotrina', 'contrasena2', 2),
('gcampos', 'contrasena3', 3),
('lramirez', 'contrasena4', 4),
('cgonzales', 'contrasena5', 5),
('lmartinez', 'contrasena6', 6),
('alopez', 'contrasena7', 7),
('dhernandez', 'contrasena8', 8),
('fsantos', 'contrasena9', 9),
('aramirez', 'contrasena10', 10),
('pgutierrez', 'contrasena11', 11),
('ecastro', 'contrasena12', 12),
('mfernandez', 'contrasena13', 13),
('ldiaz', 'contrasena14', 14),
('rsanchez', 'contrasena15', 15),
('pmartinez', 'contrasena16', 16),
('mlopez', 'contrasena17', 17),
('lhernandez', 'contrasena18', 18),
('gsantos', 'contrasena19', 19),
('vramirez', 'contrasena20', 20),
('rgutierrez', 'contrasena21', 21),
('ccastro', 'contrasena22', 22),
('jfernandez', 'contrasena23', 23),
('mdiaz', 'contrasena24', 24),
('osanchez', 'contrasena25', 25),
('eramirez', 'contrasena26', 26),
('rlopez', 'contrasena27', 27),
('ihernandez', 'contrasena28', 28),
('psantos', 'contrasena29', 29),
('cramirez', 'contrasena30', 30),
('hrojas', 'contrasena31', 31),
('jcotrina', 'contrasena32', 32),
('gcampos', 'contrasena33', 33),
('lramirez', 'contrasena34', 34),
('cgonzales', 'contrasena35', 35),
('lmartinez', 'contrasena36', 36);


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
INSERT INTO Problemas (tipo_problema, id_maquina) VALUES
   ('Fallo del sistema hidráulico', 1),
   ('Problema en el motor', 2),
   ('Fugas de aceite', 3),
   ('Sobrecalentamiento', 4),
   ('Mal funcionamiento de la transmisión', 5),
   ('Problema eléctrico', 6),
   ('Desgaste excesivo de las llantas', 7),
   ('Problema en el sistema de dirección', 8),
   ('Batería descargada', 9),
   ('Problema en el sistema de frenos', 10),
   ('Desgaste prematuro de las cuchillas', 11),
   ('Fallo en el sistema neumático', 12),
   ('Problema en el sistema de combustible', 13),
   ('Ruido anormal en el motor', 14),
   ('Problema en el sistema de elevación', 15),
   ('Desgaste en los componentes del tren de rodaje', 16),
   ('Problema en el sistema de carga', 17),
   ('Vibraciones inusuales', 18),
   ('Problema en el sistema de iluminación', 19),
   ('Fallo en el sistema de refrigeración', 20),
   ('Problema en el sistema hidrostático', 21),
   ('Desgaste en los dientes de la excavadora', 22),
   ('Problema en el sistema de escape', 23),
   ('Falla en el sistema de seguridad', 24),
   ('Problema en el sistema de tracción', 25),
   ('Fallo del sistema hidráulico', 26),
   ('Problema en el motor', 27),
   ('Fugas de aceite', 28),
   ('Sobrecalentamiento', 29),
   ('Mal funcionamiento de la transmisión', 30),
   ('Problema eléctrico', 31),
   ('Desgaste excesivo de las llantas', 32),
   ('Problema en el sistema de dirección', 33),
   ('Batería descargada', 34),
   ('Problema en el sistema de frenos', 35),
   ('Desgaste prematuro de las cuchillas', 36),
   ('Fallo en el sistema neumático', 37),
   ('Problema en el sistema de combustible', 38),
   ('Ruido anormal en el motor', 39);


-- TABLA FACTURA
INSERT INTO Factura (forma_pago, fecha_emision, costo_total, id_usuario) VALUES
   ('Tarjeta de Crédito', '2023-04-20', 150, 14),
   ('Efectivo', '2023-04-21', 1200, 3),
   ('Transferencia Bancaria', '2023-04-22', 500, 8),
   ('Pago Móvil', '2023-04-23', 800, 5),
   ('Cheque', '2023-04-24', 1600, 20),
   ('Tarjeta de Crédito', '2023-05-01', 900, 10),
   ('Efectivo', '2023-05-02', 300, 18),
   ('Transferencia Bancaria', '2023-05-03', 700, 12),
   ('Pago Móvil', '2023-05-04', 1500, 7),
   ('Cheque', '2023-05-05', 1800, 25),
   ('Tarjeta de Crédito', '2023-05-06', 1000, 1),
   ('Efectivo', '2023-05-07', 1300, 16),
   ('Transferencia Bancaria', '2023-05-08', 400, 22),
   ('Pago Móvil', '2023-05-09', 1200, 9),
   ('Cheque', '2023-05-10', 600, 2),
   ('Tarjeta de Crédito', '2023-05-11', 1800, 19),
   ('Efectivo', '2023-05-12', 700, 15),
   ('Transferencia Bancaria', '2023-05-13', 1000, 11),
   ('Pago Móvil', '2023-05-14', 300, 6),
   ('Cheque', '2023-05-15', 1600, 13),
   ('Tarjeta de Crédito', '2023-05-16', 1200, 24),
   ('Efectivo', '2023-05-17', 900, 17),
   ('Transferencia Bancaria', '2023-05-18', 500, 21),
   ('Pago Móvil', '2023-05-19', 1400, 23),
   ('Cheque', '2023-05-20', 800, 4),
   ('Tarjeta de Crédito', '2023-05-21', 1300, 8),
   ('Efectivo', '2023-05-22', 1000, 14),
   ('Transferencia Bancaria', '2023-05-23', 700, 7),
   ('Pago Móvil', '2023-05-24', 900, 16),
   ('Cheque', '2023-05-25', 1200, 5),
   ('Tarjeta de Crédito', '2023-05-26', 1500, 12),
   ('Efectivo', '2023-05-27', 1800, 2),
   ('Transferencia Bancaria', '2023-05-28', 1000, 18),
   ('Pago Móvil', '2023-05-29', 1200, 10),
   ('Cheque', '2023-05-30', 800, 22),
   ('Tarjeta de Crédito', '2023-05-31', 500, 9),
   ('Efectivo', '2023-06-01', 700, 1),
   ('Transferencia Bancaria', '2023-06-02', 1500, 25),
   ('Pago Móvil', '2023-06-03', 300, 6),
   ('Cheque', '2023-06-04', 1200, 13),
   ('Tarjeta de Crédito', '2023-06-05', 1000, 19),
   ('Efectivo', '2023-06-06', 1800, 15);

-- TABLA SERVICIO
INSERT INTO Servicio (nombre_servicio, fecha_inicio, fecha_fin, costo, cantidad_servicios, subtotal_servicios, tecnico_asignado, id_orden_compra, id_factura, id_nomusuario) VALUES
('Mantenimiento Preventivo', '2023-04-20', '2023-04-21', 500, 1, 500, 'Hector Rojas', 1, 1, 5),
('Reparación del Sistema Hidráulico', '2023-04-22', '2023-04-23', 1200, 2, 2400, 'Jefferson Cotrina', 2, 2, 12),
('Cambio de Neumáticos', '2023-04-24', '2023-04-25', 300, 4, 1200, 'Gabriel Campos', 3, 3, 19),
('Servicio de Transmisión', '2023-04-26', '2023-04-27', 800, 1, 800, 'Lucia Ramirez', 4, 4, 29),
('Inspección Técnica', '2023-04-28', '2023-04-29', 200, 3, 600, 'Carlos Gonzales', 5, 5, 9),
('Cambio de Aceite', '2023-05-01', '2023-05-02', 150, 1, 150, 'Ana Perez', 6, 6, 25),
('Reparación de Frenos', '2023-05-03', '2023-05-04', 400, 2, 800, 'Juan Rodriguez', 7, 7, 35),
('Inspección de Motor', '2023-05-05', '2023-05-06', 250, 1, 250, 'Maria Gutierrez', 8, 8, 1),
('Alineación y Balanceo', '2023-05-07', '2023-05-08', 120, 4, 480, 'Carlos Silva', 9, 9, 15),
('Diagnóstico de Fallas', '2023-05-09', '2023-05-10', 300, 1, 300, 'Laura Medina', 10, 10, 24),
('Cambio de Filtros', '2023-05-11', '2023-05-12', 180, 3, 540, 'Pedro Martinez', 11, 11, 31),
('Revisión de Luces', '2023-05-13', '2023-05-14', 100, 1, 100, 'Sofia Hernandez', 12, 12, 3),
('Reparación de Transmisión', '2023-05-15', '2023-05-16', 700, 2, 1400, 'Alberto Ramirez', 13, 13, 14),
('Cambio de Batería', '2023-05-17', '2023-05-18', 200, 1, 200, 'Elena Cruz', 14, 14, 20),
('Servicio de Pintura', '2023-05-19', '2023-05-20', 600, 1, 600, 'Jorge Flores', 15, 15, 28),
('Diagnóstico de Computadora', '2023-05-21', '2023-05-22', 350, 2, 700, 'Raul Diaz', 16, 16, 6),
('Cambio de Pastillas de Freno', '2023-05-23', '2023-05-24', 180, 4, 720, 'Carmen Torres', 17, 17, 16),
('Lavado y Encerado', '2023-05-25', '2023-05-26', 80, 1, 80, 'Diego Ortega', 18, 18, 23),
('Reparación de Sistema Eléctrico', '2023-05-27', '2023-05-28', 450, 1, 450, 'Luisa Gomez', 19, 19, 30),
('Cambio de Amortiguadores', '2023-05-29', '2023-05-30', 300, 2, 600, 'Manuel Vargas', 20, 20, 8),
('Ajuste de Embrague', '2023-05-31', '2023-06-01', 200, 1, 200, 'Isabel Castro', 21, 21, 14),
('Reparación de Sistema de Escape', '2023-06-02', '2023-06-03', 250, 3, 750, 'Fernando Lopez', 22, 22, 18),
('Recarga de Aire Acondicionado', '2023-06-04', '2023-06-05', 120, 1, 120, 'Miguel Sanchez', 23, 23, 25),
('Reparación de Radiador', '2023-06-06', '2023-06-07', 280, 2, 560, 'Patricia Mendoza', 24, 24, 33),
('Cambio de Correa de Distribución', '2023-06-08', '2023-06-09', 400, 1, 400, 'Ricardo Herrera', 25, 25, 5),
('Alineación de Chasis', '2023-06-10', '2023-06-11', 150, 1, 150, 'Alejandro Fernandez', 26, 26, 12),
('Reparación de Neumáticos', '2023-06-12', '2023-06-13', 100, 2, 200, 'Monica Silva', 27, 27, 19),
('Diagnóstico de Sistema de Combustible', '2023-06-14', '2023-06-15', 300, 1, 300, 'Daniel Gomez', 28, 28, 29),
('Cambio de Sensor de Oxígeno', '2023-06-16', '2023-06-17', 120, 3, 360, 'Cristina Torres', 29, 29, 9),
('Servicio de Desinfección Interior', '2023-06-18', '2023-06-19', 80, 1, 80, 'Hugo Morales', 30, 30, 35),
('Reparación de Ventanas Eléctricas', '2023-06-20', '2023-06-21', 200, 1, 200, 'Laura Rodriguez', 31, 31, 6),
('Cambio de Placas de Freno', '2023-06-22', '2023-06-23', 180, 2, 360, 'Sergio Perez', 32, 32, 16),
('Ajuste de Suspensión', '2023-06-24', '2023-06-25', 250, 1, 250, 'Angela Diaz', 33, 33, 23),
('Limpieza de Inyectores', '2023-06-26', '2023-06-27', 150, 3, 450, 'Francisco Garcia', 34, 34, 30),
('Cambio de Bomba de Agua', '2023-06-28', '2023-06-29', 300, 1, 300, 'Eva Martinez', 35, 35, 1),
('Reparación de Sistema de Escape', '2023-07-01', '2023-07-02', 250, 2, 500, 'Rosa Gutierrez', 36, 36, 8),
('Recarga de Aire Acondicionado', '2023-07-03', '2023-07-04', 120, 1, 120, 'David Ramirez', 37, 37, 14),
('Reparación de Radiador', '2023-07-05', '2023-07-06', 280, 3, 840, 'Karla Vargas', 38, 38, 16),
('Cambio de Correa de Distribución', '2023-07-07', '2023-07-08', 400, 1, 400, 'Martin Rodriguez', 39, 39, 6),
('Alineación de Chasis', '2023-07-09', '2023-07-10', 150, 1, 150, 'Natalia Diaz', 40, 40, 12),
('Reparación de Neumáticos', '2023-07-11', '2023-07-12', 100, 2, 200, 'Oscar Torres', 41, 41, 19),
('Diagnóstico de Sistema de Combustible', '2023-07-13', '2023-07-14', 300, 1, 300, 'Paula Martinez', 42, 42, 29);



-- TABLA CONSUMIBLE
INSERT INTO Consumible (id_consumible, nombre_consumible, fecha_uso, cantidad, costo, id_servicio) VALUES
('CONS001', 'Aceite Hidráulico', '2023-04-20', 10, 50, 'SERV001'),
('CONS002', 'Filtro de Aire', '2023-04-22', 5, 30, 'SERV002'),
('CONS003', 'Neumáticos', '2023-04-24', 4, 300, 'SERV003'),
('CONS004', 'Aceite de Transmisión', '2023-04-26', 20, 40, 'SERV004'),
('CONS005', 'Batería', '2023-04-28', 2, 100, 'SERV005');

-- TABLA REPUESTO
INSERT INTO Repuesto (nombrerepuesto, stock, precio, cantidad, subtotal_repuesto, id_servicio, id_factura) VALUES
('Aceite Hidráulico', 100, 10, 50, 500, 50, 5),
('Filtro de Aire', 50, 5, 30, 150, 30, 10),
('Neumáticos', 200, 4, 300, 1200, 20, 15),
('Aceite de Transmisión', 50, 20, 40, 800, 10, 20),
('Batería', 10, 2, 100, 200, 40, 25),
('Aceite de Motor', 80, 15, 80, 1200, 5, 21),
('Filtro de Combustible', 35, 7, 35, 245, 15, 31),
('Líquido Refrigerante', 60, 10, 60, 600, 12, 36),
('Pastillas de Freno', 20, 3, 20, 60, 8, 41),
('Llantas de Repuesto', 150, 2, 150, 300, 4, 8),
('Aceite para Frenos', 45, 6, 45, 270, 20, 13),
('Filtro de Aceite', 30, 5, 30, 150, 18, 18),
('Líquido de Dirección Asistida', 55, 9, 55, 495, 32, 23),
('Batería de Repuesto', 110, 1, 110, 110, 2, 28),
('Lubricante Multiusos', 15, 3, 15, 45, 42, 33),
('Kit de Herramientas', 120, 1, 120, 120, 25, 38),
('Líquido Limpiaparabrisas', 40, 8, 40, 320, 35, 43),
('Fusibles', 10, 2, 10, 20, 15, 7),
('Herramientas de Reparación', 80, 1, 80, 80, 28, 12),
('Líquido de Frenos', 50, 7, 50, 350, 42, 17),
('Filtro de Polen', 30, 4, 30, 120, 10, 22),
('Gas Refrigerante', 70, 6, 70, 420, 25, 27),
('Pastillas Limpiaparabrisas', 25, 3, 25, 75, 5, 32),
('Anticongelante', 60, 10, 60, 600, 15, 37),
('Llave Inglesa', 20, 1, 20, 20, 30, 42),
('Silenciador', 50, 1, 50, 50, 20, 9),
('Lámparas de Repuesto', 15, 4, 15, 60, 38, 14),
('Cinta Aislante', 10, 1, 10, 10, 10, 19),
('Herramienta de Diagnóstico', 100, 1, 100, 100, 12, 24),
('Kit de Reparación de Neumáticos', 40, 5, 40, 200, 4, 29),
('Baterías para Controles Remotos', 15, 2, 15, 30, 30, 34),
('Gato Hidráulico', 75, 1, 75, 75, 40, 39),
('Cables de Batería', 30, 3, 30, 90, 5, 44),
('Aceite para Caja de Cambios', 55, 7, 55, 385, 15, 10),
('Llave de Ruedas', 20, 1, 20, 20, 25, 15),
('Gafas de Seguridad', 10, 2, 10, 20, 32, 20),
('Botiquín de Primeros Auxilios', 30, 1, 30, 30, 18, 25),
('Manual de Reparación', 20, 1, 20, 20, 22, 30),
('Herramienta de Extracción de Tuercas', 25, 1, 25, 25, 7, 35),
('Linterna Recargable', 15, 1, 15, 15, 42, 40),
('Impermeabilizante para Cables', 10, 2, 10, 20, 15, 45);

-- TABLA PROVEEDOR
INSERT INTO Proveedor (nombre_empresa, telefono_prov, direccion_prov, email) VALUES
('Ferreyros', '01 712 3000', 'Av. Arequipa 1067, Lima, Perú', 'contacto@ferreyros.com'),
('Repuestos Maquinaria Pesada - Mining Corp.', '999 123 456', 'Av. Los Próceres 123, San Juan de Lurigancho, Perú', 'ventas@miningcorp.com'),
('GC SERVICE & PARTS SAC', '999 687 090', 'Av. Universitaria 123, San Martín de Porres, Perú', 'ventas@gcserparts.com'),
('M.LL.V. Ventas y Servicios Empresariales', '(01) 523 7420', 'Av. Los Olivos 123, Los Olivos, Perú', 'ventas@mllv.com'),
('Técnica Repuestos', '987 654 321', 'Av. Panamericana Norte 123, Callao, Perú', 'ventas@tecnicarepuestos.com');

-- TABLA PROVEEDORREPUESTO
INSERT INTO Proveedor_Repuesto (id_proveedor, id_repuesto) VALUES
(1, 1), (3, 2), (5, 3), (1, 4), (3, 5), (5, 6), (1, 7), (3, 8), (5, 9), (1, 10),
(3, 11), (5, 12), (1, 13), (3, 14), (5, 15), (1, 16), (3, 17), (5, 18), (1, 19), (3, 20),
(5, 21), (1, 22), (3, 23), (5, 24), (1, 25), (3, 26), (5, 27), (1, 28), (3, 29), (5, 30),
(1, 31), (3, 32), (5, 33), (1, 34), (3, 35), (5, 36), (1, 37), (3, 38), (5, 39), (1, 40),
(3, 41);

-- TABLA ACCION RECOMENDADA

INSERT INTO AccionRecomendada (nombre_accion, costo_asociado, id_orden_compra) VALUES
  ('Lavado de cada componente', 600, 7),
  ('Reemplazo y Armado de piñón de ataque', 1200, 15),
  ('Montaje de eje propulsor', 800, 23),
  ('Armado del housing de pistón de freno Lh y Rh', 700, 31),
  ('Reemplazo de resortes y pernos de pistón de servicio', 550, 39),
  ('Reemplazo de tapa de bocamasa', 900, 5),
  ('Montaje de fundas', 600, 12),
  ('Reemplazo de bocina de bocamasa', 550, 20),
  ('Reemplazo de reten, rodajes y pistas de bocamasa (Mandos finales)', 1000, 28),
  ('Reemplazo de pernos de tapa de bocamasa', 700, 36),
  ('Armado de diferencial', 1100, 2),
  ('Se midió juego de Backlash', 600, 10),
  ('Montaje de tapa de cubos reductores', 800, 18),
  ('Reemplazo de todos los o-ring', 500, 26),
  ('Metalización de eje propulsor', 700, 34),
  ('Reemplazo de bocinas de tapas de bocamasa', 550, 42),
  ('Reemplazo de 4 arandelas de los espárragos', 600, 8),
  ('Reemplazo de respiradero', 650, 16),
  ('Montaje de housing de freno Lh y Rh', 750, 24),
  ('Se verificó pisada de los dientes de piñón de ataque y la corona', 900, 32);

```


