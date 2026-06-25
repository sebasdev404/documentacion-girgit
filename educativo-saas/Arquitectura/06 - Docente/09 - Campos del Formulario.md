---
tags:
  - arquitectura
  - rol/docente
  - formularios
aliases:
  - Campos Formulario ROL-07
---

# Campos del Formulario — Docente

Campos de cada formulario que opera el rol. Todos operan dentro del alcance de SUS grupos y materias asignados (RR-10).

## A) Formulario "Registrar / editar nota" (RF-16)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo | Select | Si | Solo grupos asignados al docente | Grupo donde dicta la materia |
| Materia | Select | Si | Solo materias asignadas en ese grupo | Materia que se califica |
| Periodo | Select | Si | Debe estar abierto (RR-07) | Periodo lectivo de la nota |
| Evaluacion | Select | Si | Evaluacion existente del periodo | Examen, taller, quiz, etc. |
| Estudiante | Auto (fila de planilla) | Si | Inscrito en el grupo | Estudiante a calificar |
| Nota | Numero / Imagen | Si | Dentro de la escala valorativa configurada por el Rector | Valor en escala numerica o por imagenes (preescolar) |
| Justificacion | Texto largo | Condicional | Obligatoria solo si edita con periodo cerrado y el permiso esta activo | Motivo del cambio post-cierre |

## B) Formulario "Registrar asistencia" (RF-22)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo | Select | Si | Solo grupos asignados | Grupo de la clase |
| Materia | Select | Si | Solo materias asignadas | Materia de la clase |
| Fecha | Fecha | Si | <= hoy; coherente con el horario | Dia de la clase |
| Estado por estudiante | Radio (P/A/T/E) | Si | Un estado por estudiante | Presente / Ausente / Tarde / Excusa |
| Nota de excusa | Texto | Condicional | Requerido solo si el estado es Excusa | Detalle de la excusa |

## C) Formulario "Observacion academica" (RF-24)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | De un grupo asignado | Estudiante observado |
| Materia | Select | Si | Materia asignada | Materia a la que aplica la observacion |
| Tipo | Select | Si | Catalogo academico (no disciplinario) | Avance, dificultad, compromiso, felicitacion |
| Descripcion | Texto largo | Si | Min 10 caracteres | Detalle de la observacion |
| Visibilidad | Select | Si | Segun configuracion del colegio | Quien puede ver la anotacion |

## D) Formulario "Cargar evidencia" (configurable)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Evaluacion | Select | Si | Evaluacion existente | A que evaluacion se asocia |
| Archivo | Archivo | Si | Tipo y peso permitidos; dentro de cuota del tenant | PDF/imagen de la evidencia |
| Descripcion | Texto | No | — | Nota sobre la evidencia |

## E) Formulario "Reportar situacion de convivencia"

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante(s) involucrado(s) | Select multiple | Si | De un grupo asignado | Estudiantes del hecho |
| Fecha y lugar | Fecha + Texto | Si | <= hoy | Cuando y donde ocurrio |
| Descripcion de los hechos | Texto largo | Si | Min 20 caracteres | Relato del docente |
| Medida pedagogica aplicada | Texto | No | — | Accion inmediata en aula (tipo I) |
| Marcar presunto delito | Checkbox | No | Si se marca, escala al Rector (RN-CVE-004) | Escalamiento inmediato y visibilidad restringida |

> El docente NO captura el tipo (I/II/III) del caso: esa clasificacion la hace el Coordinador de Convivencia (RN-CVE-002).

## F) Formulario "Remitir a enfermeria"

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | De un grupo asignado | Estudiante a remitir |
| Motivo | Texto | Si | Min 5 caracteres | Por que lo remite |
| Urgencia | Select | Si | Normal / Prioritaria | Severidad percibida |

## G) Formulario "Mensaje a acudiente" (RF-43, configurable)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | De un grupo asignado | Define el acudiente destinatario |
| Asunto | Texto | Si | Min 3 caracteres | Tema del mensaje |
| Mensaje | Texto largo | Si | Min 5 caracteres | Cuerpo de la comunicacion |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
