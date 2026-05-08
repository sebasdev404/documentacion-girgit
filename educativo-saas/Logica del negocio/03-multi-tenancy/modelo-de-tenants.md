---
titulo: Modelo de tenants
modulo: multi-tenancy
tipo: referencia
estado: borrador
tags: [multi-tenancy, tenants]
---

# Modelo de tenants

Cada colegio es un tenant independiente. Esta página define cómo se modelan, identifican y gestionan.

## Definición de tenant

Un tenant es la representación lógica de un colegio dentro de la plataforma. Cada tenant tiene:

- **Base de datos exclusiva** (no compartida con otros tenants).
- **Subdominio propio** del tipo `<slug-colegio>.dominio-saas.com`, o un dominio propio configurado por el colegio.
- **Configuración independiente** (datos institucionales, calendario, escala, etc.).
- **Cuota de almacenamiento** asociada al plan contratado.
- **Plan de suscripción** activo.
- **Backups automáticos** independientes.

## Identificación del tenant (subdominio, slug, etc.)

- **Slug del tenant:** identificador único, en minúsculas y sin caracteres especiales (ej. `colegio-san-jose`). Se asigna en la creación y no puede modificarse posteriormente sin intervención del superadministrador.
- **Subdominio por defecto:** `<slug>.<dominio-saas>`.
- **Dominio propio (opcional):** el colegio puede configurar un dominio que apunte al tenant, sujeto a verificación DNS.
- **Identificación interna:** UUID inmutable usado en logs, integraciones y backups.

## Atributos básicos del tenant

| Atributo | Descripción |
| --- | --- |
| Nombre completo del colegio | Visible en documentos generados. |
| NIT | Para facturación electrónica. |
| Resolución MEN | Número de resolución del Ministerio de Educación. |
| Dirección física | |
| Teléfono | |
| Correo institucional | Destinatario inicial de credenciales del administrador. |
| Logo | Sujeto a cuota de almacenamiento. |
| Tipo de calendario | A o B (ver [[../04-procesos-academicos/periodos-academicos\|Períodos académicos]]). |
| Plan contratado | Define cuota, número de estudiantes incluidos, funcionalidades. |

## Plan asociado al tenant

Cada tenant tiene exactamente **un plan activo** en cualquier momento. El plan determina:

- Número máximo de estudiantes facturables.
- Cuota de almacenamiento.
- Periodo de retención de backups.
- Funcionalidades habilitadas (notificaciones WhatsApp, plantilla personalizada, etc.).

Ver [[../06-monetizacion-y-pagos/planes-y-suscripciones|Planes y suscripciones]].

## Estados del tenant

| Estado | Descripción | Operable |
| --- | --- | --- |
| **En provisionamiento** | Tenant recién creado por el superadministrador, base de datos y subdominio en preparación. | No |
| **Activo** | Tenant en operación normal. | Sí |
| **Configurando** | El administrador del colegio aún no ha completado la configuración inicial obligatoria. | Parcial — solo configuración |
| **Suspendido** | Tenant temporalmente bloqueado por incumplimiento, problema técnico o restauración en curso. Los usuarios no pueden iniciar sesión. | No |
| **En restauración** | Restauración de backup en curso. Los usuarios no pueden iniciar sesión. | No |
| **Eliminado** | Tenant dado de baja definitivamente. Los datos siguen retenidos según la política contractual antes del borrado físico. | No |

## Reglas de negocio

- **RN-T-001 — Creación exclusiva por superadministrador:** solo el [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma|Superadministrador de la Plataforma]] puede crear tenants. No existe registro público de colegios.
- **RN-T-002 — Provisionamiento automático:** al crear un tenant, el sistema genera automáticamente la base de datos aislada, el subdominio y el usuario administrador inicial con credenciales enviadas al correo institucional.
- **RN-T-003 — Configuración inicial obligatoria:** un tenant en estado `Configurando` no es operable hasta que el administrador del colegio complete la configuración inicial mínima.
- **RN-T-004 — Suspensión preserva datos:** la suspensión no elimina datos. Solo bloquea el acceso de usuarios mientras el estado esté vigente.
- **RN-T-005 — Eliminación con retención contractual:** la eliminación de un tenant respeta la política de retención de datos definida contractualmente. Los datos se conservan durante el periodo acordado antes del borrado físico.
- **RN-T-006 — Slug inmutable:** el slug del tenant no puede modificarse desde el panel del colegio. Solo el superadministrador puede cambiarlo bajo solicitud formal.
- **RN-T-007 — Un plan activo a la vez:** cada tenant tiene exactamente un plan activo. Los cambios de plan generan transición con efecto en la siguiente facturación.

## Notas y pendientes

- Definir si el subdominio se puede liberar para reutilización cuando un tenant es eliminado o queda reservado para evitar suplantación.
- Definir el flujo exacto de migración de plan (upgrade/downgrade) y su impacto en cuotas.
