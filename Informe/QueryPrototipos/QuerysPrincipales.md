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
![1]((https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/RevisionesSolicitadas.png)

```sql
INSERT INTO servicio (nombreServicio, direccion, idproblema)
VALUES ('Nombre_Servicio', 'Direccion_Servicio', id_problema);

```



