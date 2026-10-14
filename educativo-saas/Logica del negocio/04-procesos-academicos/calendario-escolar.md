---
titulo: Calendario escolar
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [calendario, eventos]
---

# Calendario escolar

## Corte implementado — 14 de octubre de 2026

El calendario actual unifica eventos manuales (actividad, reunión, celebración y aviso) y tareas publicadas del Aula mediante lectura, sin copiar tareas a eventos. Una tarea con plazo aparece el día de entrega; sin plazo, el día de publicación efectiva. Borradores/ocultos/programaciones futuras no aparecen. Cada entrada conserva sus permisos y origen. El alcance actual es por grupos o institucional; otros alcances, recurrencias, festivos automáticos y hitos descritos abajo son objetivos futuros, no capacidades verificadas.

Los eventos pueden guardarse como borrador o publicarse. Solo el autor ve sus borradores; los gestores pueden consultar los eventos publicados. El docente requiere asignación vigente a sus grupos; no existe una excepción configurable de cualquier grupo. Toda publicación institucional exige el permiso específico. No se crean cuentas ni se notifican acudientes en este corte.

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
- **Acudiente:** portal no implementado en el corte actual.
- **Docente:** ve los eventos que le aplican según sus asignaciones, más eventos institucionales generales.
- **Coordinación y administración:** vista completa de publicados; los borradores ajenos permanecen privados.

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

- El creador elige «Enviar evento por correo al publicar», apagado inicialmente. Guardar un borrador no envía nada; publicar sin activarlo tampoco.
- Solo estudiantes activos con matrícula dentro del alcance. No docentes ni representantes. Se procesa por cola en lotes y con reintentos; no hay urgencia que evada estos controles.
- La edición no reenvía automáticamente. Avisos explícitos de cambios/cancelaciones y recordatorios son futuros.
- Aceptación SMTP no acredita bandeja de entrada. El detalle autorizado muestra pendientes, aceptados y fallidos, sin revelar destinatarios a estudiantes.

Ver [[../05-comunicacion/notificaciones|Notificaciones]].

## Reglas de negocio

- **RN-CE-001 — Festivos cancelan clases:** un día marcado como festivo cancela automáticamente las sesiones del horario regular y no genera registro de asistencia.
- **RN-CE-002 — Alcance del evento:** un evento puede dirigirse a toda la institución, a un nivel, grado, grupo, materia o jornada. Solo los destinatarios del alcance ven el evento en su calendario.
- **RN-CE-003 — Eventos no se solapan con cierres:** no se permite programar exámenes ni salidas pedagógicas en días marcados como festivos o cierre de periodo.
- **RN-CE-004 — Eliminación auditada:** la eliminación de un evento queda registrada en el log de auditoría.

## Notas y pendientes

- **[Pendiente — producto]** Preprovisión automática de festivos nacionales por país (Colombia + segundo país piloto) con actualización anual mantenida por la plataforma. El colegio puede añadir o desactivar festivos.
- **[Funcionalidad futura]** Sincronización iCal/Google Calendar (suscripción de solo lectura). Fuera de MVP.
