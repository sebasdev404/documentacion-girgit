---
titulo: Autorización por plan, matriz y colegio
modulo: usuarios-roles-y-permisos
tipo: decision-e-implementacion
estado: implementado-local
tags: [roles, permisos, planes, sedes]
---

# Autorización por plan, matriz y colegio

## Decisión

El superadministrador mantiene el catálogo central de acciones, roles base, celdas de la matriz y características comerciales de cada plan. La rectora o el rector administra **solo la configuración de su colegio**: activa o desactiva celdas configurables y crea roles adicionales sin crear acciones nuevas ni quitar permisos estructurales. Una asignación académica de docente sigue siendo el límite del grupo y la asignatura, aunque un rol adicional conceda una acción.

El permiso efectivo exige simultáneamente: característica incluida en el plan vigente, permiso concedido por el rol base o adicional y alcance autorizado sobre el recurso. La interfaz oculta lo no disponible y la API vuelve a comprobarlo; ocultar un botón no es la medida de seguridad. Una sede hereda la matriz y los roles adicionales del colegio principal, pero conserva sus propios usuarios y datos en su base aislada.

Los roles adicionales **complementan** el rol principal, no lo sustituyen. Esencial permite cero; Estándar, dos; Premium, ilimitados. Estos valores se almacenan en el límite del plan para que el superadministrador gestione también planes personalizados. El colegio puede conservar los roles y la configuración guardada al bajar de plan, pero los que superen el nuevo cupo dejan de conceder acceso; los permisos de características retiradas tampoco son efectivos. Al recuperar el plan, se reactivan sin reconstruirlos. El rector no puede delegar `usuarios.ajustar_permisos` a un rol adicional. Eliminar un rol exige retirar antes todas sus asignaciones, incluso en sedes.

## Estado del corte local

- El panel del rector incluye matriz del colegio, alta/renombrado/baja de roles adicionales y asignación complementaria a personal de sede principal o adicional. Las modificaciones quedan auditadas.
- Las respuestas de sesión entregan permisos efectivos y características del plan del colegio principal; un usuario de sede recibe el mismo plan. El backend filtra permisos de roles suspendidos por cupo y de características ausentes aun si una fila histórica de permisos sigue guardada.
- Aula, preinformes, plantillas de boletín personalizables, asistencia, creación de sedes, entrada a Pagos y Reportes financieros se condicionan por característica. Pagos y Reportes financieros siguen siendo vistas informativas: esto **no** implementa cobros ni reportes contables.
- La interfaz y las rutas de Pagos y Reportes financieros exigen además sus permisos `pagos.ver` y `reportes.financieros`. El colegio puede configurar las celdas que el catálogo central marca configurables.
- Se añadieron migraciones centrales y de tenants para el límite de roles, el catálogo de permisos y los roles adicionales. Deben aplicarse en cada entorno por separado; la migración local no acredita despliegue en producción.
- El cambio administrativo de plan y la edición de un plan se rechazan si el nuevo límite deja sedes existentes fuera de capacidad. No se eliminan sedes automáticamente.

## Pendientes antes de una salida comercial

- El ciclo comercial de downgrade (fecha efectiva, facturación y conflictos por sedes activas) sigue lo definido en [[../06-monetizacion-y-pagos/planes-y-suscripciones|Planes y suscripciones]]; el cambio administrativo directo de plan de esta versión actúa de inmediato y no reemplaza ese flujo de suscripción.
- Antes de habilitar módulos nuevos se debe registrar cada acción en la matriz central, ligarla a la característica correcta, proteger la API y comprobar su alcance. No basta con añadir un enlace de menú.
- Validar visualmente con perfiles reales de rector, docente y sede, además de pruebas de regresión multi-tenant y de cambios de plan. Los datos de colegios y contraseñas de prueba no pertenecen a este documento.
