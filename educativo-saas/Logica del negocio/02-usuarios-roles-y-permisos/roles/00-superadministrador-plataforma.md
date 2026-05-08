---
titulo: "Rol: Superadministrador de la Plataforma"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, superadmin, global, plataforma]
---

# Rol: Superadministrador de la Plataforma

## Identificación

- **Nombre del rol:** Superadministrador de la Plataforma
- **Tipo de usuario asociado:** Personal técnico de la empresa que opera el SaaS (programadores / equipo interno)
- **Ámbito:** Plataforma (global, fuera de cualquier tenant)
- **Configurable por el colegio:** no (no existe en el contexto del colegio)
- **Tipo:** principal

## Descripción

Único rol que vive **por encima de todos los colegios**. Tiene acceso transversal a la plataforma para crear, configurar y mantener los tenants. No interviene en la operación académica diaria de ningún colegio: una vez crea el tenant, le entrega el acceso al Administrador del Colegio.

## Responsabilidades

- Crear nuevos tenants (colegios) en la plataforma.
- Asignar el plan de licencia contratado por cada tenant (básico, estándar, premium).
- Definir el subdominio o dominio de cada colegio.
- Realizar configuraciones técnicas iniciales del tenant (provisioning del schema, semillas base).
- Gestionar el almacenamiento asignado a cada tenant.
- Cambiar el calendario académico de un tenant entre Calendario A y Calendario B cuando aplique.
- Tener visibilidad global sobre el estado, métricas y salud de todos los colegios activos.
- Soporte de último nivel ante incidentes técnicos que requieren acceso cross-tenant.

## Scope / alcance de visibilidad

- Ve **todos los tenants** y todos los datos de la plataforma.
- Es el único actor con visibilidad cross-tenant. Cualquier acceso suyo a datos de un tenant queda registrado en el log de auditoría con motivo.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Crear tenant | Provisionar un colegio nuevo, generar su schema y semillas |
| Eliminar / suspender tenant | Por incumplimiento de contrato u otras razones administrativas |
| Asignar y cambiar plan de licencia | Básico, estándar, premium |
| Definir subdominio del tenant | Y cambiarlo si es necesario |
| Cambiar calendario A ↔ B del tenant | Solo este rol puede hacerlo |
| Gestionar cuotas de almacenamiento | Por tenant |
| Acceso a logs de auditoría globales | De todos los tenants |
| Impersonación / acceso de soporte | Acceso temporal al tenant para diagnóstico, siempre auditado |

## Permisos configurables por el colegio

Ninguno. Este rol vive fuera del tenant, por lo que ningún colegio puede ajustar sus permisos.

## Permisos explícitamente NO otorgados

- No registra ni edita notas de estudiantes.
- No registra asistencia ni observaciones disciplinarias.
- No emite documentos oficiales del colegio (constancias, certificados).
- No participa en la operación académica diaria.

## Reglas de asignación

- Solo el equipo interno de la empresa que opera el SaaS puede tener este rol.
- La asignación se hace fuera del flujo normal de creación de usuarios (no se asigna desde el portal de un colegio).
- Cantidad máxima por plataforma: pequeña, idealmente 2-5 personas. Definir política interna.

## Compatibilidad con otros roles

- Es un rol **exclusivo de plataforma**. Un Superadministrador no puede simultáneamente ser Rector, Docente o cualquier otro rol de tenant.
- Si una persona del equipo interno necesita actuar como rol de tenant, debe usar la vía de **impersonación** auditada, no asignarse el rol del tenant.

## Variantes según configuración del colegio

No aplica — este rol no depende de la configuración de ningún colegio.

## Notas y pendientes

- Definir política de impersonación: cuándo se permite, ventana de tiempo, notificación al admin del colegio.
- Definir política de retención de logs de acceso del Superadmin (deben conservarse por más tiempo que los logs comunes).
