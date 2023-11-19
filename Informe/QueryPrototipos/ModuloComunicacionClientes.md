![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/df96d4f8-bcfe-4c7a-b1ee-f30b68563a14)
```sql
INSERT INTO Servicio (id_servicio, nombre_servicio, fecha_inicio, tecnico_asignado, id_orden_compra, id_factura) 
VALUES ('SERV001', 'Reparación de motor', '2023-04-15', 'Juan Pérez', 'OC123', 'FAC456');

```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/545fba8f-899a-4344-b45a-1f2de1e94130)
```sql
SELECT id_solicitud, estado_revision, fecha_revision, detalles
FROM EstadoServicios
WHERE usuario_id = 'id_del_cliente';
```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/54ca6118-eee3-4200-8678-fc18cbb19b30)
```sql
INSERT INTO Comentarios (id_servicio, comentario, fecha_comentario, usuario_id) 
VALUES ('SOL002', 'El servicio fue excelente y en tiempo.', CURRENT_DATE, 'usuario_cliente');
```

