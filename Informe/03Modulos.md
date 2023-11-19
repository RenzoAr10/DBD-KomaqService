
# Módulo de Registro de Usuarios:

Este módulo permitirá a los usuarios registrarse en la aplicación. Los usuarios podrían ser clientes, técnicos, o personal de la empresa. Deberá recopilar información básica como nombre, correo electrónico y número de teléfono. Esto es esencial para tener un sistema de autenticación y para rastrear quién realiza qué acciones en la aplicación.

## Responsabilidades:

Registro de nuevos clientes, empleados o cambios de área/cargo.

Inicio de sesión para clientes y empleados.

Recordar datos de inicio de sesión.

Registro de solicitudes de servicio.

Visualización y actualización de datos personales.

Historial de servicios y estado de pedidos para clientes.

El contratante, usualmente un administrador, se encarga de comunicarse y recibir asistencia.

Empleados pueden ver solicitudes, detalles y cambiar estados.

Calendario con fechas de pedidos.

Registro y autenticación de usuarios requerido para acceder a funciones de gestión.

Cumplimiento de regulaciones de privacidad y seguridad junto con Komaq.


# Módulo de Gestión de Órdenes de Compra:

Se encarga de la gestión de órdenes de compra dentro de la aplicación que implica la creacioón, asignación y actualización de la misma. Facilita la interacción entre clientes, proveedores, y personal interno encargado de las compras.

## Responsabilidades:

Creación de Órdenes de Compra

Visualización y actualización de órdenes

Seguimiento de estado de la orden de compra para el cliente

Asociación con proveedores

Asociación con facturas para la facilitación de la contabilidad y el seguimiento financiero

Notificaciones y recordatorios al usuario sobre fechas límite, cambios en las órdenes y otros eventos importantes

Registro de historial de las Ordenes de compras, incluyendo cambios realizados


# Módulo de Comunicación con Clientes:

Facilita la comunicación directa con los clientes, lo que es crucial para que los clientes soliciten asistencia, se mantengan informados sobre el estado de sus órdenes de servicio y mejora la satisfacción del cliente.

## Responsabilidades:

Facilitar la comunicación bidireccional entre la empresa y los clientes.

Proporcionar un canal para que los clientes soliciten asistencia.

Enviar actualizaciones sobre el estado de las órdenes de servicio a los clientes.

Mejorar la satisfacción del cliente al mantenerlos informados.

# Módulo de Comunicación con Proveedores:

Gestiona Y  optimiza  la cadena de suministro de repuestos para maquinaria pesada, asegurando la disponibilidad constante y la entrega eficiente de piezas necesarias para el mantenimiento y operación óptima de la maquinaria.

## Responsabilidades:


Realizar y gestionar pedidos precisos de repuestos, asegurando que las especificaciones y cantidades sean correctas y estén alineadas con las necesidades de la empresa.

Establecer y mantener relaciones sólidas con proveedores confiables, negociando términos favorables y asegurando la calidad y fiabilidad en la entrega de repuestos.

Organizar eficientemente la logística para la entrega de repuestos, incluyendo el seguimiento de envíos y la gestión de cualquier incidencia logística.

Supervisar el inventario de repuestos para evitar escasez o excesos, y realizar ajustes basados en análisis de tendencias y patrones de uso.

Asegurar que todos los repuestos cumplan con los estándares de calidad requeridos y adherirse a las regulaciones y normativas pertinentes.

Evaluar el rendimiento de los proveedores y la eficiencia del proceso de suministro, generando informes que ayuden en la toma de decisiones estratégicas.

R04001: Los usuarios autorizados deben poder acceder y revisar la lista completa de proveedores a través de la Página Principal del Módulo, con la capacidad de realizar búsquedas específicas y recibir notificaciones relacionadas con cambios o actualizaciones en el estado de los proveedores.

