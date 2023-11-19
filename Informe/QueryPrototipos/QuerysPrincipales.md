# INTERFAZ USUARIO

**Pagina Incio**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/paginainicio.png)

```sql
INSERT INTO pagina_inicio (usuario, contraseña)
VALUES ('nombre_de_usuario', 'contraseña_secreta');
```

**Añadir nuevo cliente**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/a%C3%B1adircliente.png)

```sql
INSERT INTO Usuario (nombre, telefono, email, apellidopaterno, apellidomaterno, usuario, contraseña, direccion, DNI)
VALUES ('NombreEjemplo', '123456789', 'correo@example.com', 'ApellidoPaternoEjemplo', 'ApellidoMaternoEjemplo', 'UsuarioEjemplo', 'ContraseñaEjemplo', 'DireccionEjemplo', '12345678');
```

**Datos Personales**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/DatosPersonales.png)

 ```sql
SELECT c.id_cliente, c.NombrePila, c.ApellidoPaterno, c.ApellidoMaterno, c.email, c.Dirección, u.usuario, u.contraseña
FROM CLIENTE c
JOIN Usuario u ON c.id_cliente = u.id_cliente;

```
**Solicitar Revision**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/SolicitarRevision.png)

 ```sql
INSERT INTO maquina (nombremaquina, TipoMaquina, Modelo, AñoFabricacion)
VALUES ('Nombre_Maquina', 'Tipo_Maquina', 'Modelo_Maquina', Año_Fabricacion);

 ```



**Revision de problemas**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/RevisionProblemas.png)

 ```sql
SELECT p.id_problema, p.problema, p.atender_problema
FROM problema p
JOIN revisionmaquina r ON p.id_problema = r.id_problema
WHERE r.id_maquina = 'tu_id_maquina';

 ```

**Revision Solicitudes**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/RevisionesSolicitadas.png)

 ```sql
SELECT rm.id_revision, rm.Estado, rm.fecha_revision,
       m.Id_maquina, m.TipoMaquina, m.Modelo, m.AñoFabricacion
FROM revisionmaquinaria rm
JOIN maquina m ON rm.Id_maquina = m.Id_maquina;

 ```

**Solicitar Servicio**

![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/SolicitarServicio.png?raw=true)

```sql
INSERT INTO servicio (nombreServicio, direccion, idproblema)
VALUES ('Nombre_Servicio', 'Direccion_Servicio', id_problema);

```

# INTERFAZ EMPLEADO

**Borrar Cliente**

![borrarclientes](https://github.com/RenzoAr10/DBD-KomaqService/assets/144966624/fb52fa61-d2b5-489e-a65b-64f55ac29bea)


 ```sql
SELECT nombre, DNI FROM Clientes;
DELETE FROM Clientes WHERE id_usuario = 'id_usuario';
DELETE FROM Usuario WHERE id_usuario = 'id_usuario';

INSERT INTO Cliente (nombre, telefono, email, apellidopaterno, apellidomaterno, direccion, DNI)
VALUES ('NombreEjemplo', '123456789', 'correo@example.com', 'ApellidoPaternoEjemplo', 'ApellidoMaternoEjemplo', 'DireccionEjemplo', '12345678');
INSERT INTO Usuario (nombre_usuario, contraseña)
VALUES ('UsuarioEjemplo', 'ContraseñaEjemplo')
```


**Editar Solicitud*

![2S](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/0a8d579f-9ddc-4159-96b2-2f48d38873b6)

 ```sql

SELECT revision_id, status FROM revisions;
UPDATE revisions SET status = 'Finalizado' WHERE revision_id = 'REV-001';

```

# Módulo de Comunicación con Proveedores
![4](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/616c0aae-cef2-4f1e-a400-a784d9a21096)
 ```sql

```
![5](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/5fa26fcc-61d6-46eb-a956-f1a436b08f35)

 ```sql
INSERT INTO Solicitudes (Empleado, Proveedor, Fecha, Detalles)
VALUES ('EmpleadoNombre', 'ProveedorNombre', '2023-01-01', 'Detalles de la solicitud');
```
![6](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/e01181ab-70d8-4c20-aec3-13ae1e6d561a)
 ```sql
SELECT * FROM Pedidos WHERE NumeroPedido = 'PED001';
UPDATE Pedidos SET Estado = 'En proceso', Transportista = 'Pedro Lopez', FechaEstimadaLlegada = '2023-08-05' WHERE NumeroPedido = 'PED001';

```
# Módulo de Reporte de Servicios
![1](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/07f05f0c-11f3-49b3-a928-06edcd0f163c)
 ```sql
INSERT INTO Servicio (Servicio, Fecha, Tecnico, Maquina, Descripcion, Repuestos)
VALUES ('Nombre del Servicio', '2023-09-21', 'Nombre del Técnico', 'ID o Tipo de la Máquina', 'Descripción del trabajo realizado', 'Lista de repuestos utilizados');
```
![2](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/06145328-d418-4a01-b0da-78e57b59089d)
![3](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/f804b50c-ffdf-4fc0-a7a2-bacd793b7783)




