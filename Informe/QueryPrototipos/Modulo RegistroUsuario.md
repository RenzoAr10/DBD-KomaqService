![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/24255496-932a-490a-83ff-701b7602dbd9)

SELECT *
FROM Usuarios
WHERE nombreUsuario = @user1 AND contrasenaUsuario = @pass1;

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/969f03f9-3019-411e-b4fa-ad67c435cb57)
--Al presionar el boton Registrar
INSERT INTO Usuario (nombreUsuario, contraseñaUsuario , IdCliente)
VALUES (‘hrojas’, ‘password2’ , ‘'CL002’)
INSERT INTO Cliente (id_cliente, nombre, apellido_paterno, apellido_materno, RUC, dni, telefono, email, direccion, NombreEmpresa)
VALUES
  ('CL002', 'Ana', 'Rodriguez', 'Lopez', 19876543210, '71234567', 912345678, 'ana.rodriguez@email.com', 'Jr. Las Flores 456, Arequipa', 'Compañia minera poderosa s.a.'),
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/d49ed786-4f8c-427e-a0d9-6a3e7ed4159b)
SELECT *
FROM Usuarios
WHERE nombreUsuario = @user2 AND contrasenaUsuario = @pass2;

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/e5f3c62f-ca80-4b80-a9f0-df9146ad3783)
INSERT INTO Usuario (nombreUsuario, contraseñaUsuario , IdEmpleado)
VALUES (‘jcustodio’ , ‘password1’, ‘EMP001’)
--Al presionar el botón REGISTRAR
INSERT INTO Empleado (id_empleado, nombre, apellido_paterno, apellido_materno, dni, telefono, email, especializacion, cargo, id_jefe) VALUES
('EMP001', 'Hector', 'Rojas', 'Cotrina', '12345678', '987654321', 'hrojas@komq.com', 'Mecánico', 'Técnico Senior', NULL),

