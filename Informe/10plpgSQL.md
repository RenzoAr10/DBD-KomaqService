# Informe de gestion 

**PRO7001**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/0796b76f2f0a29e50fef25f8a30936ef6848abc4/Documentacion%20de%20Soporte/querys/FacturacionYPagos/GectionDeVentas.png)

 ```sql
CREATE OR REPLACE FUNCTION generar_reporte_ventas()
RETURNS TABLE (
    id_factura VARCHAR(10),
    estado VARCHAR(100),
    nombreempresa VARCHAR(50),
    fecha_emision VARCHAR(100),
    costo_total DECIMAL(8,2)
) AS
$$
BEGIN
    RETURN QUERY
    SELECT
        F.id_factura,
        F.forma_pago,
        C.nombreempresa,
        F.fecha_emision,
        F.costo_total
    FROM
        factura F
    JOIN
        usuario U ON F.id_usuario = U.id_usuario
    JOIN
        cliente C ON U.id_cliente = C.id_cliente
    WHERE
        C.nombreempresa = 'Mminera las bambas s.a.';
END;
$$ LANGUAGE plpgsql;

---------

SELECT * FROM generar_reporte_ventas();
 ```



# Modulo facturacion y pagos

**PRO6003**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/60a1d4fd0b998af08f7f97751724bb9ff8d63eda/Documentacion%20de%20Soporte/querys/FacturacionYPagos/REPORTE%20DE%20VENTAS.png)

Cuando se haga click en reporte de ventas se tiene una vista de las facturas y sus caracteristicas

 ```sql
DO $$ 
BEGIN
    INSERT INTO factura (id_factura, estado, id_usuario, fecha_emision, costo_total)
    VALUES ('FAC002', 'Pagada', 'UR001', '2023-01-01', 100.00);
END $$;
```

# Informe de STOCK
```sql
-- Crear procedimiento almacenado para el proceso batch
CREATE OR REPLACE PROCEDURE GenerarInformeControlStock()
LANGUAGE PLPGSQL
AS $$
BEGIN
    -- Obtener la fecha actual
    DECLARE fecha_actual DATE := CURRENT_DATE;

    -- Crear una tabla temporal para almacenar el informe
    CREATE TEMPORARY TABLE TempInformeStock AS
    SELECT
        id_repuesto,
        nombreRepuesto,
        stock,
        cantidad,
        precioUnitario
    FROM
        Repuesto;

    -- Insertar registros en la tabla temporal según el filtro
    INSERT INTO TempInformeStock
    SELECT
        id_repuesto,
        nombreRepuesto,
        stock,
        cantidad,
        precioUnitario
    FROM
        Repuesto
    WHERE
        NombreRepuesto = '%NombreRepuesto_x%'
        AND CantidadRespuesto <= Cantidad_x;

    -- Imprimir el informe en la consola o en una tabla de informes
    RAISE NOTICE 'Informe de Control de Stock (%)', fecha_actual;
    SELECT * FROM TempInformeStock;

    -- Limpiar la tabla temporal después de generar el informe
    DROP TABLE IF EXISTS TempInformeStock;
END;
$$;

-- Ejecutar el procedimiento almacenado para generar el informe
CALL GenerarInformeControlStock();
```
