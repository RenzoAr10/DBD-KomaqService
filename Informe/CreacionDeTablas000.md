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

 ```
** INSERCION DE VALORES

INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ001', 'Telehandler Manitou', 'MT-X 1030', 'Diésel', 'Perkins 1104D-44TA', 'U31540B', 'USR001');
INSERT INTO Maquina (id_maquina, nombre_maquina, modelo, combustible, motor, serie_motor, id_usuario) VALUES ('MAQ002', 'Cargador Frontal Cat', 'CAT 980K', 'Diésel', 'Cat C13 ACERT', 'X3C1234B', 'USR002');

 ```


