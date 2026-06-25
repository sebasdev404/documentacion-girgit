---
tags:
  - arquitectura
  - rol/coord-academico
  - prd
aliases:
  - PRD-04
  - PRD Coord. Academico
---

# PRD — Coordinador Academico

| Campo | Valor |
|---|---|
| ID PRD | PRD-04 |
| HU | Como Coordinador Academico quiero organizar y mantener la estructura academica del colegio (plan, grupos, horarios, notas y cierres) sin tocar la configuracion base |
| Funcionalidad | Gestion de la operacion academica del tenant |
| Actor | ROL-03 Coordinador Academico |
| Dispositivo | Desktop (portal del colegio por subdominio) |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Permitir que el Coordinador Academico organice toda la operacion academica del colegio —plan de estudios, grupos, asignacion docente, horarios, consolidados, cierres de periodo y nivelaciones— de forma ordenada y trazable, dentro de los limites de la configuracion base que define el Rector, sin acceder al observador disciplinario ni a la emision de documentos oficiales.

## Flujo General

```
Inicio de ano lectivo -> Armar plan de estudios -> Crear grupos por grado
   -> Asignar docentes a materias + designar directores de grupo
   -> Construir y publicar horarios (validar cruces)
   -> Durante el periodo: revisar consolidados y detectar riesgo
   -> Cierre de periodo (validar consolidados, activar cierre)
   -> Generar / aprobar boletines -> Abrir nivelaciones de materias perdidas
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-11 | Gestionar plan de estudios | Alta |
| RF-12 | Crear y gestionar grupos | Alta |
| RF-13 | Asignar docentes a materias y grupos | Alta |
| RF-14 | Designar director de grupo | Alta |
| RF-15 | Construir horarios de clase | Alta |
| RF-17 | Editar notas despues del cierre (configurable) | Media |
| RF-18 | Ver consolidados de notas por grupo | Alta |
| RF-19 | Ver consolidado de todos los grupos | Media |
| RF-20 | Cierre de periodo academico | Alta |
| RF-21 | Gestion de nivelaciones y habilitaciones | Media |
| RF-39 | Aprobar / firmar boletines (configurable) | Alta |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-01 | Aislamiento total entre tenants | Solo ve datos de su propio colegio | Alta |
| RR-03 | Auditoria de acciones sensibles | Cierres, edicion de notas y asignaciones quedan registrados | Alta |
| RR-04 | Asignacion de roles por el Rector | Su rol lo asigna el Rector del tenant | Alta |
| RR-05 | Configurabilidad acotada de permisos | Edicion de notas, aprobacion de boletines, etc. son permisos configurables, no nuevos | Alta |
| RR-06 | Acceso por subdominio | Entra por el subdominio del colegio, no por URL de plataforma | Alta |
| RR-07 | Notas se editan dentro del periodo abierto | Tras el cierre, editar notas requiere permiso configurable + justificacion | Alta |
| RR-09 | Director de Grupo solo opera sobre su grupo | La designacion activa permisos solo sobre el grupo dirigido | Media |
| RR-10 | Docente ve solo lo asignado | La asignacion docente determina la visibilidad del docente | Alta |
| RR-12 | Coordinador combinado excluye los separados | Si el colegio usa el rol combinado, no usa ROL-03 + ROL-04 | Media |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Modificar la configuracion base (escala, jornadas, modelo pedagogico, calendario) | Es la base del sistema academico del colegio | Rector (ROL-02) |
| 2 | Acceder al observador disciplinario | Es competencia de convivencia | Coord. de Convivencia (ROL-04) o combinado (ROL-05) |
| 3 | Emitir documentos oficiales (constancias, certificados, paz y salvos, SIMAT) | Responsabilidad legal de la institucion | Secretaria (ROL-06) |
| 4 | Editar notas directamente (por defecto) | El titular de la nota es el docente | Docente (ROL-07); o el Coordinador si el colegio activa el permiso (RR-05, RR-07) |
| 5 | Acceder a datos de otros tenants | Aislamiento por colegio | Nadie (excepto Superadmin auditado, RR-01) |
| 6 | Acceder a los logs de auditoria del tenant | La consulta de auditoria del colegio es del Rector | Rector (ROL-02) |

## Dependencias

- Configuracion base del tenant (escala valorativa, jornadas, calendario, periodos) definida por el Rector — sin ella no se pueden construir horarios ni cerrar periodos.
- Matricula de estudiantes y carga de docentes (Secretaria / Rector) para crear grupos y asignar.
- Modulo de Notas (carga de docentes) para alimentar consolidados y cierres.
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
