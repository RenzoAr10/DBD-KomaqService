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

   5.El cliente ingresa los datos de pago de su tarjeta

   6.El sistema verifica si los datos son correctos. El sistema notificará si los datos han sido correctos o no en caso que haya un dato erroneo.

   7.El cliente confirmará si el se realiza el pago. El sistema procesa el pago

   8.El sistema genera un recibo para que el cliente vea los detalles como descripcion del servicio, fecha y costo de la transacción.

   9. El sistem actualiza el estado del servicio como Pagado
   
   10.-El caso de us termina.


6) Enviar informe

   1.-El empleado del Area de Comecial accede a su cuenta.
   
   2.-El empleado AC entra a la seccion de Pedidos y escoge uno de los pedidos pendientes.
   
   3.-El empleado AC escribe detalles y define la fecha de finalizacion.
   
   4.-El sistema guarda el nuevo informe.
   
   5.-El caso de uso termina.

7) Actualizando el estado del servicio

   El técnico informa al empleado del Area de Logistica sobre el estado del servicio

   1.-El empleado AL accede a su cuenta.
   
   2.-El empleado AL entra a la seccion de informes y escoge el informe a actualizar.
   
   3.-El empleado AL escribe detalles descritos por el tecnico.
   
   4.-El sistema actualiza el informe.
   
   5.-El caso de uso termina.

8) Actualizacion del estado del servicio al cliente

   1.-El empleado AC accede a su cuenta.
   
   2.-El empleado AC entra a la seccion de informes y escoge un informe que ha sido actualizado.
   
   3.-El empleado AC actualiza el estado del sevicio en base a la descripcion.
   
   4.-El sistema actualiza el servicio.
   
   5.-El caso de uso termina.

   # Requerimientos de atributos de calidad



