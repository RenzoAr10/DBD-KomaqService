# Modelo Conceptual


![Erdplus](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/ERDPLUS..png?raw=true)


## Diccionario de datos

**Entidad: Cliente**

**Semántica: Representa a las personas con las que la empresa tiene relaciones comerciales.**
![cliente](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/cliente.png)

**Entidad: Servicio**

**Semántica: Representa una acción o tarea específica que la empresa realiza para atender las necesidades de sus clientes.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/servicio.png)

Tabla 1

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/tabla1.png?raw=true)

**Entidad: AreaComercial**

**Semántica: Representa el gestión de las actividades comerciales y de ventas de la empresa, implica la gestión de relaciones con clientes.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/AreaComercial.png?raw=true)

**Entidad: Técnico**

**Semántica: Representa a los profesionales que son asignados para el servicio.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/tecnico.png?raw=true)

**ENTIDAD: AreaLogistica**

**Semántica: Representa al área que se ocupa de la planificación y el tiempo promedio para terminar un servicio, trabaja de la mano con el área comercial.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/AreaLogistica.png?raw=true)

**Entidad: Informe** 

**Semántica: Representa al área que se ocupa de la planificación y el tiempo promedio para terminar un servicio, trabaja de la mano con el área comercial.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/Informe.png?raw=true)

## Reglas de Negocio 

***Cliente Solicita Servicio:***

Regla: Un cliente puede solicitar uno o varios servicios de mantenimiento.

Descripción: Los clientes tienen la capacidad de iniciar solicitudes de servicio cuando requieren mantenimiento o reparación en su maquinaria pesada. Pueden solicitar múltiples servicios en diferentes momentos.

***AreaComercial Recepciona Servicio:***

Regla: El área comercial es responsable de recibir y registrar las solicitudes de servicio de los clientes.

Descripción: El personal del área comercial debe estar disponible para recibir y documentar las solicitudes de servicio realizadas por los clientes.

***AreaComercial Documenta Informe:***

Regla: El área comercial es responsable de registrar la información relacionada con la creación de informes de servicio.

Descripción: Cuando se completa un servicio, el área comercial debe documentar la información relevante para la generación de informes, como la fecha de finalización y el contenido del informe.

***AreaLogistica Recepciona Informe:***

Regla: El área logística recibe y registra los informes de servicio generados por el área comercial.

Descripción: Los informes de servicio, una vez generados por el área comercial, se envían al área logística para su recepción y almacenamiento.

***AreaLogistica Asigna Técnico:***

Regla: El área logística es responsable de asignar técnicos para llevar a cabo los servicios de mantenimiento.

Descripción: El área logística debe asegurarse de que se asigne un técnico calificado para realizar el servicio de mantenimiento programado, teniendo en cuenta la disponibilidad y las habilidades del técnico.





