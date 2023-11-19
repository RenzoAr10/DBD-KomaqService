Creación de Usuario

REQ0001: El sistema permite al usuario acceder a la página oficial.
REQ0002: El usuario puede ingresar a la sección de Sesión y elegir 'Crear cuenta'.
REQ0003: Se proporciona un formulario de registro para que el usuario complete con información personal, incluyendo nombre, apellido, país, DNI, correo electrónico y contraseña.
REQ0004: El sistema guarda la nueva cuenta del usuario.
REQ0005: El sistema notifica al usuario sobre la creación exitosa de la cuenta.
REQ0006: En caso de error al llenar datos, el sistema notifica al usuario sobre el error.

Solicitar Orden de Compra

REQ0007: El cliente puede acceder a su cuenta.
REQ0008: En la sección "Solicitar Orden de compra", el cliente especifica el tipo de servicio requerido.
REQ0009: El cliente proporciona detalles específicos de la solicitud, como fecha, hora, ubicación y otros detalles según el tipo de servicio seleccionado.
REQ0010: El sistema verifica la disponibilidad de recursos y fechas.
REQ0011: El sistema calcula los costos del servicio según los detalles proporcionados.
REQ0012: Se muestra al cliente un resumen de la solicitud para su confirmación.
REQ0013: El sistema guarda la nueva orden de compra.
REQ0014: El sistema notifica al cliente sobre la realización exitosa del servicio.
REQ0015: En caso de datos faltantes, el sistema notifica al cliente.

Pagar Orden de Compra

REQ0016: El cliente puede acceder a su cuenta.
REQ0017: En la sección "Recibo", se muestra un resumen de los servicios completados y disponibles para pagar.
REQ0018: El cliente selecciona los servicios que desea pagar y procede al pago.
REQ0019: El cliente ingresa los datos de pago de su tarjeta.
REQ0020: El sistema verifica la corrección de los datos y notifica al cliente.
REQ0021: El cliente confirma el pago y el sistema procesa la transacción.
REQ0022: Se genera un recibo con detalles de la transacción y se actualiza el estado del servicio a "Pagado".

Cancelar Factura

REQ0023: El cliente accede a su cuenta.
REQ0024: En la sección de "Pedidos", se muestra la opción de cancelar el servicio si el estado es "Pendiente".
REQ0025: El cliente selecciona la opción de cancelar el servicio y confirma.
REQ0026: El sistema notifica al cliente sobre la cancelación exitosa y actualiza el estado a "Cancelado".
REQ0027: En caso de intentar cancelar un servicio en curso, el cliente puede llamar al número de la empresa para encontrar una solución.

Actualizar Estado de Solicitud

REQ0028: El empleado accede a su cuenta.
REQ0029: En la sección de "Pedidos", el empleado busca el identificador del servicio.
REQ0030: El empleado selecciona el pedido y cambia su estado a "En curso" o "Finalizado".
REQ0031: El sistema actualiza el estado del servicio y finaliza el caso de uso.
Requisitos de Atributos de Calidad:

REQ0032: Disponibilidad: La aplicación debe estar disponible ampliamente durante el día.
REQ0033: Seguridad: La aplicación garantiza la seguridad de los datos del usuario.
REQ0034: Fiabilidad: La aplicación minimiza inconvenientes en el servicio.
REQ0035: Usabilidad: La interfaz de usuario es intuitiva y fácil de usar.

Restricciones:

REQ0036: Plataforma: La aplicación debe ser compatible con dispositivos móviles y computadoras.
REQ0037: Tecnología: Se utilizarán tecnologías de código abierto.
REQ0038: Costo del Desarrollo: El presupuesto para el desarrollo es limitado.
REQ0039: Tecnología Utilizada: La aplicación se desarrollará utilizando tecnologías específicas.
REQ0040: Tiempo de Desarrollo: El tiempo de desarrollo está sujeto a restricciones.

Caso de Uso 1: Registrarse como Cliente

REQ0041: El cliente puede abrir la aplicación.
REQ0042: Accede a la opción de registro.
REQ0043: Completa el formulario de registro con información personal.
REQ0044: Confirma el registro.
REQ0045: El sistema verifica y notifica sobre la creación exitosa de la cuenta.
REQ0046: En caso de error en los datos, el sistema notifica al cliente.

Caso de Uso 2: Iniciar Sesión

REQ0047: El usuario abre la aplicación.
REQ0048: Ingresa su correo electrónico y contraseña.
REQ0049: La aplicación verifica las credenciales y permite el acceso.

Caso de Uso 3: Crear Orden de Servicio

REQ0050: El cliente inicia sesión.
REQ0051: Accede a la sección de creación de órdenes de servicio.
REQ0052: Completa el formulario de la orden de servicio.
REQ0053: Envía la orden de servicio.

Caso de Uso 4: Asignar Técnico a Orden de Servicio

REQ0054: El personal de la empresa abre una orden de servicio.
REQ0055: Asigna un técnico disponible a la orden de servicio.

Caso de Uso 5: Actualizar Estado de Orden de Servicio

REQ0056: El técnico inicia sesión.
REQ0057: Accede a las órdenes de servicio asignadas.
REQ0058: Actualiza el estado de la orden de servicio.

Caso de Uso 6: Ver Inventario de Repuestos

REQ0059: El usuario abre la aplicación.
REQ0060: Accede a la sección de inventario de repuestos.
REQ0061: Explora la lista de repuestos disponibles.

Caso de Uso 7: Solicitar Repuestos a Proveedores

REQ0062: El personal de la empresa inicia sesión.
REQ0063: Accede al módulo de comunicación con proveedores.
REQ0064: Crea una solicitud de repuestos.
REQ0065: Envía la solicitud a los proveedores.

Caso de Uso 8: Recibir Cotizaciones de Proveedores

REQ0066: El personal de la empresa accede a las cotizaciones de repuestos.
REQ0067: Compara las cotizaciones y selecciona la más adecuada.

Caso de Uso 9: Generar Factura para el Cliente

REQ0068: El personal de la empresa abre la sección de facturación y pagos.
REQ0069: Selecciona una orden de servicio completada.
REQ0070: Completa el formulario de la orden de servicio.
REQ0071: Genera una factura con los detalles de los servicios y repuestos.

Caso de Uso 10: Registrador Actividad de Mantenimiento

REQ0072: El técnico inicia sesión.
REQ0073: Accede a la sección de registro de actividades de mantenimiento.
REQ0074: Completa un formulario para registrar las actividades realizadas en una máquina.
REQ0075: Genera un informe detallado de las actividades de mantenimiento realizadas.

Caso de Uso 11: Ofrecer Propuestas ABC

REQ0076: El cliente inicia sesión.
REQ0077: Accede a la sección de propuestas de valor.
REQ0078: Revisa las opciones de costos y calidad de repuestos.

Caso de Uso 12: Registrador Diagnóstico de Fallas

REQ0079: El técnico inicia sesión.
REQ0080: Accede a la sección de diagnóstico de fallas.
REQ0081: Registra detalles sobre el estado actual de la máquina y los problemas identificados.

Caso de Uso 13: Importar y Vender Repuestos

REQ0082: El personal de la empresa inicia sesión.
REQ0083: Accede al módulo de importación y venta de repuestos.
REQ0084: Registra nuevos repuestos importados y gestiona las ventas.

Caso de Uso 14: Brindar Asistencia Remota

REQ0085: El técnico inicia sesión.
REQ0086: Accede a la sección de asistencia remota.
REQ0087: Brinda asistencia en línea a los clientes.
