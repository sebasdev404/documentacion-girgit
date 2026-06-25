---
tags:
  - arquitectura
  - rol/director-de-grupo
  - formularios
aliases:
  - Campos Formulario ROL-08
---

# Campos del Formulario — Director de Grupo

Campos de cada formulario que opera el complemento sobre el grupo dirigido.

> Los formularios de Docente (captura de notas, registro de asistencia de sus clases) viven en [[../06 - Docente/09 - Campos del Formulario|Campos del Docente]]. Aqui solo lo adicional.

## A) Formulario "Observacion general en boletin" (RF-40)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del grupo dirigido | A quien se le escribe la observacion |
| Periodo | Select | Si | Periodo lectivo del boletin | A que boletin aplica |
| Observacion general | Texto largo | Si | Min 10 caracteres | Fortalezas, compromisos y recomendaciones |
| Visibilidad para el acudiente | Toggle | No | Default visible | Si la observacion aparece en el boletin del acudiente |

## B) Formulario "Anotacion en observador del grupo" (RF-25)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del grupo dirigido (RR-09) | A quien se le registra |
| Tipo de anotacion | Select | Si | Tipologia configurada por el colegio | Clasifica la anotacion |
| Fecha del hecho | Fecha | Si | <= hoy | Cuando ocurrio |
| Descripcion | Texto largo | Si | Min 10 caracteres | Relato de los hechos |
| Evidencia | Archivo | No | Tipo y peso permitidos (sujeto a cuota) | Soporte adjunto |
| Visibilidad | Select | Si | Segun catalogo (RN-OB-081) | Quien puede ver la anotacion |
| Requiere confirmacion del acudiente | Checkbox | No | — | Notifica al acudiente para firma/lectura |

## C) Formulario "Generar boletines del grupo" (RF-38)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo dirigido | Select | Si | Solo grupos que dirige | Grupo objetivo |
| Periodo | Select | Si | Periodo con notas cerradas | Periodo del boletin |
| Alcance | Radio | Si | Todo el grupo / estudiante puntual | A quienes generar |
| Confirmacion de notas faltantes | Checkbox | Condicional | Obligatorio solo si hay faltantes | "Entiendo que hay materias sin nota" |

## D) Formulario "Reportar situacion de convivencia" (Ley 1620)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante(s) involucrado(s) | Multi-select | Si | Estudiantes del grupo dirigido | Generadores y/o afectados |
| Fecha del hecho | Fecha | Si | <= hoy | Cuando ocurrio |
| Descripcion de la situacion | Texto largo | Si | Min 20 caracteres | Relato de lo sucedido |
| Medida tipo I aplicada en el aula | Texto largo | No | — | Medida pedagogica inmediata, si aplica |
| Marcar como presunto delito | Checkbox | No | Si se marca, escala al Rector (RN-CVE-004) | Para situaciones graves |
| Evidencia | Archivo | No | Tipo y peso permitidos | Soporte adjunto |

## E) Formulario "Citar acudiente" (configurable)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del grupo dirigido | Por quien se cita |
| Motivo | Texto largo | Si | Min 10 caracteres | Razon de la citacion |
| Fecha y hora propuesta | Fecha/Hora | Si | >= hoy | Cuando se cita |
| Canal de notificacion | Select | Si | Canal habilitado por el colegio | Correo / portal / WhatsApp |

## F) Formulario "Mensaje a acudiente" (configurable)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del grupo dirigido | Acudiente destinatario (opera la cuenta del estudiante, RR-11) |
| Plantilla | Select | No | Catalogo del colegio | Comunicado pre-armado opcional |
| Mensaje | Texto largo | Si | Min 5 caracteres | Contenido del mensaje |

## G) Formulario "Editar nota fuera de scope / tras cierre" (configurable, RF-17)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante / materia | Select | Si | Del grupo dirigido | Que nota se edita |
| Nueva nota | Numero / Imagen | Si | Dentro de la escala valorativa del colegio | Valor a aplicar |
| Justificacion | Texto largo | Si | Min 10 caracteres | Obligatoria; queda en log (RR-07, RR-09) |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
- [[../06 - Docente/09 - Campos del Formulario|Campos del Docente (rol base)]]
