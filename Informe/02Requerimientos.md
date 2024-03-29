# Requerimientos funcionales

1) Creacion de usuario
   
   1.-El usuario accede a la página oficial.
   
   2.-El usuario entra a la sección de Sesión y escoge 'Crear cuenta'.
   
   3.-El usuario proporciona su nombre, apellido, pais, DNI, correo electrónico y contraseña (agreagar foto de perfil es opcional) además de confirmar los Terminos y condiciones.
   
   4.-El sistema guarda la nueva cuenta.

   5.-El sistema notifica al usuario que la cuenta ha sido creada con éxito
   
   6.-El caso de uso termina.


   3.-El sistema notifica al usuario en caso que haya algun error al llenar los datos, ya sea por falta completar, datos duplicados o error de conectividad.


2) Solicitar orden de compra
   
   1.-El cliente accede a su cuenta.
   
   2.-El cliente selecciona la seccion Solicitar Orden de compra.
   
   3.-El cliente especifica el tipo de servicio que requiere

   4.-El cliente proporciona los detalles especificos de la solicitud como fecha, hora ,ubicacion y urgencia, y otros detalles segun el tipo de servicio seleccionado (puede ser seleccionar el respuesto y la cantidad, escoger tipo de maquinaria, etc).

   5.El sistema verifica la disponibilidad de la fecha o de los recursos. El sistema notificará al ususario en caso que falte disponibilidad correspondiente.

   6.El sistema calculará los costos del servicio según los detalles poporcionados.

   7.El sistema mostrará un resumen de la solicitud y el cliente confirmará la solicitud.

   8.El sistema guarda la nueva orden de compra

   9.El sistema notifica al cliente que los servicios han sido realizados con exito.

   10.El cliente puede hacer seguimiento del estado de su servicio en la seccion Pedidos 
   
   11.-El caso de uso termina.

   

   4.-El sistema notificará al cliente en caso que falten datos primordiales


4) Pagar Orden de compra
   
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


5) Cancelar Factura

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

   ### Objetivo:

   El objetivo de este caso de uso es permitir que un cliente potencial se registre en la aplicación móvil de Komaq Service para acceder a los servicios y funcionalidades disponibles.


   
    ### Actor:

      -Cliente
   
    ### Pasos:

      -El cliente abre la aplicación.

      -Selecciona la opción de registro.

      -Completa el formulario de registro con su información personal.

      -Confirma su registro.
   
   ## Caso de Uso 2: Iniciar Sesión

   ### Objetivo:

   El objetivo de este caso de uso es permitir que los usuarios inicien sesión en la aplicación móvil de Komaq Service para acceder a sus cuentas y utilizar las funcionalidades disponibles.



   ### Actores: 

      -Cliente

      -Técnico

      -Personal de la Empresa

   ### Pasos:

      -El usuario abre la aplicación.

      -Ingresa su correo electrónico y contraseña.

      -La aplicación verifica las credenciales y permite el acceso.

   ## Caso de Uso 3: Crear Orden de Servicio
   
   ### Objetivo:
   
   El objetivo de este caso de uso es permitir que un cliente cree una orden de servicio para solicitar mantenimiento o reparación de maquinaria pesada.


   
   ### Actores: 
   
    ### Actor:

      -Cliente

   ### Pasos:

      -El cliente inicia sesión.

      -Accede a la sección de creación de órdenes de servicio.

      -Completa el formulario de la orden de servicio

      -Envia la orden de servicio.


   
      ## Caso de Uso 4: Asignar Técnico a Orden de Servicio

   ### Objetivo:

   El objetivo de este caso de uso es permitir que el personal de la empresa asigne un técnico disponible a una orden de servicio para que realice el mantenimiento requerido.



   
   ### Actores: 


      -Técnico

      -Personal de la Empresa

   ### Pasos:

      -El personal de la empresa abre una orden de servicio.

      -Asigna un técnico disponible a la orden de servicio.
   

      ## Caso de Uso 5: Actualizar Estado de Orden de Servicio

   ### Objetivo:

   El objetivo de este caso de uso es permitir que el técnico actualice el estado de una orden de servicio para reflejar su progreso o completitud.



   ### Actores: 


      -Técnico

      -Personal de la Empresa

   ### Pasos:

      -El técnico inicia sesión.

      -Accede a las órdenes de servicio asignadas.

      -Actualiza el estado de la orden de servicio (por ejemplo, en progreso, completada).


   
 ## Caso de Uso 6: Ver Inventario de Repuestos
 
   ### Objetivo:

