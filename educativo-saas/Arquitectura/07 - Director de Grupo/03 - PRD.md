---
tags:
  - arquitectura
  - rol/director-de-grupo
  - prd
aliases:
  - PRD-09
  - PRD Director de Grupo
---

# PRD — Director de Grupo

| Campo | Valor |
|---|---|
| ID PRD | PRD-09 |
| HU | Como director de grupo quiero acompanar a mi grupo, consolidar sus notas, generar boletines y dar seguimiento a su convivencia |
| Funcionalidad | Complemento de acompanamiento sobre un grupo dirigido (se suma al rol Docente) |
| Actor | ROL-08 Director de Grupo (complemento de ROL-07 Docente) |
| Dispositivo | Mobile + desktop |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Dar al docente designado como titular de un grupo una vista y un conjunto de acciones adicionales **sobre ese grupo** para acompanarlo durante el ano lectivo: ver el consolidado completo de notas (todas las materias, no solo las que dicta), generar y observar los boletines, registrar anotaciones en el observador, y reportar y dar seguimiento a las situaciones de convivencia de su grupo, todo con trazabilidad auditable y sin salir del aislamiento de su tenant ni de su grupo (RR-09).

## Alcance

- **Incluye:** consolidado completo del grupo dirigido; generacion y observacion general de boletines; observador disciplinario del grupo; consulta de asistencia del grupo; reporte de convivencia y medidas tipo I; seguimiento de acuerdos; citaciones y comunicacion con acudientes (configurables).
- **Fuera del alcance:** clasificar el tipo de una situacion de convivencia (Coord. de Convivencia); decidir situaciones tipo III (Rector); configuracion del colegio; gestion de usuarios y roles; emision de documentos oficiales; matricula; operar otros grupos como director (RR-09). El comportamiento como Docente sobre sus materias se documenta en el PRD del Docente.

## Flujo General

```
Coord. Academico designa al docente como Director de Grupo
   -> El docente recibe el complemento ROL-08 sobre ese grupo
   -> Acompanamiento diario: consolidado, asistencia, observador, convivencia del grupo
   -> Cierre de periodo: revisa consolidado -> genera boletines -> observacion general -> entrega
   -> Seguimiento: acuerdos de convivencia, citaciones, comunicacion con acudientes
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-18 | Ver consolidado completo de notas del grupo dirigido | Alta |
| RF-23 | Consultar asistencia del grupo dirigido | Alta |
| RF-25 | Registrar anotacion en el observador del grupo dirigido | Alta |
| RF-38 | Generar boletin del grupo dirigido | Alta |
| RF-40 | Agregar observacion general en el boletin | Media |
| RF-39 | Aprobar / firmar boletines del grupo (configurable) | Alta |
| RF-17 | Editar notas despues del cierre (configurable) | Media |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-09 | Director de Grupo solo opera sobre su grupo | Los permisos extra del complemento aplican unicamente sobre el grupo dirigido; en otros grupos sigue siendo solo Docente | Alta |
| RR-07 | Notas dentro del periodo abierto | Editar notas tras el cierre exige permiso configurable + justificacion | Alta |
| RR-10 | Docente ve solo lo asignado | Como Docente solo ve materias/grupos asignados; el consolidado completo es exclusivo del grupo que dirige | Alta |
| RR-11 | El menor tiene una unica cuenta (Estudiante) | No existe rol Acudiente como usuario; el director se comunica con el acudiente que opera la cuenta del Estudiante | Media |
| RN-CVE-003 | Protocolo segun el tipo | El director aplica medidas tipo I; no instancia ni salta actuaciones de tipos superiores | Alta |
| RN-CVE-004 | Tipo III escala al Rector | Si el director marca presunto delito, el sistema escala al Rector y restringe la visibilidad | Alta |
| RN-CVE-007 | Articulacion con el observador | Todo acuerdo o medida de convivencia genera la anotacion correspondiente en el observador | Media |
| RN-OB-081 | Visibilidad por anotacion | Las anotaciones respetan la visibilidad configurada; el acudiente ve solo lo que le corresponde | Alta |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Operar otro grupo como director | Sus permisos extra son solo sobre el grupo dirigido (RR-09) | El director de ese otro grupo |
| 2 | Editar notas de materias que no dicta (por defecto) | Permiso configurable, desactivado por defecto | El docente titular de la materia; el director si el colegio lo activa |
| 3 | Clasificar el tipo (I/II/III) de una situacion | La tipificacion es del Coord. de Convivencia | Coord. de Convivencia (ROL-04) / combinado (ROL-05) |
| 4 | Decidir o cerrar una situacion tipo III | Constituye presunto delito y la decide el Rector | Rector (ROL-02) |
| 5 | Acceder a configuracion del colegio | Es del Rector | Rector (ROL-02) |
| 6 | Emitir documentos oficiales (constancias, certificados) | Responsabilidad de la Secretaria | Secretaria (ROL-06) |
| 7 | Citar acudientes formalmente (si no esta activado) | Puede ser potestad del Coord. de Convivencia | Coord. de Convivencia; el director si el colegio lo activa |

## Dependencias

- Rol base Docente (ROL-07): el complemento se monta sobre el (ver [[../06 - Docente/03 - PRD|PRD Docente]]).
- Modulo de consolidados y boletines (`Logica del negocio/04-procesos-academicos/`).
- Modulo de observador del estudiante (`Logica del negocio/04-procesos-academicos/observador-del-estudiante.md`).
- Modulo de convivencia Ley 1620 (`Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`).
- Log de auditoria del tenant (RR-03).
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
