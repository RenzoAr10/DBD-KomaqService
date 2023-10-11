# Requerimientos funcionales

1) Creacion de usuario
   
   1.-El usuario accede a la página oficial.
   
   2.-El usuario entra a la sección de Sesión y escoge 'Crear cuenta'.
   
   3.-El usuario proporciona su nombre, apellido, pais, DNI, correo electrónico y contraseña (agreagar foto de perfil es opcional) además de confirmar los Terminos y condiciones.
   
   4.-El sistema guarda la nueva cuenta.

   5.-El sistema notifica al usuario que la cuenta ha sido creada con éxito
   
   5.-El caso de uso termina.


   3.-El sistema notifica al usuario en caso que haya algun error al llenar los datos, ya sea por falta completar, datos duplicados o error de conectividad.


2) Solicitar servicio
   
   1.-El cliente accede a su cuenta.
   
   2.-El cliente selecciona la seccion Solicitar Servicio.
   
   3.-El cliente especifica el tipo de servicio que requiere

   4.-El cliente proporciona los detalles especificos de la solicitud como fecha, hora ,ubicacion y urgencia, y otros detalles segun el tipo de servicio seleccionado (puede ser seleccionar el respuesto y la cantidad, escoger tipo de maquinaria, etc).

   5.El sistema verifica la disponibilidad de la fecha o de los recursos. El sistema notificará al ususario en caso que falte disponibilidad correspondiente.

   6.El sistema calculará los costos del servicio según los detalles poporcionados.

   7.El sistema mostrará un resumen de la solicitud y el cliente confirmará la solicitud.

   8.El sistema guarda el nuevo servicio

   9.El sistema notifica al cliente que el servicio ha sido realizado con exito.

   10.El cliente puede hacer seguimiento del estado de su servicio en la seccion Pedidos 
   
   11.-El caso de uso termina.

   

   4.-El sistema notificará al cliente en caso que falten datos primordiales


4) Pagar servicio
   
   1.-El cliente accede a su cuenta.
   
   2.-El cliente selecciona la seccion Recibo.
   
   3.-El sistema mostrará un resumen de los servicios que ya han sidos completados y disponibles a pagar. Esto mostraria detalles como la descripcion del sericio, fecha y hora de la solicitud y el costo.
   
   4.-El cliente selecciona los servicios que desea pagar y luego escoger la opcion Pagar. Mostrará costo total de los servicios seleccionados

   5.-El cliente ingresa los datos de pago de su tarjeta

   6.-El sistema verifica si los datos son correctos. El sistema notificará si los datos han sido correctos o no en caso que haya un dato erroneo.

   7.-El cliente confirmará si el se realiza el pago. El sistema procesa el pago

   8.-El sistema genera un recibo para que el cliente vea los detalles como descripcion del servicio, fecha y costo de la transacción.

   9.-El sistem actualiza el estado del servicio como Pagado
   
   10.-El caso de uso termina.


5) Cancelar Servicio

   1.-El cliente accede a su cuenta.

   2.-El cliente entra a la seccion de Pedidos

   3.-El sistema mostrará la opcion de cancelar servicio en caso que el estado de la solicitud este en "Pendiente".

   4.-El cliente selecciona la opcion Cancelar Servicio del cual quiere cancelar.

   5.-El sistema solicitará confirmación de la cancelación del servicio.

   6.-El notificará que el servicio ha sido cancelado

   7.-El sistema actualizara el estado del sevicio a Cancelado y borrará el servicio del listado del cliente.

   8.-El caso de uso termina.

   En caso que se quiera cancelar servicio cuando el estado está en curso, el cliente podrá llamar al número de la empresa para dar a un posible solución.


6) Actualizar estado de solicitud

   1.-El empleado accede a su cuenta.

   2.-El empleado entra a la seccion pedidos. Tendrá disponible una busquedor en la cual puede poner el identificador del servicio

   3.-El empleado selecciona el pedido a actualizar estado. El sistema mostaraá detalles del servicio.

   4.-El empleado cambia el estado del sevicio. Los estados disponibles a cambiar son "en curso" o "finalizado".

   5.-El sistema actualiza el el estado del servicio.

   6.-El caso de uso termina.

   
   # Requerimientos de atributos de calidad


   1.-Disponibilidad: El sistema está disponible para que los usuarios realicen solicitudes y accedan a la información en un horario amplio.

   2.-Seguridad: El sistema garantiza la seguridad de los datos del usuario, además de protección de información personal y financiera.

   3.-Fiabilidad: El sistema minimiza los inconvenientes del servicio solicitados, como la realizacion del pedido de manera consistente

   4.-Usabilidad: La interfaz de usuario es sencillo y facil de usar, permitiendo a los usuarios realizar solicitudes y realizar pagos de manera intuitiva.



    # Restricciones
 
   1.-Plataforma: La app debe estar disponible para dispositivos móviles y computadoras.

   2.-Tecnología: La app debe ser desarrollada utilizando tecnologías de código abierto.

   3.-Costo del Desarrollo:   El presupuesto para el desarrollo de la aplicación podría ser limitado, lo que requerirá una gestión eficiente de los recursos disponibles.
   
   4.-Tecnología Utilizada:   La aplicación debe desarrollarse utilizando tecnologías específicas, lo que puede incluir el uso de un lenguaje de programación o un marco de desarrollo particular.

   5.-Tiempo de Desarrollo:   El tiempo de desarrollo de la aplicación puede estar sujeto a restricciones, lo que podría afectar el cronograma del proyecto.


   # Casos de uso

## Caso de Uso 1: Registrarse como Cliente
-Actor: Cliente

-Pasos:

-El cliente abre la aplicación.

-Selecciona la opción de registro.

-Completa el formulario de registro con su información personal.

-Confirma su registro.

## Caso de Uso 2: Iniciar Sesión
-Actores: Cliente, Técnico, Personal de la Empresa

-Cliente

-Técnico

-Personal de la Empresa

-Pasos:

-El usuario abre la aplicación.

-Ingresa su correo electrónico y contraseña.

-La aplicación verifica las credenciales y permite el acceso.

-Módulo de Gestión de Órdenes de Servicio:

