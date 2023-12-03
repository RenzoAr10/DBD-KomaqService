R03001 R03002 R03003

PR03001

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/df96d4f8-bcfe-4c7a-b1ee-f30b68563a14)
```sql
INSERT INTO Servicio (id_servicio, nombre_servicio, fecha_inicio, tecnico_asignado, id_orden_compra, id_factura) 
VALUES ('SERV001', 'Reparación de motor', '2023-04-15', 'Juan Pérez', 'OC123', 'FAC456');

```

R03004 R03005

PR03002

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/545fba8f-899a-4344-b45a-1f2de1e94130)
```sql
SELECT id_solicitud, estado_revision, fecha_revision, detalles
FROM EstadoServicios
WHERE usuario_id = 'id_del_cliente';
```

# INDICE
```sql
CREATE INDEX idx_tipo_maquina ON Servicios(tipo_maquina);
CREATE INDEX idx_ano_fabricacion ON Servicios(ano_fabricacion);
```

# BATCH 

BEGIN TRANSACTION;
```sql
-- Insertar la nueva solicitud de servicio
INSERT INTO Servicios (servicio, maquina, descripcion, tipo_de_maquina, modelo, ano_de_fabricacion)
VALUES ('valor_servicio', 'valor_maquina', 'valor_descripcion', 'valor_tipo_de_maquina', 'valor_modelo', 'valor_ano_de_fabricacion');

-- Suponiendo que hay un sistema de notificaciones o auditoría
INSERT INTO Notificaciones (tipo, descripcion, fecha, id_servicio)
VALUES ('Nueva solicitud de servicio', 'Se ha registrado una nueva solicitud de servicio.', CURRENT_TIMESTAMP, SCOPE_IDENTITY());

-- O insertar en la tabla de auditoría
INSERT INTO AuditoriaServicios (accion, fecha, usuario)
VALUES ('Creación de solicitud de servicio', CURRENT_TIMESTAMP, 'usuario_cliente');

COMMIT TRANSACTION;
```

# AJUSTE DEL INDICE
```sql
--Índice para la Tabla EstadoServicios:
CREATE INDEX idx_usuario_id ON EstadoServicios(usuario_id);

--Índice para la Columna fecha_inicio en la Tabla Servicios:
CREATE INDEX idx_fecha_inicio ON Servicios(fecha_inicio);

--Índices Basados en las Operaciones de Inserción:
CREATE INDEX idx_servicio ON Servicios(servicio);
CREATE INDEX idx_maquina ON Servicios(maquina);
CREATE INDEX idx_modelo ON Servicios(modelo);

--Índices Compuestos:
CREATE INDEX idx_tipo_modelo ON Servicios(tipo_de_maquina, modelo);

--Índice para la Tabla Notificaciones:
CREATE INDEX idx_id_servicio_notificaciones ON Notificaciones(id_servicio);


```
