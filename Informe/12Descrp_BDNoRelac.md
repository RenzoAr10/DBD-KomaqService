# Descripcion de la implementacion BD no relacional
InfluxDB es una base de datos de series temporales optimizada para operaciones de alta velocidad de escritura y lectura, y es ideal para manejar métricas, eventos y otros datos temporales.
La implementación de InfluxDB para el proyecto implica un cambio significativo en la forma en que se almacenen y consulten los datos.

## ¿Cómo se podría implementar InfluxDB en el proyecto?

### Estructura de Datos
En lugar de tablas con relaciones, se usa "measurements" para almacenar series de tiempo. Cada measurement contiene puntos que consisten en un conjunto de campos y tags, junto con un timestamp.

Por ejemplo, si se rastrea el estado de las solicitudes de servicio con una frecuencia temporal (como solicitudes por minuto), cada punto en el measurement representaría una solicitud de servicio individual con tags para los detalles de la solicitud.

### Almacenamiento de Datos
Tags: Se usan tags para almacenar metadatos y valores que suelen ser consultados o sobre los cuales se filtra, como el ID del usuario o el nombre del servicio.
Fields: Los campos almacenan los valores que se miden o registran, como la duración del servicio, costos, etc.

### Consultas
Las consultas en InfluxDB se hacen con su lenguaje de consulta InfluxQL, que tiene similitudes con SQL pero está optimizado para consultas de series temporales.

Por ejemplo, para consultar el estado de las solicitudes de servicios se tiene:

SELECT * FROM estado_solicitudes WHERE usuario_id = 'id_del_cliente' AND time > now() - 1d
