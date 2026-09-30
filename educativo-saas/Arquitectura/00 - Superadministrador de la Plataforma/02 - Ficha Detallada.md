---
tags:
  - arquitectura
  - rol/superadmin
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-01
---

# Ficha Detallada — Superadministrador de la Plataforma

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-01 |
| Nombre | Superadministrador de la Plataforma |
| Alias | Superadmin, SA |
| Tipo | Principal — Global (fuera de cualquier tenant) |
| Tipo de usuario | Personal tecnico de la empresa que opera el SaaS |
| Reporta a | Direccion de la empresa (fuera del producto) |
| Supervisa a | Todos los tenants y sus Rectores |
| Ambito de datos | Cross-tenant (todos los colegios) |
| Cantidad sugerida | 2 a 5 personas (politica interna) |
| Como se asigna | Fuera del flujo de usuarios del tenant (provisioning interno) |
| Modulos que usa | Dashboard global, Tenants, Planes, Calendario A/B, Almacenamiento, Backups, Log global, Soporte/Impersonacion, Salud del sistema |
| Permisos CRUD | Tenants: CRUD · Planes: asignar/editar · Calendario A/B: editar · Cuotas: editar · Logs globales: ver · Impersonacion: si (auditada) |
| Permisos negados | Notas, asistencia, observador, boletines, documentos oficiales, operacion academica |
| MFA | Opcional; si se activa, se exige código al iniciar sesión |
| Acceso | URL de plataforma (no subdominio de colegio) |
| Dispositivo | Desktop (panel administrativo) |
| Frecuencia de uso | Esporadica; picos al crear tenants o ante incidentes |
| Dolor / Necesidad actual | Necesita visibilidad global de salud y estado de todos los colegios; provisioning rapido y seguro de tenants nuevos; trazabilidad total de sus propias acciones |
| Notas UX / Recomendaciones | Confirmaciones fuertes con motivo en acciones irreversibles (eliminar/suspender tenant, restaurar backup); banner permanente durante impersonacion; doble verificacion para cambio de calendario A/B |
| Reglas asociadas | RR-01, RR-03, RR-06, RR-13, RN-RT-400, RN-RT-401, RN-RT-402, RN-LA-002, RN-LA-006 |

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Abuso de acceso cross-tenant | Toda accion auditada con motivo; notificacion al Rector (RN-LA-002) |
| Impersonacion indebida | Ticket + justificacion + expiracion + banner + doble identificador (RN-RT-402) |
| Eliminacion accidental de tenant | Confirmacion fuerte + motivo + retencion de logs antes de borrado |
| Cambio erroneo de calendario | Doble confirmacion + motivo; solo este rol (RR-13) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma.md`
