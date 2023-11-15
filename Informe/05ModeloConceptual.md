# Modelo Conceptual


![Erdplus](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/CHEN%20(2).png)


# Modelo Conceptual2


![1](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/erdplus003.png)



## Diccionario de datos

**Entidad: Cliente**

**Semántica: Representa a las personas con las que la empresa tiene relaciones comerciales.**
![cliente](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/cliente.png)

**Entidad: OrdenServicio**

**Semántica: Representa una acción o tarea específica que la empresa realiza para atender las necesidades de sus clientes.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/ordenServicio.png)

Tabla 1

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/tabla%201.png)

**Entidad: Empleado**

**Semántica: Representa al empleado en la empresa.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/empleado.png)

Tabla 2

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/tabla%202.png)

Tabla 3

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/tabla%203.png)


**Entidad: RegistroServicio**

**Semántica:  Representa un registro detallado de un servicio de mantenimiento realizado en una maquinaria pesada específica.**

![](https://github.com/RenzoAr10/DBD-KomaqService/blob/main/Documentacion%20de%20Soporte/RegistroServicio.png)


## Reglas de Negocio 

***Maquina - OrdenServicio:***

Cada orden de servicio debe estar asociada a una máquina pesada específica que requiere mantenimiento.
Una máquina pesada puede tener múltiples órdenes de servicio a lo largo del tiempo, pero cada orden está relacionada con una máquina específica.

***RevisionMaquinaria - ProgramacionServicios:***

Cada Revision de Maquinaria debe estar programada para un servicio específico en una fecha de inicio determinada.
Cada Revision de Maquinaria debe estar relacionada con una única programación de servicio.

***Repuesto - AlmacenRepuestos:***

Cada repuesto debe estar relacionado con el almacén de repuestos en el que se encuentra actualmente.
El stock de repuestos se gestiona en los almacenes de repuestos.

***Cliente - OrdenServicio:***

Cada orden de servicio debe estar vinculada a un cliente que solicitó el servicio de mantenimiento.
Registra qué cliente solicitó cada servicio.

***RegistroServicio - DetallesActividades:***

Cada registro de servicio puede incluir detalles específicos de actividades realizadas en el servicio.
Los detalles de las actividades son una entidad débil y dependen de un registro de servicio.

***RegistroServicio - RegistroConsumibles :***

Cada registro de servicio puede incluir detalles de consumibles utilizados durante el servicio.
Los registros de consumibles son una entidad débil y dependen de un registro de servicio.


***Proveedor - Repuesto:***

Cada repuesto debe estar asociado a un proveedor específico que suministra ese repuesto.
Registra los proveedores que suministran repuestos a la empresa.

***Repuesto - OrdenServicio:***

Cada orden de servicio puede incluir múltiples repuestos utilizados durante el servicio.
Cada repuesto utilizado en una orden de servicio debe estar relacionado con esa orden de servicio específica.
El registro de repuestos utilizados en una orden de servicio debe incluir la cantidad de cada repuesto y su costo asociado.

***OrdenServicio - Empleado:***

Cada orden de servicio debe asignarse a al menos un empleado responsable de realizar el servicio.
Un empleado puede estar asignado a múltiples órdenes de servicio, dependiendo de la carga de trabajo y la especialización requerida.

***Empleado - Empleado (Relación de Asignacion):***

Establece una relación de asignación entre los empleados, donde un empleado puede ser un supervisor o jefe de otro empleado.
Cada empleado puede tener un único supervisor o jefe, pero un supervisor puede tener varios subordinados.

***OrdenServicio - RevisionMaquinaria:***

Cada orden de servicio puede estar relacionada con una revisión de maquinaria específica.
Las revisiones de maquinaria pueden llevarse a cabo como parte de una orden de servicio de mantenimiento.

***RevisionMaquinaria - RegistroServicio:***

Cada revisión de maquinaria puede tener asociados uno o más registros de servicio relacionados con los resultados de la inspección.
Los registros de servicio pueden incluir detalles sobre las acciones tomadas en función de los resultados de la revisión de maquinaria.

