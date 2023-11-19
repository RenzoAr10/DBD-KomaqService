# PRO3001
## R04001 R04002 R04003

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/7fe07380-3b13-4a8a-94cf-4c05973d3767)





 ```sql
SELECT
    id_repuesto,
    nombreRepuesto,
    stock,
    cantidad,
    precioUnitario
FROM
    Repuesto;
--Al presionar al boton buscar , obteniene los valores del CB y el placeholder para filtrar la busqueda
SELECT
    id_repuesto,
    nombreRepuesto,
    stock,
    cantidad,
    precioUnitario
FROM
    Repuesto;
WHERE NombreRespuesto = %NombreRepuesto_x%
AND CantidadRespuesto <= Cantidad_x 
```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/fb83823e-1ba9-428b-98fe-a6a144c2d9b8)



``` sql
--Los campos del Proveedor se completan automaticamente en el ComboBox , al seleccionar un proveedor_x 
SELECT
    id_proveedor,
    nombre_empresa,
    telefono_prov,
    direccion_prov,
    email
FROM
    Proveedor
WHERE 
    Id_proveedor = Id_proveedor_x;

-- Insertar repuestos
INSERT INTO Repuesto (id_repuesto, stock, precio, cantidad, subtotal_repuesto, id_servicio, id_factura)
VALUES 
   ('REP_01', 8, 5000.00, 5000.00, 5000.00, 'SERV_001', 'FACT_001'),
   ('REP_02', 12, 1200.00, 1200.00, 1200.00, 'SERV_002', 'FACT_002'),
   ('REP_03', 110, 140.00, 140.00, 140.00, 'SERV_003', 'FACT_003'),
   ('REP_04', 20, 80.00, 80.00, 80.00, 'SERV_004', 'FACT_004');

-- Insertar en la tabla de relación ProveedorRepuesto
INSERT INTO ProveedorRespuesto (idProveedor, idRespuesto)
VALUES
    ('Ferreyros', 'REP_01'),
    ('Ferreyros', 'REP_02'),
    ('Ferreyros', 'REP_03'),
    ('Ferreyros', 'REP_04');
``` 
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/922d21db-4e60-4fb7-ba81-0775f3d442ce)



``` sql
-- SELECT de datos de proveedores
SELECT nombre_empresa, telefono_prov, direccion_prov, email
FROM Proveedor
WHERE NombreProveedor = %nombrex%
AND
 Desempeño = %Bueno%;
```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/8017fa7a-5640-40f2-af0f-612a6d0a59dc)


```sql
-- Insertar nuevo proveedor
INSERT INTO Proveedor (id_proveedor, nombre_empresa, telefono_prov, direccion_prov, email)
VALUES ('PROV_05', 'Nuevo Proveedor', 123456789, 'Calle Principal 123', 'nuevo@proveedor.com');
```
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/77c40c54-0b01-4feb-bc58-cd63dcd4063f)
```sql
-- Acutalizar datos proveedor
UPDATE SET nombre_empresa='FERREYROS' , telefono_prov = '987541364', direccion_prov ='Calle Principal 1341', email='fconstructora@gmail.com' , EstadoPRoveedor='Excelente'
WHERE idProveedor = 'PROV_05';
```

