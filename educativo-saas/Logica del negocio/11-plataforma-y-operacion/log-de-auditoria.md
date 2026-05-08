---
titulo: Log de auditoría
modulo: 11-plataforma-y-operacion
tipo: regla
estado: borrador
tags: [auditoria, log, seguridad, trazabilidad]
---

# Log de auditoría

## Descripción

Registro inmutable y consultable de todas las acciones relevantes que ocurren en la plataforma. Es la base de la trazabilidad institucional y un requisito de cumplimiento (Habeas Data, Ley 1581/2012 en Colombia).

## Eventos registrados

| Categoría | Eventos |
| --- | --- |
| Autenticación | Login exitoso, login fallido, bloqueo, desbloqueo, logout, cambio de contraseña, reset, MFA habilitado / deshabilitado. |
| Sesión | Inicio, cierre, expiración por inactividad. |
| Datos académicos | Creación, edición y eliminación de notas, asistencia, observador, boletines, matrículas. |
| Datos financieros | Generación de cuota, registro de pago, anulación, conciliación manual, emisión de factura, nota crédito. |
| Configuración | Cambios en planes, calendario, conceptos, descuentos, plantillas, escalas de calificación. |
| Permisos | Asignación / revocación de roles, cambios en matriz de permisos, creación / eliminación de usuarios. |
| Comunicación | Envío de comunicados, publicaciones en agenda, citaciones. |
| Acceso del superadmin | Toda acción del [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma\|Superadministrador]] sobre el tenant. |
| Operación | Backups, restores, exportaciones, eliminaciones de tenant, suspensiones. |

## Atributos de cada entrada

| Atributo | Descripción |
| --- | --- |
| `tenantId` | Colegio en cuyo contexto ocurrió el evento. |
| `actorId` | Usuario que ejecutó la acción. |
| `actorRol` | Rol con el que actuó. |
| `accion` | Verbo de la acción (CREATE, UPDATE, DELETE, READ, LOGIN, etc.). |
| `recurso` | Entidad afectada (estudiante, nota, pago, configuración…). |
| `recursoId` | Identificador del recurso afectado. |
| `valorPrevio` | Estado anterior (en cambios). |
| `valorNuevo` | Estado nuevo. |
| `motivo` | Texto cuando aplica (anulación, eliminación, override). |
| `ip` | IP de origen. |
| `userAgent` | Navegador / cliente. |
| `timestamp` | Fecha y hora UTC. |

## Inmutabilidad

- Las entradas del log NO se editan ni borran.
- El sistema usa almacenamiento append-only para esta tabla.
- La eliminación administrativa solo se permite cuando una autoridad regulatoria lo ordena, y queda registrada como evento de meta-auditoría.

## Retención

- Mínimo **5 años** para datos académicos / financieros (alineado con normativa).
- Eventos de seguridad: mínimo **2 años**.
- El colegio puede contratar retención extendida.
- Al cerrar un tenant, los logs se preservan según política de retención antes de eliminación final.

## Acceso al log

| Quién | Qué puede ver |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma\|Superadmin de Plataforma]] | Todos los logs (auditados al consultarlos). |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Logs de su tenant. |
| [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica\|Secretaría]] / Coordinación | Vista filtrada según permiso (ej. solo logs académicos del año vigente). |
| Otros roles | No tienen acceso al log de auditoría general. |

## Búsqueda y exportación

- Filtros: tenant, actor, rol, acción, recurso, rango de fechas, IP.
- Exportación a CSV / JSON con marca de quién exportó.
- Las exportaciones también quedan en el log (meta-auditoría).

## Reglas de negocio

- **RN-LA-001 — Append-only:** los registros del log no se modifican ni eliminan.
- **RN-LA-002 — Acción privilegiada doblemente auditada:** las acciones del superadmin sobre datos del tenant se notifican al administrador del colegio y quedan en log.
- **RN-LA-003 — Cambios con valor previo y nuevo:** toda acción de modificación registra el estado antes y después.
- **RN-LA-004 — IP y user-agent obligatorios:** cada entrada captura origen.
- **RN-LA-005 — Retención mínima legal:** la retención respeta los plazos legales del país del colegio.
- **RN-LA-006 — Acceso al log auditado:** consultas y exportaciones del log también se registran.

## Notas y pendientes

- Definir el formato exacto de los `valorPrevio` / `valorNuevo` (JSON diff vs snapshot completo).
- Validar herramienta de SIEM o equivalente para análisis a gran escala.
