**R07001  R07002   R07002**

**PRO7001**

![](https://raw.githubusercontent.com/RenzoAr10/DBD-KomaqService/0796b76f2f0a29e50fef25f8a30936ef6848abc4/Documentacion%20de%20Soporte/querys/FacturacionYPagos/GectionDeVentas.png)

**(1)** 
Si se quiere mostrar las facturas de un cliente especifico:
Se inserta el nombre de la empresa del cliente

 ```sql
SELECT
   F.id_factura, F.estado,
   C.nombreempresa, F.fecha_emision, F.costo_total
FROM
   factura F
JOIN
   usuario U ON F.id_usuario = U.id_usuario
JOIN
   cliente C ON U.id_cliente = C.id_cliente
WHERE
   C.nombreempresa = 'NombreEmpresaEspecifica';
 ```

**(2)** 
Si se quiere mostrar las facturas si estan por cobrar o cancelado, para tomar decisiones:
Se selecciona (por cobrar) o (cancelado)

 ```sql
SELECT
   F.id_factura, F.estado,
   C.nombreempresa, F.fecha_emision, F.costo_total
FROM
   factura F
JOIN
   usuario U ON F.id_usuario = U.id_usuario
JOIN
   cliente C ON U.id_cliente = C.id_cliente
WHERE
   F.estado = 'por cobrar';

 ```

**(3)** 
Si se quiere mostrar las facturas desde una fecha inicial(se selecciona la fecha) hasta la fecha actual:
 ```sql
SELECT
    F.id_factura,
    F.estado,
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
    F.fecha_emision >= '2023-01-01' AND F.fecha_emision <= CURRENT_DATE;
 ```

# Indices 
 ```sql
-- Crear un índice en la columna nombreempresa de la tabla cliente
CREATE INDEX idx_nombreempresa ON cliente (nombreempresa);

-- La consulta original con el índice
SELECT
  F.id_factura, F.estado,
  C.nombreempresa, F.fecha_emision, F.costo_total
FROM
  factura F
JOIN
  usuario U ON F.id_usuario = U.id_usuario
JOIN
  cliente C ON U.id_cliente = C.id_cliente
WHERE
  C.nombreempresa = 'NombreEmpresaEspecifica';
 ```
ANTES

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/DESPUESnombreempresa.png)

DESPUES

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/querys/imagescostosIndices/ANTESnombreempresa.png)


# Proceso batch
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

# AJUSTE DE INDICE

```sql
--Índice para Búsqueda por Nombre de Empresa:
CREATE INDEX idx_nombreempresa ON cliente (nombreempresa);

--Índice para Filtrar por Estado de Factura:
CREATE INDEX idx_estado ON factura (estado);

--Índice para Búsquedas por Rango de Fechas:
CREATE INDEX idx_fecha_emision ON factura (fecha_emision);

--Índices Compuestos:
CREATE INDEX idx_cliente_fecha ON factura (id_usuario, fecha_emision);

--Revisar la Necesidad de Índices Existentes:
DROP INDEX IF EXISTS idx_nombreempresa;


 ```
AJUSTE DE INDICES

```sql

--Mas que todo recomendacion en caso de  eliminar un índice de clave primaria, no se hace a menos que se este rediseñando cómo se manejan las claves en la base de datos

--Eliminar indices
DROP INDEX idx_nombreempresa ON cliente;

-- si SE quiere indexar clientes activos
CREATE INDEX idx_nombreempresa_active ON cliente(nombreempresa)
WHERE estado = 'Activo';


-- crear un índice compuesto que incluya ambas columnas : nombreempresa y  id_cliente
CREATE INDEX idx_nombreempresa_idcliente ON cliente(nombreempresa, id_cliente);


-- Si un índice se ha fragmentado mucho con el tiempo, se reconstruye para mejorar el rendimiento
ALTER INDEX idx_nombreempresa ON cliente REBUILD;


-- Reconstruir un índice
ALTER INDEX idx_factura_id_factura ON factura REBUILD;

-- Actualizar estadísticas
UPDATE STATISTICS cliente idx_nombreempresa;


 ```
