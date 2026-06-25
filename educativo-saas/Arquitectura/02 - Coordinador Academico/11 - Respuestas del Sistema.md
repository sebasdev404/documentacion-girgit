---
tags:
  - arquitectura
  - rol/coord-academico
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-03
---

# Respuestas del Sistema — Coordinador Academico

Que responde el sistema ante cada evento.

| Evento | Respuesta del Sistema |
|---|---|
| Coordinador crea una materia del plan | Agrega la materia al plan del grado · la deja disponible para grupos y horarios · registra en log |
| Coordinador archiva una materia en uso | Conserva el historico de notas asociado · la retira del plan activo · advierte el impacto en grupos · registra en log |
| Coordinador crea un grupo | Crea el grupo en el grado/ano · lo habilita para asignacion y matricula · registra en log |
| Coordinador asigna un docente a una materia/grupo | Habilita la visibilidad del docente sobre ese grupo y materia (RR-10) · notifica al docente · registra en log |
| Coordinador designa un director de grupo | Activa el complemento Director de Grupo sobre ese docente para ese grupo (RR-09) · notifica al docente · registra en log |
| Coordinador publica un horario | Hace visible el horario a docentes y estudiantes del grupo · notifica a los afectados · registra en log |
| Sistema detecta cruce al armar horario | Resalta el bloque en conflicto · no permite guardar/publicar hasta resolver · no registra cambio |
| Coordinador consulta el consolidado del tenant | Devuelve el estado academico de todos los grupos · marca grupos incompletos y estudiantes en riesgo |
| Coordinador edita una nota (permiso activado, periodo abierto) | Aplica el cambio · guarda valor anterior y nuevo · registra en log (RR-07) |
| Coordinador edita una nota tras el cierre (permiso activado) | Exige justificacion · aplica el cambio · registra evento sensible con justificacion en log (RR-07) |
| Coordinador activa el cierre de periodo | Congela las notas del periodo · bloquea la edicion a los docentes · habilita la generacion de boletines · notifica a docentes · registra en log |
| Coordinador reabre un periodo | Reabre la edicion de notas · si la config. lo exige, valida autorizacion del Rector · registra evento sensible con motivo en log |
| Coordinador abre un proceso de nivelacion | Crea el proceso para el estudiante y la materia · notifica al docente responsable · registra en log |
| Coordinador registra resultado de nivelacion | Actualiza el estado del estudiante en la materia · refleja el resultado en el consolidado · registra en log |
| Coordinador genera boletines de un grupo | Arma los boletines desde el consolidado cerrado · los deja en estado "generado" |
| Coordinador aprueba/firma boletines (permiso activado) | Marca los boletines como aprobados · los publica a los acudientes via portal · registra en log |
| Docente carga notas en un grupo del coordinador | Refleja la carga en el consolidado del coordinador · actualiza el semaforo de cierre del grupo |
| Periodo llega a su fecha limite con grupos incompletos | Genera alerta en el dashboard del coordinador · notifica por correo · no cierra automaticamente |
| Login fallido del coordinador | Mensaje generico (no revela si el usuario existe) · incrementa contador de intentos · registra en log de seguridad |
| Intento de acceso a modulo no permitido (observador, config., documentos) | Rechaza en backend (RR-02) · registra el intento en log |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/02-usuarios-roles-y-permisos/roles/02-coordinador-academico.md`
