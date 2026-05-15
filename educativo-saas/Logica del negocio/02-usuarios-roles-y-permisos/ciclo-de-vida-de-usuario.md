---
titulo: Ciclo de vida de usuario
modulo: usuarios-roles-y-permisos
tipo: proceso
estado: borrador
tags: [usuarios, ciclo-de-vida, estados]
---

# Ciclo de vida de usuario

Estados por los que pasa una cuenta de usuario desde su creación hasta su baja.

## Estados

| Estado | Descripción |
| --- | --- |
| Pendiente | Cuenta creada por el sistema o por un administrador, aún no ha activado su contraseña definitiva. La cuenta funciona con la contraseña temporal hasta el primer cambio. |
| Activo | Cuenta operativa con todas las funcionalidades de su rol. |
| Suspendido | Cuenta bloqueada temporalmente por decisión del administrador (problema disciplinario, financiero, o por bloqueo del tenant). El usuario no puede iniciar sesión. Los datos se mantienen. |
| Inactivo | Cuenta sin actividad reciente (definida por el colegio). No bloquea el acceso pero aparece en reportes de uso para depuración. |
| Eliminado | Cuenta dada de baja. El usuario ya no existe operativamente. Los datos históricos asociados (notas, asistencia, observador) se preservan. |

## Transiciones permitidas

```
Pendiente → Activo (al completar el primer cambio de contraseña)
Activo → Suspendido (decisión del administrador o bloqueo del tenant)
Suspendido → Activo (decisión del administrador)
Activo → Inactivo (automático por inactividad prolongada)
Inactivo → Activo (al iniciar sesión nuevamente)
Activo → Eliminado (decisión del administrador)
Suspendido → Eliminado (decisión del administrador)
Inactivo → Eliminado (decisión del administrador o política de retención)
```

No se permiten transiciones desde `Eliminado`. La eliminación es definitiva.

## Eventos que disparan transiciones

| Evento | Transición |
| --- | --- |
| Cierre exitoso de matrícula | Crea usuario en estado `Pendiente` |
| Creación manual por administrador | Crea usuario en estado `Pendiente` |
| Primer cambio de contraseña | `Pendiente → Activo` |
| Bloqueo manual por administrador | `Activo → Suspendido` |
| Reactivación manual por administrador | `Suspendido → Activo` |
| Inactividad prolongada (configurable) | `Activo → Inactivo` |
| Inicio de sesión tras inactividad | `Inactivo → Activo` |
| Eliminación manual por administrador | `* → Eliminado` |
| Suspensión del tenant (superadmin) | `Activo → Suspendido` (todos los usuarios del tenant) |

## Reglas de negocio

- **RN-CV-001 — Estado inicial Pendiente:** todo usuario recién creado nace en estado `Pendiente`. Solo pasa a `Activo` cuando completa el primer cambio de contraseña.
- **RN-CV-002 — Eliminación preserva histórico:** al eliminar un usuario, sus datos históricos (notas, asistencia, observador, pagos) se preservan. Solo la cuenta de acceso se elimina.
- **RN-CV-003 — No reutilización de correos eliminados:** un correo de un usuario eliminado no puede ser reasignado a una cuenta nueva en el mismo tenant durante el periodo de retención.
- **RN-CV-004 — Suspensión del tenant suspende usuarios:** cuando el superadministrador suspende un tenant, todos los usuarios del tenant pasan a `Suspendido` automáticamente.
- **RN-CV-005 — Cambios de estado auditados:** toda transición queda registrada en el log de auditoría con usuario, fecha, hora, IP y motivo.

## Política de retención de datos

- Los datos de un usuario eliminado se conservan asociados al historial académico del estudiante o al historial de actuaciones del docente/personal.
- La eliminación física de un usuario solo ocurre tras la eliminación del tenant completo y vencido el periodo de retención contractual.
- El colegio puede solicitar al superadministrador la exportación de los datos de un usuario antes de su eliminación definitiva.

## Notas y pendientes

- **[Decisión tomada]** **Sin transición automática a `Inactivo` por inactividad** en MVP. El estado `Inactivo` se asigna **manualmente** por un rol con permiso. La caducidad automática queda como funcionalidad futura.
- **[Decisión tomada]** **Usuarios `Inactivos` permanecen en el sistema** por razones históricas y de auditoría, pero **quedan fuera de los listados operativos por defecto**. Su visualización requiere **filtro explícito** "incluir inactivos". Regla: **RN-CV-370 — Inactivos ocultos por defecto, visibles solo bajo filtro explícito**.
