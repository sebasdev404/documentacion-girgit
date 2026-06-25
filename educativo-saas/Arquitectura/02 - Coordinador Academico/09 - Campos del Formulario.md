---
tags:
  - arquitectura
  - rol/coord-academico
  - formularios
aliases:
  - Campos Formulario ROL-03
---

# Campos del Formulario — Coordinador Academico

Campos de cada formulario que opera el rol.

## A) Formulario "Crear / editar materia del plan" (RF-11)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre de la materia | Texto | Si | Min 3 caracteres, unica por grado | Ej. Matematicas, Lengua Castellana |
| Area del conocimiento | Select | Si | Lista de areas configuradas | Agrupa materias afines |
| Grado(s) | Multi-select | Si | Al menos un grado | Grados a los que aplica la materia |
| Intensidad horaria semanal | Numero | Si | > 0, entero | Horas de clase por semana |
| Estado | Select | Si | Activa / Archivada | Solo se archiva si no esta en grupos activos |

## B) Formulario "Crear / editar grupo" (RF-12)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grado | Select | Si | Grado existente del plan | Grado al que pertenece el grupo |
| Nombre del grupo | Texto | Si | Unico dentro del grado y ano | Ej. 6A, 6B |
| Jornada | Select | Si | Jornada configurada por el Rector | Manana / Tarde / Unica |
| Ano lectivo | Select | Si | Ano lectivo activo | Periodo anual del grupo |
| Capacidad maxima | Numero | No | > 0 | Cupo del grupo |

## C) Formulario "Asignar docente / designar director de grupo" (RF-13, RF-14)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo | Select | Si | Grupo existente | Grupo a asignar |
| Materia | Select | Si | Materia del plan del grado | Materia a cubrir |
| Docente | Select | Si | Docente activo del tenant | Titular de la materia (RR-10) |
| Designar como director de grupo | Checkbox | No | Solo un director por grupo | Activa el complemento Director de Grupo (RR-09) |

## D) Formulario "Crear / editar bloque de horario" (RF-15)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo | Select | Si | Grupo existente | Grupo del bloque |
| Dia | Select | Si | Dia habil de la jornada | Lunes a viernes (segun config.) |
| Bloque horario | Select | Si | Bloque definido por el Rector | Franja horaria |
| Materia | Select | Si | Materia asignada al grupo | Materia del bloque |
| Docente | Auto / Select | Si | Docente asignado a esa materia/grupo | Se infiere de la asignacion |
| Aula | Select | Si | Aula libre en ese bloque | Sin cruce de aula |

## E) Formulario "Activar / reabrir cierre de periodo" (RF-20)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Periodo | Select | Si | Periodo lectivo del calendario | Periodo a cerrar/reabrir |
| Confirmacion | Checkbox | Si | Debe marcarse | "Entiendo que esto congela las notas del periodo" |
| Motivo (solo al reabrir) | Texto largo | Si (al reabrir) | Min 10 caracteres | Queda en log (RR-07) |

## F) Formulario "Abrir proceso de nivelacion / habilitacion" (RF-21)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante con materia perdida | Sujeto del proceso |
| Materia | Select | Si | Materia perdida del estudiante | Materia a nivelar |
| Tipo de proceso | Select | Si | Nivelacion / Habilitacion | Segun reglamento del colegio |
| Docente responsable | Select | Si | Docente activo | Quien evalua la nivelacion |
| Fecha limite | Fecha | Si | >= hoy | Plazo del proceso |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
