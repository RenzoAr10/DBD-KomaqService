
![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/135069f3-7f7b-45f3-973a-82722d41c453)

```sql
SELECT
    id_repuesto,
    nombreRepuesto,
    stock,
    cantidad,
    precioUnitario
FROM
    Repuesto;```

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/121067321/9bf7bac5-5858-419e-a93a-13bc3cf79668)
```
-- SELECT
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

-- SELECT de datos de proveedores
SELECT nombre_empresa, telefono_prov, direccion_prov, email
FROM Proveedor;

-- Insertar nuevo proveedor
INSERT INTO Proveedor (id_proveedor, nombre_empresa, telefono_prov, direccion_prov, email)
VALUES ('PROV_05', 'Nuevo Proveedor', 123456789, 'Calle Principal 123', 'nuevo@proveedor.com');

