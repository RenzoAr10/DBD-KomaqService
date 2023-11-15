--Tabla de Usuarios: Para almacenar la información de los usuarios que acceden al sistema.

CREATE TABLE usuarios (
    id_usuario INT PRIMARY KEY,
    nombre VARCHAR(255),
    correo_electronico VARCHAR(255),
);


--Tabla de Problemas: Para registrar los problemas que pueden surgir con las máquinas, con un identificador, una descripción del problema, el tipo y la gravedad del mismo.

CREATE TABLE problemas (
    id_problema VARCHAR(10) PRIMARY KEY,
    descripcion VARCHAR(255),
    tipo_problema VARCHAR(255),
    gravedad VARCHAR(50),
    atender_problema BOOLEAN
);


--Tabla de Revisión de Máquinas: Para mantener un historial de todas las revisiones realizadas en las máquinas.

CREATE TABLE revisiones_maquina (
    id_revision INT PRIMARY KEY,
    id_usuario INT,
    fecha_revision DATE,
    comentarios TEXT,
    FOREIGN KEY (id_usuario) REFERENCES usuarios(id_usuario)
);

--Tabla de Servicios Solicitados: Para registrar las solicitudes de servicio hechas por los usuarios.

CREATE TABLE servicios (
    id_servicio INT PRIMARY KEY,
    id_usuario INT,
    fecha_solicitud DATE,
    estado VARCHAR(50),
    FOREIGN KEY (id_usuario) REFERENCES usuarios(id_usuario)
    -- Cada servicio solicitado está vinculado a un usuario.
);
