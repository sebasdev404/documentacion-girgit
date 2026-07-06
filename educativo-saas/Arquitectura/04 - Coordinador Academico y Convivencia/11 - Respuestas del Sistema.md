---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-05
---

# Respuestas del Sistema — Coordinador Academico y Convivencia

Que responde el sistema ante cada evento.

## Eventos academicos

| Evento | Respuesta del Sistema |
|---|---|
| El coordinador crea una materia | Agrega la materia al plan del grado · la habilita para grupos y horarios · registra en log |
| El coordinador asigna un docente a materia x grupo | Habilita al docente para ver ese grupo y materia (RR-10) · refleja la asignacion en horarios, notas y asistencia · registra en log |
| El coordinador designa un director de grupo | Otorga al docente el complemento sobre ese grupo (RR-09) · habilita boletines y observador del grupo · notifica al docente · registra en log |
| El coordinador detecta un choque al armar horario | Bloquea la publicacion · resalta el conflicto (docente o aula) · no guarda el bloque en conflicto |
| El coordinador publica un horario | Lo hace visible a docentes y estudiantes del grupo · notifica a los afectados · registra en log |
| El coordinador ejecuta el cierre de un periodo | Congela las notas del periodo · genera automaticamente las nivelaciones de los reprobados (RN-NH-001) · habilita la generacion de boletines · notifica a docentes y directores · registra en log |
| El coordinador edita una nota tras el cierre | Verifica el permiso configurable · exige justificacion (RR-07) · aplica el cambio · guarda el antes/despues en log |
| El coordinador aprueba un boletin | Marca el boletin como aprobado · lo habilita para publicacion a acudientes · registra en log |
| Un docente registra la nota de una nivelacion | Evalua aprobado/no aprobado segun la configuracion del colegio · actualiza el historial academico · notifica al coordinador · registra en log |

## Eventos de convivencia

| Evento | Respuesta del Sistema |
|---|---|
| El coordinador registra una anotacion en el observador | Acumula la anotacion en el observador del ano · aplica el nivel de visibilidad elegido (RN-OB-081) · si requiere confirmacion, la solicita al estudiante/acudiente · registra en log |
| El coordinador anula una anotacion | Marca la anotacion como anulada conservando el historial y la justificacion (RN-OE-003) · registra en log |
| El coordinador clasifica un caso de convivencia | Instancia el protocolo de la Ruta de Atencion Integral del tipo asignado con plazos, responsables y actuaciones · abre el caso con consecutivo · registra la clasificacion auditada (RN-CVE-002) |
| El coordinador clasifica un caso como tipo III | Escala automaticamente al Rector · restringe la visibilidad del caso · marca el cierre como bloqueado hasta registrar el reporte a la autoridad (RN-CVE-004) |
| El caso involucra dano al cuerpo | Marca la remision a salud/EPS como actuacion obligatoria · bloquea el cierre del caso hasta registrarla (RN-CVE-005) |
| El coordinador cita formalmente a un acudiente | Genera la citacion con fecha/hora/lugar · notifica por el canal habilitado sin exponer el motivo sensible · registra en log |
| El coordinador registra un acuerdo / compromiso del caso | Asocia el acuerdo al caso · genera la anotacion correspondiente en el observador (RN-CVE-007) · pasa el caso a seguimiento · registra en log |
| El coordinador origina una remision a orientacion | Crea la remision interna al area de bienestar · no expone el contenido sensible al cuerpo docente · registra en log |
| El coordinador genera un reporte de convivencia | Agrega anotaciones y casos respetando la visibilidad por anotacion (RN-OE-005) · entrega PDF · registra la generacion |
| Un caso entra en seguimiento incumplido o reincide | Reabre el caso o escala su tipo · notifica al coordinador · registra el cambio en log |

## Eventos transversales

| Evento | Respuesta del Sistema |
|---|---|
| El coordinador intenta una accion fuera de su tenant | Rechaza en backend · no devuelve datos · registra el intento en log de seguridad (RR-01) |
| Login fallido del coordinador | Mensaje generico (no revela si el usuario existe) · incrementa contador de intentos · registra en log |
| El Rector intenta asignar ROL-03 / ROL-04 separados con ROL-05 activo | Advierte que el esquema combinado excluye los separados (RR-12) · bloquea o pide confirmacion segun politica |
| Se cierra el ano lectivo | Vuelve inmutables observadores, casos de convivencia y procesos de nivelacion/habilitacion del ano (RN-OE-004, RN-NH-005, RN-CVE-009) |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md` y `Logica del negocio/04-procesos-academicos/observador-del-estudiante.md`
