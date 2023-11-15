--Tabla de Usuarios: Para almacenar la información de los usuarios que acceden al sistema.

CREATE TABLE usuarios (
    id_usuario INT PRIMARY KEY,
    nombre VARCHAR(255),
    correo_electronico VARCHAR(255),
);
