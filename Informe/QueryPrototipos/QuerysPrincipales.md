**Añadir nuevo cliente**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/a%C3%B1adircliente.png)

```sql
INSERT INTO Usuario (nombre, telefono, email, apellidopaterno, apellidomaterno, usuario, contraseña, direccion, DNI)
VALUES ('NombreEjemplo', '123456789', 'correo@example.com', 'ApellidoPaternoEjemplo', 'ApellidoMaternoEjemplo', 'UsuarioEjemplo', 'ContraseñaEjemplo', 'DireccionEjemplo', '12345678');
```

**Datos Personales**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/DatosPersonales.png)

 ```sql
SELECT Cliente
FROM Cliente
JOIN Usuario ON Cliente.id_cliente = Usuario.id_cliente
WHERE Usuario.id_usuario = tu_id_usuario;

```
**Añadir Cliente**
![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/a%C3%B1adircliente.png)

 ```sql
INSERT INTO Usuario (nombre, telefono, email, apellidopaterno, apellidomaterno, usuario, contraseña, direccion, DNI)
VALUES ('NombreEjemplo', '123456789', 'correo@example.com', 'ApellidoPaternoEjemplo', 'ApellidoMaternoEjemplo', 'UsuarioEjemplo', 'ContraseñaEjemplo', 'DireccionEjemplo', '12345678');

 ```
