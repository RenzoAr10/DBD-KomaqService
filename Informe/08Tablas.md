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
