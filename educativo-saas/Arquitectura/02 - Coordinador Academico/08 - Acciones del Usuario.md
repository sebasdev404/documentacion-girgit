---
tags:
  - arquitectura
  - rol/coord-academico
  - acciones
aliases:
  - Acciones ROL-03
---

# Acciones del Usuario — Coordinador Academico

Tabla accion -> resultado. Cada accion sensible (cierre, edicion de notas, asignacion) genera entrada en el log de auditoria del tenant (RR-03).

| Accion | Resultado |
|---|---|
| Click en "Crear materia" y completa el formulario | Sistema valida datos · crea la materia con su area e intensidad horaria · la deja disponible para grupos del grado · registra en log |
| Edita / archiva una materia | Sistema actualiza el plan de estudios · si la materia esta en uso en grupos activos, advierte el impacto · registra en log |
| Click en "Crear grupo" y completa el formulario | Sistema valida grado/jornada/ano · crea el grupo · lo deja disponible para asignacion y matricula · registra en log |
| Asigna un docente a una materia de un grupo | Sistema valida que no exista doble titular · habilita la visibilidad del docente sobre ese grupo/materia (RR-10) · registra en log |
| Designa un director de grupo | Sistema activa el complemento Director de Grupo sobre ese docente para ese grupo (RR-09) · notifica al docente · registra en log |
| Crea / edita un bloque de horario | Sistema valida cruces de docente/aula/grupo en el mismo bloque · si hay cruce, lo resalta y bloquea · registra en log |
| Click en "Publicar horario" | Sistema publica el horario · cada docente y estudiante ve su horario propio · notifica a los afectados · registra en log |
| Consulta el consolidado de un grupo | Sistema muestra notas, promedios y materias perdidas del grupo · marca estudiantes en riesgo |
| Consulta el consolidado de todos los grupos | Sistema agrega el estado academico del tenant · resalta grupos con consolidado incompleto |
| Edita una nota (si el colegio habilita el permiso) | Sistema valida periodo abierto (RR-07) · aplica el cambio · registra quien, que valor anterior y nuevo en log |
| Edita una nota tras el cierre (si el colegio habilita el permiso) | Sistema exige justificacion · aplica el cambio · registra evento sensible en log (RR-07) |
| Click en "Validar consolidados" en el panel de cierre | Sistema verifica que todos los grupos tengan consolidado completo · lista grupos/docentes pendientes |
| Click en "Activar cierre de periodo" | Sistema exige consolidados completos · congela las notas · bloquea edicion a los docentes · habilita boletines · notifica a docentes · registra en log |
| Click en "Reabrir periodo" | Sistema valida permiso (puede requerir Rector) · exige motivo · reabre edicion de notas · registra evento sensible en log |
| Abre un proceso de nivelacion / habilitacion | Sistema crea el proceso para el estudiante y materia perdida · notifica al docente · registra en log |
| Registra el resultado de una nivelacion | Sistema actualiza el estado del estudiante en esa materia · refleja el resultado en el consolidado · registra en log |
| Genera el boletin de un grupo | Sistema arma los boletines a partir del consolidado cerrado · los deja en estado "generado" |
| Aprueba / firma boletines (si el colegio habilita el permiso) | Sistema marca los boletines como aprobados · los publica a los acudientes · registra en log |
| Envia un comunicado academico (si habilitado) | Sistema entrega el comunicado a los destinatarios · registra el envio |
| Cierra sesion | Sistema invalida el token · registra logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
