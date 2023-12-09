# InfluxDB

La implementación de InfluxDB en el proyecto implica la transición a una base de datos de series temporales, un tipo especial de base de datos NoSQL. Vamos a explorar el desarrollo conceptual de esta decisión, enfocándonos en el tipo de motor elegido y el motor de base de datos específico. 

## Tipo de Motor Elegido: Base de Datos de Series Temporales
Las bases de datos de series temporales como InfluxDB se especializan en el manejo de datos que cambian o se registran con el tiempo. A diferencia de los motores de bases de datos tradicionales (como bases de datos relacionales o documentales), las bases de datos de series temporales están optimizadas para:

Almacenamiento Eficiente: Pueden almacenar grandes cantidades de puntos de datos temporales de manera eficiente, aprovechando compresiones y estructuras de datos especializadas.

Consultas Temporales: Ofrecen un rendimiento superior en consultas que involucran intervalos de tiempo, como promedios móviles, sumas acumulativas, y comparaciones a lo largo del tiempo.

Escritura de Alta Velocidad: Diseñadas para manejar un alto volumen de escrituras, lo que es esencial para aplicaciones como monitoreo en tiempo real y telemetría.

## Motor de Base de Datos Elegido
InfluxDB se destaca entre las bases de datos de series temporales por varias razones:

Estructura de Datos: Utiliza 'measurements' y puntos, donde cada punto consta de tags (para metadatos) y fields (para valores medidos), acompañados de un timestamp. Esto facilita un esquema flexible y eficiente para datos temporales.

Lenguaje de Consulta: InfluxQL, similar a SQL, pero optimizado para manipular y consultar series de tiempo, lo que facilita la transición para aquellos familiarizados con SQL.

Rendimiento: Ofrece un equilibrio óptimo entre velocidad de escritura y capacidad de consulta, crucial para aplicaciones que requieren análisis en tiempo real.

Escalabilidad y Seguridad: Adecuado para escenarios de alto rendimiento y ofrece opciones para garantizar la seguridad de los datos.

## Comparación con Otros Tipos de Motores NoSQL
Bases de Datos Documentales: Como MongoDB, son excelentes para almacenar documentos JSON y ofrecen una gran flexibilidad de esquemas. Sin embargo, no están optimizadas específicamente para datos temporales.

Bases de Datos Orientadas a Grafos: Como Neo4j, son ideales para representar y explorar relaciones complejas entre datos, pero no son la mejor opción para manejar grandes volúmenes de datos temporales.

Bases de Datos Clave-Valor: Como Redis, son extremadamente rápidas para operaciones de lectura y escritura pero no ofrecen las mismas capacidades analíticas para datos temporales que InfluxDB.



# Descripcion de la implementacion BD no relacional

InfluxDB es una base de datos de series temporales optimizada para operaciones de alta velocidad de escritura y lectura, y es ideal para manejar métricas, eventos y otros datos temporales.

Implementar InfluxDB  podría ofrecer un rendimiento mejorado para datos temporales y métricas, pero también requerirá que se adapten los métodos actuales de manejo de datos para acomodar una estructura de almacenamiento y consulta diferente. Esto incluiría repensar los modelos de datos, cómo y cuándo se eswcribe en la base de datos, y cómo  se realizan las consultas para extraer información relevante.

La implementación de InfluxDB para el proyecto implica un cambio significativo en la forma en que se almacenen y consulten los datos.

 

### ¿Cómo se podría implementar InfluxDB en el proyecto?



## Estructura de Datos
En lugar de tablas con relaciones, se usa "measurements" para almacenar series de tiempo. Cada measurement contiene puntos que consisten en un conjunto de campos y tags, junto con un timestamp.

Por ejemplo, si se rastrea el estado de las solicitudes de servicio con una frecuencia temporal (como solicitudes por minuto), cada punto en el measurement representaría una solicitud de servicio individual con tags para los detalles de la solicitud.

## Almacenamiento de Datos
Tags: Se usan tags para almacenar metadatos y valores que suelen ser consultados o sobre los cuales se filtra, como el ID del usuario o el nombre del servicio.
Fields: Los campos almacenan los valores que se miden o registran, como la duración del servicio, costos, etc.

## Consultas
Las consultas en InfluxDB se hacen con su lenguaje de consulta InfluxQL, que tiene similitudes con SQL pero está optimizado para consultas de series temporales.

Por ejemplo, para consultar el estado de las solicitudes de servicios se tiene:

 ```sql
SELECT * FROM estado_solicitudes WHERE usuario_id = 'id_del_cliente' AND time > now() - 1d

 ```
## Inserciones
Las inserciones se realizan enviando puntos a la base de datos. Cada punto consiste en un conjunto de tags y fields, así como un timestamp.

Por ejemplo:
```sql
INSERT estado_solicitudes,usuario_id=id_del_cliente estado_revision="En curso", detalles="Solicitud visualizada por técnico" 1465839830100400200

 ```

## Seguridad
Nos aseguramos de que InfluxDB esté configurado de manera segura, con autenticación y autorización adecuadas para proteger los datos.

## Monitoreo y Análisis
InfluxDB es especialmente potente para el monitoreo y análisis en tiempo real debido a su capacidad para manejar grandes volúmenes de escrituras y consultas rápidas.

## Integración con la Aplicación
Se adapta la aplicación para interactuar con InfluxDB, utilizando sus bibliotecas cliente para el lenguaje de programación que se esta usando.



# Configuración

## Instalación Local:

- Se descarga InfluxDB desde el sitio web oficial.
- Se instala InfluxDB siguiendo las instrucciones para el sistema operativo.
- Se inicia el servicio de InfluxDB y asegúrate de que esté corriendo.

## Como Servicio en la Nube:

- Elegimos un proveedor de servicios en la nube que ofrezca InfluxDB como un servicio gestionado (por ejemplo, AWS, Azure, o InfluxData Cloud).
- Creamos una instancia de InfluxDB a través del portal del proveedor.
- Configuramos los ajustes de seguridad, como grupos de seguridad y políticas de acceso.


# Implementación

### Crear Measurements y Schema:

- Definimos los measurements (equivalentes a las tablas en SQL).
- Establecimos los tags (p.ej., ID de usuario, tipo de máquina) y fields (p.ej., duración del servicio, costos).


 ### Insertar Datos:

-Utilizamos la línea de comandos de InfluxDB o clientes de biblioteca en la aplicación para insertar datos.
-Formato de ejemplo para inserción:
```sql
insert servicio,usuario_id=user1234,tipo_maquina=excavadora duracion=3h,costo=300

 ```
### Realizar Consultas:

InfluxQL para realizar consultas que extraigan datos de series temporales relevantes para la aplicación.
Ejemplo de consulta para obtener la duración total del servicio por usuario:
```sql
SELECT sum(duracion) FROM servicio WHERE usuario_id = 'user1234'

 ```
### Modificar el Código de Aplicación:

- Integramos la biblioteca cliente de InfluxDB en la aplicación.
- Reemplazamos las operaciones de base de datos relacional por llamadas a la API de InfluxDB para escribir y leer datos.

### Generar el Escenario Externamente:

- Creamos un conjunto de scripts o una interfaz de administración para gestionar los measurements y datos.
- Implementamos una función de exportación/importación si se necesitan operaciones de migración de datos desde o hacia sistemas relacionales.

