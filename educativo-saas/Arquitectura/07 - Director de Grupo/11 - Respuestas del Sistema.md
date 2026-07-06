---
tags:
  - arquitectura
  - rol/director-de-grupo
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-08
---

# Respuestas del Sistema — Director de Grupo

Que responde el sistema ante cada evento del complemento sobre el grupo dirigido.

> Las respuestas a eventos de Docente (guardar nota, registrar asistencia de sus clases) viven en [[../06 - Docente/11 - Respuestas del Sistema|Respuestas del Docente]]. Aqui solo lo adicional.

| Evento | Respuesta del Sistema |
|---|---|
| El Coord. Academico designa al docente como Director de Grupo | Activa el complemento ROL-08 sobre ese grupo · habilita los modulos adicionales en el sidebar · notifica al docente · registra en log |
| Se retira el complemento de un docente | Oculta los modulos adicionales · conserva las anotaciones y observaciones ya registradas · registra el cambio en log |
| Director abre el consolidado del grupo | Devuelve todas las materias del grupo con sus notas (solo lectura) · resalta materias en rojo y sin nota |
| Director genera los boletines del grupo (RF-38) | Si las notas estan cerradas, genera los boletines · si faltan notas, advierte y exige confirmacion · deja los boletines disponibles segun la politica de firma · registra en log |
| Director agrega una observacion general (RF-40) | Asocia la observacion al estudiante y al periodo · la incluye en el boletin · registra en log |
| Director firma un boletin (RF-39, si esta activado) | Marca el boletin como firmado por el director · lo libera al acudiente via portal · registra en log |
| Director registra una anotacion en el observador (RF-25) | Guarda la anotacion sobre el estudiante del grupo · aplica la visibilidad configurada (RN-OB-081) · si requiere confirmacion, notifica al acudiente · registra en log |
| Acudiente confirma/lee una anotacion | Marca la anotacion como confirmada · notifica al director · registra en log |
| Director aplica una medida pedagogica tipo I | Registra la actuacion tipo I · genera la anotacion correspondiente en el observador (RN-CVE-007) · registra en log |
| Director marca un reporte como presunto delito | Escala el caso al Rector · restringe la visibilidad del caso a coordinacion y Rector · notifica al Rector (RN-CVE-004) |
| Director reporta una situacion de convivencia | Crea el reporte en estado "Reportado" · lo enruta al Coord. de Convivencia para clasificar · registra en log |
| Director registra el seguimiento de un acuerdo | Actualiza el estado del seguimiento · si el acuerdo se incumple, deja el caso disponible para reapertura (RN-CVE-003) · registra en log |
| Director edita una nota que no dicta / tras cierre (configurable) | Si el permiso esta activo, exige justificacion · aplica el cambio · registra en log con valor anterior y nuevo (RR-07, RR-09) · notifica al docente titular de la materia |
| Director cita formalmente a un acudiente (configurable) | Crea la citacion · notifica al acudiente por el canal habilitado · registra en log |
| Director solicita una citacion al Coordinador | Enruta la solicitud al Coord. de Convivencia · registra en log |
| Director envia un mensaje a un acudiente (configurable) | Entrega el mensaje por el portal/canal habilitado · lo registra · el acudiente lo recibe operando la cuenta del Estudiante (RR-11) |
| Intento de operar fuera del grupo dirigido | Rechaza la accion en backend · registra el intento en el log de seguridad (RR-09, RR-02) |
| Cierre del ano lectivo | Congela los boletines, observaciones y casos del grupo (inmutables) · deja todo consultable · registra el cierre |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../06 - Docente/11 - Respuestas del Sistema|Respuestas del Docente (rol base)]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`
