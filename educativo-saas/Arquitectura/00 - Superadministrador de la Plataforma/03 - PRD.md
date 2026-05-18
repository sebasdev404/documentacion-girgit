---
tags:
  - arquitectura
  - rol/superadmin
  - prd
aliases:
  - PRD-02
  - PRD Superadmin
---

# PRD — Superadministrador de la Plataforma

| Campo | Valor |
|---|---|
| ID PRD | PRD-02 |
| HU | Como superadmin quiero provisionar y mantener los colegios de la plataforma |
| Funcionalidad | Gestion cross-tenant del SaaS |
| Actor | ROL-01 Superadministrador de la Plataforma |
| Dispositivo | Desktop (panel de plataforma) |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Permitir que el equipo interno del SaaS cree, configure y mantenga los tenants (colegios) de forma rapida y segura, con trazabilidad total de cada accion privilegiada, sin participar en la operacion academica diaria de ningun colegio.

## Flujo General

```
Contrato firmado -> Crear tenant -> Provisioning automatico (schema + semillas)
   -> Asignar plan + subdominio + calendario -> Entregar acceso al Rector
   -> Monitoreo continuo (salud, cuotas, backups, incidentes)
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-01 | Crear tenant | Alta |
| RF-02 | Asignar plan de licencia | Alta |
| RF-03 | Cambiar calendario A/B del tenant | Media |
| RF-50 | Acceder a logs globales de plataforma | Alta |
| CU-001 | Onboardear nuevo colegio (ver `Logica del negocio/08-casos-de-uso/CU-001`) | Alta |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-01 | Aislamiento total entre tenants | Excepcion auditada para soporte | Alta |
| RR-03 | Auditoria de acciones sensibles | Sus accesos cross-tenant quedan registrados con motivo | Alta |
| RR-06 | Acceso por subdominio | El superadmin entra por URL de plataforma, no por subdominio | Alta |
| RR-13 | Cambio calendario A/B es del Superadmin | Unico rol que puede | Media |
| RN-RT-402 | Impersonacion exclusiva del superadmin | Ticket + justificacion + expiracion + banner + doble identificador | Alta |
| RN-LA-002 | Accion privilegiada doblemente auditada | Acciones sobre el tenant se notifican al Rector | Alta |
| RN-RT-401 | Retencion diferenciada de logs | Logs del superadmin con retencion extendida | Media |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Registrar / editar notas | No participa en operacion academica | Docente (ROL-07) |
| 2 | Emitir documentos oficiales | Responsabilidad del colegio | Secretaria (ROL-06) |
| 3 | Aprobar boletines | Responsabilidad del colegio | Rector / Coordinador |
| 4 | Operar un tenant como rol interno sin impersonacion | Trazabilidad | Solo via impersonacion auditada |

## Dependencias

- Provisioning de schema PostgreSQL por tenant.
- Integraciones externas (pasarelas, correo, SMS) para el panel de salud.
- Modulo de log de auditoria global (`Logica del negocio/11-plataforma-y-operacion/log-de-auditoria.md`).
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
