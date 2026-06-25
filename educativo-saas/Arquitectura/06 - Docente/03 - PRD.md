---
tags:
  - arquitectura
  - rol/docente
  - prd
aliases:
  - PRD-08
  - PRD Docente
---

# PRD — Docente

| Campo | Valor |
|---|---|
| ID PRD | PRD-08 |
| HU | Como docente quiero registrar notas, asistencia y observaciones de mis estudiantes en las materias que dicto, desde el aula |
| Funcionalidad | Operacion academica de aula dentro de un tenant |
| Actor | ROL-07 Docente |
| Dispositivo | Mobile + Desktop (mobile predominante en clase) |
| Estado | Borrador |
| Version | 0.1 |

## Objetivo

Permitir que el docente opere su aula de forma rapida y sin fricciones: registrar y editar notas dentro del periodo abierto, tomar asistencia en cada clase y dejar observaciones academicas por estudiante, siempre limitado a los grupos y materias que el Coordinador Academico le asigno explicitamente, sin acceso a la operacion academica del resto del colegio.

## Flujo General

```
Inicia jornada -> Home con clases del dia
   -> Toma asistencia por clase
   -> Tras evaluacion: carga notas (periodo abierto)
   -> Sistema recalcula acumulado del estudiante
   -> Deja observacion academica si aplica
   -> Reporta a enfermeria / convivencia si ocurre un evento
   -> Cierre de periodo: el sistema bloquea edicion de notas (RR-07)
```

## Casos de Uso

| ID | Caso | Prioridad |
|---|---|---|
| RF-16 | Registrar y editar notas en materia asignada | Alta |
| RF-22 | Registrar asistencia en clase propia | Alta |
| RF-24 | Registrar observacion academica en su materia | Alta |
| RF-46 | Consultar horario propio | Alta |
| RF-43 | Comunicarse con acudientes via portal (configurable) | Media |
| RF-44 | Recibir notificaciones por correo | Alta |

## Reglas de Negocio Aplicables

| ID | Regla | Descripcion | Prioridad |
|---|---|---|---|
| RR-01 | Aislamiento total entre tenants | No accede a datos de otro colegio | Alta |
| RR-02 | Verificacion de permisos frontend y backend | Cada accion se valida en UI y en backend | Alta |
| RR-03 | Auditoria de acciones sensibles | Notas, asistencia y observaciones registran quien/que/cuando | Alta |
| RR-06 | Acceso por subdominio | Entra por el subdominio de su colegio | Alta |
| RR-07 | Notas dentro del periodo abierto | Tras el cierre, editar exige permiso configurable + justificacion | Alta |
| RR-09 | Director de Grupo solo opera sobre su grupo | Si tiene el complemento, los permisos extra son solo del grupo dirigido | Media |
| RR-10 | Docente ve solo grupos y materias asignados | Aislamiento de visibilidad dentro del tenant | Alta |
| RN-CVE-002 | Clasificacion de convivencia es del Coordinador | El docente reporta; no clasifica tipo I/II/III | Media |
| RN-SA-007 | Alertas de salud visibles a docentes solo con autorizacion | El docente ve solo lo que el acudiente autoriza, nunca la ficha completa | Media |

## Restricciones / Permisos

| # | Accion que NO puede hacer | Por que | Quien SI puede |
|---|---|---|---|
| 1 | Ver consolidados generales del grupo | Solo ve su materia (RR-10) | Director de Grupo / Coordinador |
| 2 | Editar notas de materias que no dicta | Aislamiento por asignacion (RR-10) | Coordinador (segun esquema) |
| 3 | Editar notas con el periodo cerrado | Integridad del periodo (RR-07) | Rector / Coordinador (o docente si el colegio activa el permiso) |
| 4 | Acceder al observador disciplinario | Es de convivencia | Coord. de Convivencia / Director de Grupo |
| 5 | Clasificar un caso de convivencia | Decision reglada por ley | Coord. de Convivencia (RN-CVE-002) |
| 6 | Emitir documentos oficiales | Responsabilidad de secretaria | Secretaria (ROL-06) |
| 7 | Aprobar/firmar boletines | Responsabilidad directiva | Rector / Coordinador |
| 8 | Modificar la configuracion del colegio | Responsabilidad del Rector | Rector (ROL-02) |
| 9 | Ver la ficha medica completa de un estudiante | Dato sensible restringido (RN-SA-002) | Personal de Apoyo / enfermeria |

## Dependencias

- Asignacion de grupos y materias por el Coordinador Academico (RF-13).
- Escala valorativa, periodos y metodo de aprobacion configurados por el Rector (RF-05, RF-07, RF-08).
- Modulo de notificaciones (correo) para RF-44 (RI-03).
- Activacion opcional del modulo de evidencias, salud/enfermeria y mensajeria con acudientes.
- Ver [[../_Globales/09 - Dependencias|Dependencias]].
