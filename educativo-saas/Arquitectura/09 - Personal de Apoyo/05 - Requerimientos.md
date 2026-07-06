---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - requerimientos
aliases:
  - Requerimientos ROL-12
---

# Requerimientos — Personal de Apoyo

RFs/RRs/RNFs aplicables a este rol. Filtrado de [[../_Globales/03 - Tabla de Requerimientos|Tabla de Requerimientos]].

> Este rol no introduce nuevos IDs RF/RR: reutiliza los RF transversales ya definidos y se gobierna por las reglas `RN-XX` de Logica (`RN-TU`, `RN-BW`, `RN-SA`, `RN-BI`, `RN-OB`). Los RF formales de los modulos de servicio (Bienestar/Salud/Biblioteca) se asignan de forma central.

## Operativas — Nucleo comun

| ID | Requerimiento | Prioridad |
|---|---|---|
| RF-48 | Consultar / aportar al observador (visibilidad `RN-OB-081`) | Alta |
| RF-43 | Comunicarse con el acudiente via portal (si el colegio lo habilita) | Media |
| RF-44 | Recibir notificaciones (remisiones, citas, vencimientos) | Alta |

## Operativas — Modulo de servicio (segun perfil)

Gobernadas por reglas `RN-XX` de Logica; sin IDs RF nuevos asignados aqui.

| Servicio | Capacidad | Regla base | Prioridad |
|---|---|---|---|
| Bienestar (`RN-BW`) | Abrir caso, agendar cita, registrar seguimiento, plan, remision | `RN-BW-001`..`RN-BW-010` | Alta |
| Salud (`RN-SA`) | Registrar atencion, suministrar medicamento, vacunas, remision | `RN-SA-001`..`RN-SA-009` | Alta |
| Biblioteca (`RN-BI`) | Catalogar, prestar, devolver, multar, reservar, inventariar | `RN-BI-001`..`RN-BI-010` | Alta |

## Reglas aplicables

| ID | Regla |
|---|---|
| `RN-TU-001` | Rol de permisos minimos |
| `RN-TU-002` | Sin acceso a notas ni configuracion |
| `RN-TU-003` | Perfil obligatorio antes de activar |
| `RN-TU-004` | Modulo de servicio segun perfil |
| `RN-TU-005` | Aporte al observador con visibilidad `RN-OB-081` (default interna) |
| `RN-TU-006` | Ficha acotada, no expediente completo |
| `RN-TU-007` | Incompatible con roles academicos/administrativos |
| `RN-TU-008` | Linea de reporte configurable |
| `RN-TU-009` | Auditoria de consultas y aportes |
| `RN-TU-010` | Remision, no decision |
| `RN-OB-081` | Visibilidad por anotacion (publica/docentes/interna) |
| RR-03 | Auditoria de acciones sensibles |
| RR-05 | Configurabilidad acotada de permisos |
| RR-06 | Acceso solo por subdominio del colegio |

## No funcionales

| ID | Requerimiento |
|---|---|
| RNF-01 | Aislamiento total entre tenants a nivel BD |
| RNF-02 | Trazabilidad: cada consulta de ficha y cada aporte queda auditado |
| RNF-03 | Seguridad: datos sensibles de salud y bienestar con acceso restringido |

## Relacionado

- [[04 - Permisos Detallados]]
- [[03 - PRD]]
- [[../_Globales/03 - Tabla de Requerimientos|Tabla de Requerimientos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