El objetivo de este caso de uso es permitir que los usuarios consulten el inventario de repuestos disponibles en Komaq Service.

   ### Actores: 

   -Técnico

   -Personal de la Empresa

   ### Pasos:

   -El usuario abre la aplicación.

   -Accede a la sección de inventario de repuestos.

   -Explora la lista de repuestos disponibles.


 ## Caso de Uso 7: Solicitar Repuestos a Proveedores

 ###  Objetivo:

El objetivo de este caso de uso es permitir que el personal de la empresa solicite repuestos necesarios a los proveedores externos.
   
   ### Actor: 

   -Personal de la Empresa

   ### Pasos:

   -El personal de la empresa inicia sesión.

   -Accede al módulo de comunicación con proveedores.

   -Crea una solicitud de repuestos.

   -Envía la solicitud a los proveedores.

   
 ## Caso de Uso 8: Recibir Cotizaciones de Proveedores

   ### Objetivo:

El objetivo de este caso de uso es permitir que el personal de la empresa acceda a las cotizaciones de repuestos enviadas por los proveedores y seleccione la más adecuada.
   ### Actor: 

   -Personal de la Empresa

   ### Pasos:

   -El personal de la empresa abre la sección de comunicación con proveedores.

   -Accede a las cotizaciones de repuestos enviadas por los proveedores.

   -Compara las cotizaciones y selecciona la más adecuada.


   
   ## Caso de Uso 9: Generar Factura para el Cliente

   ### Objetivo:

El objetivo de este caso de uso es permitir que el personal de la empresa genere una factura detallada para el cliente con los servicios y repuestos proporcionados.
   
 ### Actor:

  -Personal de la Empresa

   ### Pasos:

 -El personal de la empresa abre la sección de facturación y pagos.

  -Selecciona una orden de servicio completada.

 -Completa el formulario de la orden de servicio

-Genera una factura con los detalles de los servicios y repuestos proporcionados al cliente.


  ## Caso de Uso 10: Registrar Actividad de Mantenimiento

  ### Objetivo:

El objetivo de este caso de uso es permitir que el técnico registre las actividades de mantenimiento realizadas en una máquina y genere un informe detallado.
   
   ### Actor: 

   -Técnico

   ### Pasos:

   -El técnico inicia sesión.

   -Accede a la sección de registro de actividades de mantenimiento.

   -Completa un formulario para registrar las actividades realizadas en una máquina.

   -Genera un informe detallado de las actividades de mantenimiento realizadas en un período específico.



 ## Caso de Uso 11: Ofrecer Propuestas ABC

 ### Objetivo:

El objetivo de este caso de uso es permitir que el técnico registre las actividades de mantenimiento realizadas en una máquina y genere un informe detallado.
   
   ### Actores: 

   -Cliente

   -Personal de la Empresa

   ### Pasos:

   -El cliente inicia sesión.

   -Accede a la sección de propuestas de valor.

   -Revisa las opciones de costos y calidad de repuestos para tomar decisiones informadas.


   
  ## Caso de Uso 12: Registrar Diagnóstico de Fallas

  ### Objetivo:

El objetivo de este caso de uso es permitir que el técnico registre las actividades de mantenimiento realizadas en una máquina y genere un informe detallado.
   
   ### Actor: 

   -Técnico

   ### Pasos:

   -El técnico inicia sesión.

   -Accede a la sección de diagnóstico de fallas.

   -Registra detalles sobre el estado actual de la máquina y los problemas identificados.


  ## Caso de Uso 13: Importar y Vender Repuestos

  ### Objetivo:

El objetivo de este caso de uso es permitir que el técnico registre las actividades de mantenimiento realizadas en una máquina y genere un informe detallado.
   
   ### Actor: 

   -Personal de la Empresa

   ### Pasos:

   -El personal de la empresa inicia sesión.

   -Accede al módulo de importación y venta de repuestos.

   -Registra nuevos repuestos importados y gestiona las ventas.


   
   
  ## Caso de Uso 14: Brindar Asistencia Remota
   
   ### Actor: 

   -Técnico

   ### Pasos:

   -El técnico inicia sesión.

   -Accede a la sección de asistencia remota.

   -Brinda asistencia en línea a los clientes.
