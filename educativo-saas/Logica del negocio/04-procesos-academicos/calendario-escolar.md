---
titulo: Calendario escolar
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [calendario, eventos]
---

# Calendario escolar

## Descripción

El calendario escolar agrupa todos los eventos relevantes del año lectivo: clases, exámenes, festivos, reuniones, salidas pedagógicas, fechas de cierre de periodos y eventos institucionales. Sirve de referencia visual para todos los actores del colegio.

No confundir con [[periodos-academicos|períodos académicos]]: los periodos definen la estructura del año lectivo (cuándo se registran notas), mientras que el calendario escolar es la agenda institucional con eventos puntuales.

## Tipos de evento

| Tipo | Descripción |
| --- | --- |
| Clase | Sesión regular del horario semanal. Se genera automáticamente desde el [[horarios|horario]] y no se edita evento por evento. |
| Examen | Evaluación parcial o final programada por un docente o por coordinación. |
| Festivo | Día no laborable. Suspende clases del horario regular. |
| Reunión | Reuniones de padres, consejos, jornadas pedagógicas. |
| Salida pedagógica | Actividad fuera del colegio (excursión, visita técnica, deporte). |
| Cierre de periodo | Hito automático generado por la configuración del año lectivo. |
| Inicio / fin de año lectivo | Hitos automáticos. |
| Evento institucional | Izadas de bandera, celebraciones, semanas culturales. |

## Visibilidad por rol

- **Estudiante:** ve los eventos que le aplican según su grado y grupo.
- **Acudiente:** mismo alcance que el estudiante a su cargo.
- **Docente:** ve los eventos que le aplican según sus asignaciones, más eventos institucionales generales.
- **Coordinación y administración:** vista completa.

## Creación y edición de eventos

- **Eventos institucionales:** los crea el [[roles/01-rector-administrador-colegio|Administrador]] o el [[roles/02-coordinador-academico|Coordinador Académico]].
- **Exámenes:** los crea el docente titular de la materia o la coordinación.
- **Salidas pedagógicas:** las crea el coordinador académico.
- **Festivos:** los crea la administración. El sistema puede preprovisionar los festivos nacionales del país.
- **Cierres de periodo y año lectivo:** se generan automáticamente desde la configuración.

## Recurrencia y excepciones

- Un evento puede ser puntual (un solo día) o recurrente (todos los lunes durante un mes).
- Los eventos recurrentes admiten excepciones (ej. "todos los lunes excepto el 15 de mayo").
- Los festivos cancelan automáticamente los eventos regulares de ese día.

## Integración con notificaciones

- Al crear un evento institucional, el sistema notifica automáticamente a los destinatarios según el alcance configurado.
- El autor del evento puede marcarlo como urgente para forzar la notificación inmediata.
- Los recordatorios automáticos previos al evento son configurables por el colegio (ej. recordatorio 24h antes y 1h antes).

Ver [[../05-comunicacion/notificaciones|Notificaciones]].

## Reglas de negocio

- **RN-CE-001 — Festivos cancelan clases:** un día marcado como festivo cancela automáticamente las sesiones del horario regular y no genera registro de asistencia.
- **RN-CE-002 — Alcance del evento:** un evento puede dirigirse a toda la institución, a un nivel, grado, grupo, materia o jornada. Solo los destinatarios del alcance ven el evento en su calendario.
- **RN-CE-003 — Eventos no se solapan con cierres:** no se permite programar exámenes ni salidas pedagógicas en días marcados como festivos o cierre de periodo.
- **RN-CE-004 — Eliminación auditada:** la eliminación de un evento queda registrada en el log de auditoría.

## Notas y pendientes

- **[Pendiente — producto]** Preprovisión automática de festivos nacionales por país (Colombia + segundo país piloto) con actualización anual mantenida por la plataforma. El colegio puede añadir o desactivar festivos.
- **[Funcionalidad futura]** Sincronización iCal/Google Calendar (suscripción de solo lectura). Fuera de MVP.
