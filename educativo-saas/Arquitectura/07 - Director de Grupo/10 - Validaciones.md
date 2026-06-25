---
tags:
  - arquitectura
  - rol/director-de-grupo
  - validaciones
aliases:
  - Validaciones ROL-08
---

# Validaciones — Director de Grupo

Casos de validacion y comportamiento del sistema para el complemento sobre el grupo dirigido.

> Las validaciones de captura de notas y asistencia del Docente viven en [[../06 - Docente/10 - Validaciones|Validaciones del Docente]]. Aqui solo lo adicional.

## Scope del grupo dirigido (RR-09)

| Caso | Comportamiento del Sistema |
|---|---|
| Intenta anotar / consolidar / generar boletin de un grupo que NO dirige | Bloquea; backend rechaza por scope; la UI no lista estudiantes ajenos (RR-02, RR-09) |
| Selecciona un estudiante que no pertenece al grupo dirigido | Bloquea; muestra "El estudiante no pertenece a tu grupo dirigido" |
| Dirige varios grupos y no selecciono cual | Bloquea la accion; pide elegir el grupo en el selector |

## Generar boletines (RF-38)

| Caso | Comportamiento del Sistema |
|---|---|
| Periodo academico aun abierto / sin cerrar notas | Advierte: "El periodo no esta cerrado; el boletin puede cambiar." No bloquea si el colegio lo permite, pero deja constancia |
| Faltan notas de una o mas materias | Advierte y lista las materias faltantes; exige marcar el checkbox de confirmacion para continuar |
| Estudiante retirado en el periodo | Genera el boletin marcado como "retirado"; no calcula promedios posteriores al retiro |
| No hay notas en ninguna materia | Bloquea; muestra "No hay notas registradas para generar el boletin" |

## Observacion general en boletin (RF-40)

| Caso | Comportamiento del Sistema |
|---|---|
| Observacion vacia o < 10 caracteres | Bloquea envio; muestra "La observacion debe tener al menos 10 caracteres" |
| Estudiante fuera del grupo dirigido | Bloquea; el select no ofrece estudiantes ajenos |
| Boletin del periodo ya firmado/cerrado | Bloquea edicion; muestra "El boletin ya fue firmado; solicita reapertura" |

## Anotacion en observador (RF-25)

| Caso | Comportamiento del Sistema |
|---|---|
| Descripcion vacia o < 10 caracteres | Bloquea envio; muestra "Describe el hecho (min 10 caracteres)" |
| Fecha del hecho en el futuro | Bloquea; muestra "La fecha del hecho no puede ser futura" |
| Evidencia supera el peso o tipo permitido | Bloquea la carga; muestra el limite; verifica cuota del tenant |
| Visibilidad no seleccionada | Bloquea; exige definir la visibilidad de la anotacion (RN-OB-081) |

## Convivencia (Ley 1620)

| Caso | Comportamiento del Sistema |
|---|---|
| Intenta clasificar el tipo (I/II/III) de la situacion | Bloquea; la clasificacion es del Coordinador de Convivencia (RN-CVE-002) |
| Marca "presunto delito" | No bloquea; escala automaticamente al Rector y restringe la visibilidad (RN-CVE-004) |
| Cierra un seguimiento con acuerdos sin registrar | Bloquea; exige registrar el resultado del seguimiento |
| Reporte sin estudiante del grupo | Bloquea; debe involucrar al menos un estudiante del grupo dirigido |

## Edicion de notas (configurable)

| Caso | Comportamiento del Sistema |
|---|---|
| Edita una nota de materia que no dicta y el permiso esta desactivado | Bloquea; muestra "No tienes permiso para editar notas que no dictas" |
| Edita tras el cierre sin justificacion (RF-17) | Bloquea; exige justificacion (min 10 caracteres) que queda en log (RR-07) |
| Nota fuera de la escala valorativa del colegio | Bloquea; muestra el rango valido segun la escala configurada |

## Citaciones y comunicacion (configurable)

| Caso | Comportamiento del Sistema |
|---|---|
| Cita un acudiente y el permiso esta desactivado | Bloquea la emision; ofrece "solicitar citacion al Coordinador" |
| Fecha/hora de citacion en el pasado | Bloquea; muestra "La fecha propuesta debe ser futura" |
| Mensaje a acudiente sin canal habilitado | Bloquea; muestra "No hay canal de comunicacion habilitado por el colegio" |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |
| El complemento fue retirado a mitad de sesion | Oculta los modulos adicionales; vuelve a la vista de Docente; registra el cambio |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../06 - Docente/10 - Validaciones|Validaciones del Docente (rol base)]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
