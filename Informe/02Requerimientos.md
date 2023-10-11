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

1)Disponibilidad: El sistema está disponible para que los usuarios realicen solicitudes y accedan a la información en un horario amplio.

2)Seguridad: El sistema garantiza la seguridad de los datos del usuario, además de protección de información personal y financiera.
   
3)Fiabilidad: El sistema minimiza los inconvenientes del servicio solicitados, como la realizacion del pedido de manera consistente

4)Usabilidad: La interfaz de usuario es sencillo y facil de usar, permitiendo a los usuarios realizar solicitudes y realizar pagos de manera intuitiva.


# RESTRICCIONES

Plataforma: La app debe estar disponible para dispositivos móviles y computadoras.
Tecnología: La app debe ser desarrollada utilizando tecnologías de código abierto.
Costo: El costo de desarrollo y mantenimiento de la app debe ser razonable.
Tecnología Utilizada:La aplicación debe desarrollarse utilizando tecnologías específicas, lo que puede incluir el uso de un lenguaje de programación o un marco de desarrollo particular.
Tiempo de Desarrollo:El tiempo de desarrollo de la aplicación puede estar sujeto a restricciones, lo que podría afectar el cronograma del proyecto.
Costo del Desarrollo:El presupuesto para el desarrollo de la aplicación podría ser limitado, lo que requerirá una gestión eficiente de los recursos disponibles.



#### ° El cliente al ser nuevo no cuenta con una cuenta para iniciar sesion entonces este podrá registrarse en el sistema.
#### ° Un empleado al ser nuevo y no tener cuenta para iniciar sesion entonces este podrá registrarse en el sistema.
#### ° Un empleado al ser nuevo en algun cargo (admin) o al cambiarse de area de trabajo en la empresa entonces este podrá registrarse en el sistema con un nuevo cargo o en una nueva area.
#### ° El cliente o empleado podra loguarse al sistema con su usuario y contraseña.
#### ° El usuario al no poder loguearse por olvido de su nombre de usuario o contraseña,este tiene la opción de recordar datos en la plataforma para el próximo inicio de sesión.
#### ° El cliente, como usuario,podra registrarse para solicitar algun servicio de  Komaq
#### ° Los campos solicitados son todos obligatorios exceptuando la foto de perfil
#### ° El cliente al loguearse podrá visualizar los datos personales con los cuales fueron registrados la cuenta
#### ° Si el cliente desea actualizar alguno de sus datos,este deberá contactarse con el area de soporte para poder realizar el cambio
#### ° El cliente podrá visualizar su historial de todos los servicios solicitados, detallando información al seleccionar alguna celda de la tabla
#### ° El cliente al realizar una selección de pedido podra ver el estado (Pendiente , en curso , Rechazado , Completado) del pedido el cual como se mencionó , podrá cambiar conforme el servicio siga su curso
#### ° El cliente  puede ver pero no editar los siguiente campos mostrados
#### ° El cliente puede solicitar un servicio de los cuales ofrece la empresa por medio de su plataforma web.
#### ° En los datos del usuario se menciona al contratante.
#### ° El contratante será la persona encargada de comunicarse y recibir la asistencia directo de los servicios. 
#### ° El contratante no necesariamente es el mismo de usuario de la cuenta
#### ° El usuario como contratante, por lo general, será el administrador o jefe de proyecto de la empresa que requiere los servicios.
#### ° El contratante será la persona que estará en constante comunicación con KOMAQ para validar e informar el progreso del servicio.
#### ° El empleado, como usuario, puede ver las solicitudes de todos los clientes, pudiendo filtrar estas mismas por , Cliente (contratante) , el jefe de proyecto (usuario de la cuenta) , Tipo de actividad del servicio brindada
#### ° El empleado puede ver los datos de cada pedido, al darle click a la celda de la tabla , aquí se mostrarán más detalles sobre la solicitud de servicio , así mismo podrá cambiar el estado de cada una de la solicitudes
#### ° El empleado puede visualizar un calendario con todas las fechas de los pedidos realizados, esto con la finalidad de mejorar la planificación del desarrollo de los procesos de fabricación, mantenimiento y reparación que brinda la empresa
#### °  Todos los usuarios deben registrarse y autenticarse en la plataforma para acceder a las funcionalidades relacionadas con la gestión de pedidos y solicitudes.
#### °  Los usuarios deben gerantizar, conjuntamente con Komaq, garantizar la seguridad cumpliendo con las regulaciones de privacidad aplicables.

