---
titulo: Aislamiento de datos
modulo: multi-tenancy
tipo: referencia
estado: borrador
tags: [multi-tenancy, aislamiento, seguridad]
---

# Aislamiento de datos

## Estrategia de aislamiento

El aislamiento es **total a nivel de base de datos** y **total a nivel de autenticación**.

- **Base de datos:** cada tenant tiene su propia base de datos PostgreSQL exclusiva (estrategia *database-per-tenant*). No hay tablas compartidas entre colegios. Esto elimina la posibilidad de fugas por filtros mal aplicados (`tenant_id`).
- **Autenticación:** el login se realiza siempre a través del subdominio o dominio del colegio. Las credenciales de un colegio no funcionan en el portal de otro colegio aunque el correo y la contraseña sean idénticos.
- **Almacenamiento de archivos:** los archivos del tenant (logos, fotos, documentos, PDFs, multimedia) se almacenan en buckets o prefijos exclusivos por tenant.
- **Backups:** los backups son por tenant; no existe un backup unificado.

## Reglas para acceder a datos entre tenants

- Ningún rol del tenant puede acceder a datos de otro tenant bajo ninguna circunstancia.
- La única excepción es el [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma|Superadministrador de la Plataforma]], que tiene visibilidad cross-tenant para soporte y mantenimiento.
- Todo acceso del superadministrador a datos de un tenant queda registrado en el log de auditoría con el motivo y la sesión de soporte asociada.

## Datos compartidos vs datos por tenant

| Tipo de dato | Ámbito |
| --- | --- |
| Catálogo de planes y precios | Plataforma (compartido) |
| Cuentas de superadministradores | Plataforma (compartido) |
| Logs de auditoría de acciones de plataforma | Plataforma |
| Datos institucionales del colegio | Tenant |
| Estudiantes, docentes, acudientes, demás usuarios del colegio | Tenant |
| Plan de estudios, grados, grupos, asignaciones | Tenant |
| Notas, asistencia, observador, boletines | Tenant |
| Pagos, conceptos cobrables, facturas | Tenant |
| Publicaciones, comunicados, agendas | Tenant |
| Logs de auditoría del tenant | Tenant |
| Configuración del colegio | Tenant |

## Auditoría de acceso cruzado

- Cualquier acceso a datos de un tenant por parte del superadministrador se registra en el log de auditoría del tenant accedido y en el log de plataforma.
- El registro incluye: ID del superadministrador, ID del tenant accedido, fecha, hora, IP, sesión de soporte si aplica, y la acción realizada.
- El administrador del colegio puede consultar este registro en su propio log de auditoría.

## Reglas de negocio

- **RN-AI-001 — Aislamiento total entre tenants:** ningún rol no-superadmin puede acceder a datos de otro tenant. Esta regla es estructural y no es configurable.
- **RN-AI-002 — Login por subdominio del tenant:** la autenticación se valida contra el tenant resuelto por el subdominio. Credenciales válidas en el tenant A no autentican en el tenant B.
- **RN-AI-003 — Acceso del superadmin auditado:** todo acceso del superadministrador a un tenant queda registrado y es visible para el administrador del colegio.
- **RN-AI-004 — Restauraciones aisladas:** la restauración de un tenant no afecta otros tenants. Una restauración nunca puede sobreescribir datos de otro colegio.
- **RN-AI-005 — Backups aislados:** los backups por tenant no se mezclan entre sí. La descarga o exportación de un backup nunca incluye datos de otros tenants.

## Notas y pendientes

- Documentar el procedimiento exacto de "sesión de soporte" del superadministrador (ticket interno, justificación, expiración).
- Definir si el colegio puede solicitar el log de accesos del superadministrador en cualquier momento o requiere solicitud formal.
