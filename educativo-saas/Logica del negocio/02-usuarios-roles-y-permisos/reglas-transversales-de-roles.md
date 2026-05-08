---
titulo: Reglas transversales de roles
modulo: usuarios-roles-y-permisos
tipo: regla
estado: borrador
tags: [reglas, transversales, roles, permisos]
---

# Reglas transversales de roles

Reglas que aplican a **todos los roles** del sistema, sin importar su ámbito o configuración. No se duplican en los archivos individuales: este es el lugar de la verdad.

---

## RT-1 — Aislamiento total entre tenants

Ningún rol puede acceder a información de otro tenant bajo ninguna circunstancia.

**Detalle:**
- El aislamiento entre colegios es total **a nivel de base de datos** (schema separado por tenant en PostgreSQL) **y a nivel de autenticación** (subdominio por tenant).
- La única excepción es el [[roles/00-superadministrador-plataforma|Superadministrador de la Plataforma]], que tiene visibilidad cross-tenant para fines de soporte y mantenimiento, y cuyos accesos quedan auditados.

**Aplica a:** todos los roles.

---

## RT-2 — Verificación de permisos en frontend y backend

Todos los permisos dentro de un rol son verificados **tanto en el frontend como en el backend**.

**Detalle:**
- El frontend oculta o deshabilita lo que el rol no puede hacer (UX limpia).
- El backend valida cada acción independientemente del estado del frontend. **No es posible saltarse un permiso manipulando la interfaz** o llamando directamente al API.
- Cada endpoint del backend chequea: (a) que el usuario esté autenticado, (b) que el tenant del request coincida con el del usuario, (c) que el rol tenga el permiso requerido para la acción solicitada.

**Aplica a:** todos los roles, todas las acciones.

---

## RT-3 — Auditoría de acciones sensibles

Toda acción sensible queda registrada en un **log de auditoría**.

**Detalle:** el log debe registrar:
- **Quién** hizo la acción (usuario y rol).
- **Qué** hizo (tipo de acción).
- **Cuándo** la hizo (timestamp).
- **Desde qué IP** la hizo.
- **Sobre qué registro** la hizo (entidad afectada).

**Acciones consideradas sensibles** (lista no exhaustiva — ampliar conforme crezca el sistema):
- Edición de notas.
- Generación de documentos oficiales (constancias, certificados, paz y salvos, boletines).
- Cambios de configuración del colegio.
- Cambios de roles o permisos.
- Acciones del Superadmin sobre cualquier tenant (con motivo registrado).

**Aplica a:** todos los roles. Los logs son inmutables y consultables por el Rector y el Superadmin.

---

## RT-4 — Asignación de roles

Los roles dentro del tenant son asignados por el **Administrador del Colegio** (Rector).

**Detalle:**
- Un usuario puede tener **un solo rol principal** dentro del tenant.
- El sistema permite **complementos** sobre el rol principal sin que eso cambie el rol base. El complemento estandarizado es [[roles/07-director-de-grupo|Director de Grupo]] sobre un Docente.
- La excepción al "asignación por el Rector" es el rol del propio Rector, que lo entrega el Superadmin al crear el tenant; cambios posteriores los hace el rector saliente o el Superadmin.

**Aplica a:** todos los roles del tenant.

---

## RT-5 — Configurabilidad de permisos

Los permisos de cada rol son **configurables dentro de los límites que el sistema permite**.

**Detalle:**
- El colegio **no puede crear permisos nuevos** que no existan en el sistema.
- El colegio **sí puede restringir o ampliar** los permisos existentes dentro de lo que cada rol permite configurar.
- Cada rol distingue dos bloques: **permisos estructurales** (no modificables, garantizados por el sistema) y **permisos configurables** (ajustables por el colegio).
- Los permisos estructurales no pueden desactivarse: hacerlo rompería la operación del sistema.

**Aplica a:** todos los roles del tenant. El [[roles/00-superadministrador-plataforma|Superadministrador]] no aplica esta regla porque vive fuera del tenant.

---

## RT-6 — Acceso por subdominio del colegio

El acceso al sistema se hace siempre a través del **subdominio del colegio**.

**Detalle:**
- Un usuario registrado en el Colegio San José no puede autenticarse en el portal del Colegio La Presentación, **aunque use las mismas credenciales**, porque los tenants son completamente independientes.
- Esto es una consecuencia directa de RT-1 y se materializa en la capa de autenticación: el `tenant_id` se infiere del subdominio antes de validar credenciales.
- El [[roles/00-superadministrador-plataforma|Superadministrador]] entra por una URL distinta (panel de plataforma), no por ningún subdominio de colegio.

**Aplica a:** todos los roles del tenant.

---

## Resumen

| ID | Regla | Alcance |
| --- | --- | --- |
| RT-1 | Aislamiento total entre tenants | Todos |
| RT-2 | Verificación de permisos en frontend y backend | Todos |
| RT-3 | Auditoría de acciones sensibles | Todos |
| RT-4 | Asignación de roles por el Administrador del Colegio | Roles del tenant |
| RT-5 | Configurabilidad acotada de permisos | Roles del tenant |
| RT-6 | Acceso por subdominio del colegio | Roles del tenant |

## Notas y pendientes

- Definir el detalle del catálogo de "acciones sensibles" para auditoría (RT-3).
- Definir política de retención de logs de auditoría.
- Definir mecanismo de impersonación auditada (cuando aplica RT-1, excepción del Superadmin).