####
####
#### °  Los empleados evaluaran las solicitudes, cambiando el estado de esta, la cual puede tomar 4 estados(Pendiente , en curso , Rechazado , Completado)
#### °  Los clientes pueden iniciar nuevas solicitudes o pedidos de servicios o productos a través de la plataforma.
#### °   Los clientes pueden realizar un seguimiento del estado de sus solicitudes o pedidos y recibir notificaciones cuando cambia su estado.
####  ° Los clientes pueden comunicarse directamente con el contratante asignado para recibir asistencia o aclaraciones adicionales sobre sus solicitudes.
#### °  Los contratantes son responsables de comunicarse directamente con los clientes que han solicitado servicios y proporcionarles asistencia o información adicional.
####  °  Los contratantes pueden actualizar el estado de las solicitudes o pedidos asignados a ellos a medida que avanzan en su proceso de resolución.
#### °   Los contratantes pueden generar informes de desempeño relacionados con las solicitudes que han manejado.
####  ° Los empleados pueden acceder a las solicitudes asignadas a ellos y actualizar su estado a medida que progresan.
#### °  Los empleados pueden comunicarse con otros empleados, clientes o contratantes en relación con las solicitudes o pedidos en curso
#### °  Los empleados pueden registrar el tiempo empleado en cada solicitud para fines de seguimiento y facturación si es necesario.
####  ° Los administradores pueden agregar, editar o eliminar usuarios dentro del sistema, incluyendo clientes, empleados y contratantes.
####  ° Los administradores pueden supervisar y administrar el flujo de trabajo de todas las solicitudes y pedidos en la plataforma.
####  ° Los administradores pueden asignar solicitudes o pedidos a empleados o contratantes específicos, según la disponibilidad y la capacidad.
####  ° Los administradores pueden intervenir en caso de problemas o disputas en el proceso de gestión de solicitudes.


####
####
####  ° Los clientes pueden solicitar servicios de mantenimiento preventivo o correctivo a través de la plataforma web.
####  ° Los clientes pueden realizar un seguimiento del estado de sus solicitudes de servicio y recibir actualizaciones sobre el progreso.
####  ° Los clientes pueden  utilizar la plataforma para realizar consultas técnicas y recibir orientación sobre problemas relacionados con la maquinaria pesada.
####  °  Los contratantes pueden comunicarse con los técnicos asignados para coordinar y programar servicios de mantenimiento.
####  °  Los contratantes pueden solicitar informes y actualizaciones sobre el progreso de los servicios contratados.
####  °  Los contratantes pueden realizar pagos relacionados con los servicios ejecutados a través de la plataforma.
####  ° Los administradores pueden agregar, editar o eliminar usuarios en el sistema, incluyendo personal técnico y clientes.
####  ° Los administradores pueden asignar técnicos o ingenieros específicos para realizar tareas de mantenimiento o resolver problemas técnicos.
####  ° Los administradores pueden realizar un seguimiento del desempeño del personal técnico, incluyendo evaluaciones y capacitación.
####  ° Los empleados técnicos pueden acceder a las tareas de mantenimiento asignadas a ellos a través de la plataforma y actualizar su estado a medida que avanzan en la ejecución de servicios.
####  ° Los empleados técnicos pueden hacer un registro de los diagnósticos técnicos realizados en los equipos de maquinaria pesada, identificando problemas y necesidades de reparación.
####  ° Los empleados técnicos pueden hacer una actualizacion del inventario de repuestos y materiales utilizados durante la ejecución de servicios.



####
####
####  ° Los clientes pueden solicitar cotizaciones para servicios de mantenimiento, reparación y capacitación a través de la plataforma.
####  ° Los clientes pueden revisar y aprobar los presupuestos proporcionados por la empresa a través de la plataforma web.
####  ° Los clientes pueden acceder a los contratos de servicios celebrados con la empresa y verificar los términos y condiciones a través de la plataforma.
####  ° Los empleados de ventas pueden crear presupuestos para servicios de mantenimiento, reparación y capacitación a partir de las solicitudes de los clientes.
####  ° Los empleados de ventas pueden  generar contratos en función de los presupuestos aprobados por los clientes.
####  ° Los empleados de ventas mantienen una comunicación activa con los clientes a través de la plataforma para discutir detalles de presupuestos y contratos.
####  °  Los contratantes pueden revisar propuestas de servicios y contratos a través de la plataforma antes de su aprobación final.
####  ° Los contratantes pueden firmar digitalmente los contratos a través de la plataforma.
####  ° Los administradores pueden agregar, editar o eliminar usuarios en el sistema, incluyendo personal de ventas y clientes.
####  ° Los administradores  pueden supervisar las actividades de ventas, incluyendo la generación de presupuestos y la firma de contratos.
