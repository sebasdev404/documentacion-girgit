---
tags:
  - arquitectura
  - rol/superadmin
  - permisos
aliases:
  - Permisos ROL-01
---

# Permisos Detallados — Superadministrador de la Plataforma

Detalle granular de permisos del rol, modulo por modulo. Para la vista cruzada con otros roles ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Plataforma** | Crear tenant | Crear | Provisionar colegio nuevo, generar schema y semillas |
| **Plataforma** | Eliminar / suspender tenant | Editar | Por incumplimiento de contrato u otras razones administrativas |
| **Plataforma** | Asignar plan de licencia | Editar | Basico, estandar, premium |
| **Plataforma** | Definir subdominio del tenant | Editar | Cambiarlo si es necesario |
| **Plataforma** | Cambiar calendario A/B del tenant | Editar | Unico rol con este permiso |
| **Plataforma** | Gestionar cuotas de almacenamiento | Editar | Por tenant |
| **Plataforma** | Acceso a logs de auditoria globales | Ver | De todos los tenants |
| **Plataforma** | Impersonacion / acceso de soporte | Ver | Acceso temporal al tenant para diagnostico, siempre auditado |

## Permisos configurables por el colegio

Ninguno. Este rol vive fuera del tenant.

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Registrar/editar notas de estudiantes | No participa en operacion academica |
| Registrar asistencia u observaciones | No participa en operacion academica |
| Emitir documentos oficiales del colegio | Es responsabilidad de Secretaria (ROL-06) |
| Aprobar boletines | Es responsabilidad del colegio |

## Reglas asociadas

- RR-01 Aislamiento total entre tenants — excepcion auditada para soporte.
- RR-03 Auditoria de acciones sensibles — sus accesos cross-tenant deben registrarse con motivo.
- RR-13 Cambio de calendario A/B solo por Superadmin.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma.md`
