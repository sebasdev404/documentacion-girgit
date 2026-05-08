---
titulo: Disciplina y observaciones
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [disciplina, observaciones, proceso]
---

# Disciplina y observaciones

## Descripción

Módulo encargado del registro y seguimiento del comportamiento de los estudiantes a lo largo del año lectivo. El concepto central es el [[observador-del-estudiante|observador del estudiante]], documento acumulativo anual donde se concentran todas las anotaciones disciplinarias y de convivencia.

## Responsable principal

El [[roles/03-coordinador-convivencia|Coordinador de Convivencia]] es el actor principal de este módulo. Sin embargo:

- El [[roles/07-director-de-grupo|Director de Grupo]] también puede registrar anotaciones sobre los estudiantes de su grupo.
- El [[roles/01-rector-administrador-colegio|Administrador del Colegio]] tiene acceso completo.
- Los docentes pueden registrar observaciones académicas/disciplinarias sobre estudiantes en sus materias asignadas (con alcance limitado).

## Tipos de observación / anotación

| Tipo | Descripción |
| --- | --- |
| Llamado de atención | Anotación por incumplimiento de norma o conducta inapropiada. |
| Compromiso firmado | Acuerdo entre el estudiante (y/o acudiente) y la institución para corregir comportamientos. |
| Felicitación / reconocimiento | Anotación positiva por logro académico, deportivo o de convivencia. |
| Remisión a orientación escolar | Derivación al área de psicología u orientación. |
| Suspensión | Sanción disciplinaria con duración definida. |
| Observación académica del docente | Comentario sobre desempeño o actitud en una materia. |
| Observación general del director de grupo | Comentario consolidado sobre el estudiante en el periodo (aparece en boletín). |

## Datos de cada anotación

Cada anotación registra:

- Tipo.
- Descripción detallada del hecho.
- Fecha y hora.
- Usuario que la registró (con rol).
- Estudiante afectado.
- Si requiere confirmación por parte del estudiante / acudiente.
- Adjuntos opcionales (foto, escaneo de un acta, etc., sujetos a cuota de almacenamiento).
- Acciones derivadas (compromiso, sanción, remisión).

## Flujo de registro

1. El usuario autorizado registra la anotación.
2. El sistema notifica automáticamente al estudiante y al acudiente según la configuración del colegio.
3. Si la anotación requiere confirmación, queda en estado **pendiente de confirmación**.
4. El estudiante o el acudiente confirma desde el portal (registrando fecha, hora, IP).
5. La anotación queda en estado **confirmada**.

## Notificación a acudientes

- Por defecto, las anotaciones disciplinarias generan notificación automática al acudiente por correo y portal.
- El colegio puede configurar qué tipos de anotación notifican y cuáles no (ej. felicitaciones siempre, llamados de atención sí, observaciones académicas opcional).
- Las anotaciones marcadas como urgentes notifican inmediatamente.

## Apelaciones

- El estudiante o el acudiente puede solicitar revisión de una anotación.
- La solicitud queda registrada y la coordinación decide si la mantiene, modifica o retira.
- La modificación o retiro queda en el log de auditoría con motivo.
- La anotación original no se elimina físicamente: se marca como **anulada** con la justificación.

## Estados y transiciones

```
Registrada → Pendiente de confirmación → Confirmada
                                       → En apelación → Anulada
                                                       → Mantenida
```

## Reglas de negocio

- **RN-DI-001 — Acceso por rol:** un docente solo registra observaciones sobre estudiantes en sus grupos asignados. El director de grupo sobre los estudiantes de su grupo. La coordinación de convivencia sobre cualquier estudiante del colegio.
- **RN-DI-002 — Estudiante solo lectura:** el estudiante consulta su observador en modo de solo lectura.
- **RN-DI-003 — Confirmación auditada:** las confirmaciones de anotaciones se registran con fecha, hora e IP, asociadas al usuario que confirmó.
- **RN-DI-004 — Anulación no elimina:** las anotaciones anuladas se preservan en el observador como anuladas; no se eliminan físicamente.
- **RN-DI-005 — Inmutabilidad post año cerrado:** las anotaciones de años lectivos cerrados son inmutables.
- **RN-DI-006 — Auditoría obligatoria:** toda creación, edición y anulación de anotaciones queda en el log.

## Notas y pendientes

- **[Configurable por colegio]** Comportamiento del portal del estudiante durante una sanción de suspensión: bloqueo total, lectura limitada o sin restricción. Por defecto: lectura limitada (consulta de notas y comunicados, sin participación en agenda ni mensajería).
- **[Configurable por colegio]** Si las anotaciones positivas (felicitaciones) requieren confirmación del acudiente o estudiante. Por defecto: solo notificación, sin confirmación requerida.
