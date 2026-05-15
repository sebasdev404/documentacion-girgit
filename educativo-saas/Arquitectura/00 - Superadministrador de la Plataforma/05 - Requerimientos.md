---
tags:
  - arquitectura
  - rol/superadmin
  - requerimientos
aliases:
  - Requerimientos ROL-01
---

# Requerimientos — Superadministrador de la Plataforma

RFs/RRs/RNFs aplicables a este rol. Filtrado de [[../_Globales/03 - Tabla de Requerimientos|Tabla de Requerimientos]].

## Operativas — Plataforma

| ID | Requerimiento | Prioridad |
|---|---|---|
| RF-01 | Crear tenant | Alta |
| RF-02 | Asignar plan de licencia | Alta |
| RF-03 | Cambiar calendario A/B del tenant | Media |
| RF-50 | Acceder a logs globales de plataforma | Alta |

## Reglas aplicables

| ID | Regla |
|---|---|
| RR-01 | Aislamiento total entre tenants (con excepcion auditada) |
| RR-03 | Auditoria de acciones sensibles (sus accesos cross-tenant deben quedar registrados) |
| RR-13 | Cambio de calendario A/B es del Superadmin |

## No funcionales

| ID | Requerimiento |
|---|---|
| RNF-01 | Aislamiento total entre tenants a nivel BD |
| RNF-05 | Disponibilidad >= 99.5% |
| RNF-06 | Backup automatico diario por tenant |
