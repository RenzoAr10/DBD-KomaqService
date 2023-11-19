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