R04002: Los usuarios con permisos de edición deben poder actualizar los detalles de los proveedores, incluyendo contactos y evaluaciones de desempeño, y dichas actualizaciones deben reflejarse inmediatamente en el sistema para todos los usuarios relevantes.

R04003: Las solicitudes de pedido de repuestos solo pueden ser creadas por usuarios con roles de compras y deben incluir toda la información requerida como tipo de repuesto, cantidad y fecha de solicitud antes de ser enviadas a los proveedores.

R04004: El seguimiento de logística y entregas debe ser actualizado en tiempo real, y los usuarios necesarios deben recibir alertas automáticas en caso de retrasos o cambios en la fecha estimada de llegada de los pedidos.

R04005: Los informes de gestión de suministros deben ser generados mensualmente por el sistema, y los usuarios deben poder personalizar estos informes según fecha, proveedor y tipo de repuesto para análisis específicos y toma de decisiones informadas.

# Módulo de Reporte de Servicios: 

Se encarga de facilitar una documentación detallada y eficiente de todas las actividades de mantenimiento realizadas en la maquinaria pesada, proporcionando una base de datos exhaustiva para el seguimiento de calidad y la gestión eficaz de los servicios.

## Responsabilidades:

Registrar meticulosamente todas las actividades de mantenimiento realizadas, incluyendo procedimientos, piezas usadas y tiempo invertido.

Mantener un registro actualizado de las tareas ejecutadas por cada técnico, asegurando la precisión y detalle de la información.

Crear y gestionar un historial completo para cada equipo o maquinaria, permitiendo un seguimiento efectivo a lo largo del tiempo.

Implementar y supervisar estándares de calidad en los servicios de mantenimiento, asegurando la satisfacción del cliente y la integridad del equipo.

Preparar informes detallados sobre las operaciones de mantenimiento, proporcionando insights para la toma de decisiones y la mejora continua.

R05001: Los usuarios deben poder visualizar una lista consolidada de las últimas actividades de mantenimiento desde la página principal del módulo, y esta vista debe ser actualizada en tiempo real tras cada nueva entrada de registro.

R05002: El formulario de registro de mantenimiento debe ser completado en su totalidad antes de que se permita su envío, y debe incluir la validación de campos para asegurar que todos los datos necesarios sean recogidos (fecha, técnico, maquinaria, servicio, piezas).

R05003: Solo los usuarios con los permisos adecuados, como los técnicos de mantenimiento o los administradores, pueden agregar o editar entradas en el historial de mantenimiento de la maquinaria.

R05004: Los informes generados en la sección 'Análisis y Reportes' deben reflejar datos precisos y actuales, y deben ser accesibles basándose en el nivel de permisos del usuario, garantizando que la información sensible sea manejada de manera segura.

R05005: Cada entrada en el historial de mantenimiento debe ser rastreable hasta un registro de mantenimiento específico, permitiendo auditorías detalladas y seguimiento de la calidad del servicio a lo largo del tiempo.

# Módulo de Facturación y Pagos:

Está relacionado con la facturación de servicios y permite a los clientes realizar pagos de manera conveniente, lo que es esencial para el flujo de ingresos de la empresa.

## Responsabilidades:

Generar facturas detalladas para los servicios y repuestos proporcionados.

Permitir que los clientes realicen pagos de manera conveniente.

Registrar y gestionar los pagos para el flujo de ingresos de la empresa.

Facilitar una contabilidad eficiente.

# Módulo de Informes de Gestión:

Genera informes detallados sobre el rendimiento de la empresa, lo que brinda información valiosa para tomar decisiones estratégicas basadas en datos y mejorar la eficiencia operativa.

## Responsabilidades:

Generar informes detallados sobre el rendimiento de la empresa.

Proporcionar información valiosa para la toma de decisiones estratégicas.

Ayudar a mejorar la eficiencia operativa y el cumplimiento de objetivos.

![image](https://github.com/RenzoAr10/DBD-KomaqService/assets/55066238/e6d73b53-4bd3-43c1-ba5a-d1041de034b6)

