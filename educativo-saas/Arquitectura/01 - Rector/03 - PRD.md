---
tags:
  - arquitectura
  - rol/rector
  - prd
aliases:
  - PRD-03
  - PRD Rector
---

# PRD — Rector / Administrador del Colegio

| Campo | Valor |
|---|---|
| ID PRD | PRD-03 |
| HU | Como Rector quiero configurar y administrar mi colegio para que la plataforma refleje su realidad academica, organizacional y normativa |
| Funcionalidad | Configuracion y gobierno integral del tenant (colegio) |
| Actor | ROL-02 Rector / Administrador del Colegio |
| Dispositivo | Desktop (configuracion y gestion); mobile para consulta y aprobaciones |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Dar al Rector el control total dentro de su colegio: configurar la identidad institucional, el calendario, la escala valorativa y el metodo de aprobacion; crear los usuarios y asignar roles; supervisar la operacion academica, de convivencia, de bienestar y financiera; y aprobar los actos que requieren su firma (boletines), todo con trazabilidad y sin acceso a otros tenants.

## Flujo General

```
Tenant creado por el Superadmin -> Primer ingreso del Rector
   -> Asistente de configuracion (identidad, calendario, jornadas, escala, aprobacion)
   -> Crear usuarios + asignar roles (RR-04) + ajustar permisos configurables (RR-05)
   -> Operacion del ano lectivo (academico + convivencia + bienestar + financiero)
   -> Cierres de periodo + aprobacion de boletines (RF-39)
   -> Reportes oficiales (SIMAT/MEN, RR-15) + monitoreo continuo via dashboard
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-04 | Configurar identidad institucional | Alta |
| RF-05 | Configurar calendario y periodos | Alta |
| RF-06 | Configurar jornadas y bloques horarios | Alta |
| RF-07 | Configurar escala valorativa | Alta |
| RF-08 | Configurar metodo de aprobacion y nota minima | Alta |
| RF-09 | Gestionar roles del tenant | Alta |
| RF-10 | Crear y editar usuarios | Alta |
| RF-20 | Coordinar cierre de periodo academico | Alta |
| RF-39 | Aprobar / firmar boletines | Alta |
| RF-49 | Acceder a logs de auditoria del tenant | Alta |
| RF-17 | Editar notas despues del cierre (con justificacion) | Media |
| RF-42 | Enviar comunicados al colegio entero | Media |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-01 | Aislamiento total entre tenants | El Rector solo ve datos de su colegio; nunca de otro | Alta |
| RR-02 | Verificacion de permisos frontend y backend | Sus acciones se validan en UI y backend | Alta |
| RR-03 | Auditoria de acciones sensibles | Configuracion, usuarios, roles, notas y firmas quedan en log inmutable | Alta |
| RR-04 | Asignacion de roles por el Rector | Solo el Rector asigna los roles internos del tenant | Alta |
| RR-05 | Configurabilidad acotada de permisos | Puede activar/desactivar configurables y renombrar; no crear permisos ni quitar estructurales | Alta |
| RR-06 | Acceso por subdominio del colegio | Entra por el subdominio del tenant, no por URL global | Alta |
| RR-07 | Notas se editan dentro del periodo abierto | Post-cierre requiere permiso configurable + justificacion | Alta |
| RR-08 | Bloqueo de documentos por pendientes | Configurable: bloquear constancias/paz y salvo con pendientes | Media |
| RR-12 | Coordinador combinado excluye los separados | El Rector elige el esquema de coordinacion del tenant | Media |
| RR-13 | Cambio de calendario A/B es del Superadmin | El Rector solo elige dentro del calendario habilitado | Media |
| RR-15 | Reporte SIMAT obligatorio | El colegio debe reportar matricula al MEN | Alta |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Crear o eliminar tenants | Es operacion de plataforma | Superadmin (ROL-01) |
| 2 | Cambiar el calendario A/B habilitado del tenant | Depende del plan contratado | Superadmin (ROL-01) (RR-13) |
| 3 | Acceder a datos de otros colegios | Aislamiento total | Nadie (excepcion auditada del Superadmin) |
| 4 | Impersonar a otro usuario | Trazabilidad / seguridad | Superadmin via impersonacion auditada |
| 5 | Crear permisos nuevos o quitarse permisos estructurales | Configurabilidad acotada | Nadie (RR-05) |
| 6 | Ver logs globales de plataforma | Solo ve los de su tenant | Superadmin (ROL-01) |

## Dependencias

- Tenant ya provisionado por el Superadmin (schema + semillas) antes del primer ingreso.
- Calendario habilitado por el plan (define si puede elegir A, B o ambos).
- Integraciones externas para operacion plena: SIMAT/MEN (RI-02), correo (RI-03), pasarelas (RI-01), DIAN (RI-05).
- Modulo de auditoria del tenant para trazar sus acciones (RR-03).
- Ver [[../_Globales/09 - Dependencias|Dependencias]].

## Relacionado

- [[00 - Arquitectura Rector|Wireframe]]
- [[05 - Requerimientos]]
- [[08 - Acciones del Usuario]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`
