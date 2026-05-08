---
titulo: Observador del estudiante
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [observador, disciplina, convivencia]
---

# Observador del estudiante

El observador es el **documento acumulativo anual de cada estudiante**. Concentra todas las anotaciones disciplinarias, de convivencia y de seguimiento realizadas durante el año lectivo.

## Estructura

Cada observador está asociado a:

- Un estudiante.
- Un año lectivo.

Y contiene una lista cronológica de **anotaciones** (ver [[disciplina-y-observaciones|Disciplina y observaciones]] para los tipos de anotación).

## Quién registra

| Rol | Alcance |
| --- | --- |
| [[roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Cualquier estudiante del colegio. |
| [[roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Acceso completo. |
| [[roles/07-director-de-grupo\|Director de Grupo]] | Estudiantes de su grupo. |
| [[roles/06-docente\|Docente]] | Estudiantes en sus materias asignadas (alcance limitado a observaciones académicas/disciplinarias asociadas a su clase). |

## Acceso del estudiante

- El estudiante puede consultar **su propio observador** desde el portal en modo de **solo lectura**.
- No puede modificar ninguna anotación.
- Puede confirmar (cuando se le solicite) las anotaciones que requieren confirmación.

## Acceso del acudiente

- El acudiente puede consultar el observador del estudiante a su cargo en modo de solo lectura.
- Si una anotación requiere confirmación del acudiente, esta se solicita explícitamente y el sistema registra la confirmación.

## Visualización

El observador se muestra como una vista cronológica con filtros:

| Filtro | Opciones |
| --- | --- |
| Tipo de anotación | Llamado de atención, compromiso, felicitación, remisión, suspensión, observación académica, observación general. |
| Estado | Pendiente de confirmación, Confirmada, En apelación, Anulada. |
| Rango de fechas | Periodo personalizado dentro del año lectivo. |
| Autor | Coordinador / director de grupo / docente. |

## Reportes

El sistema genera reportes de convivencia derivados del observador:

- Por estudiante (resumen anual).
- Por grupo (anotaciones agregadas).
- Por tipo de anotación (ej. "todas las suspensiones del año").
- Por rango de fechas.

Estos reportes son útiles para el seguimiento de casos recurrentes y para la preparación de informes de convivencia institucional. Ver [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]].

## Histórico

- El observador de un año cerrado es inmutable.
- Los observadores de años anteriores siguen siendo consultables por el estudiante, el acudiente y la coordinación.
- El informe disciplinario consolidado del estudiante puede generarse en PDF abarcando varios años.

## Reglas de negocio

- **RN-OE-001 — Un observador por estudiante por año lectivo:** cada estudiante tiene un único observador por año lectivo. Las anotaciones se acumulan ahí.
- **RN-OE-002 — Solo lectura para el estudiante y el acudiente:** ninguno puede modificar ni eliminar anotaciones.
- **RN-OE-003 — Anulación preserva historial:** las anotaciones anuladas se conservan en el observador como anuladas con la justificación correspondiente.
- **RN-OE-004 — Inmutabilidad post-cierre:** los observadores de años cerrados son inmutables.
- **RN-OE-005 — Reportes respetan visibilidad:** los reportes de convivencia respetan el alcance del rol que los solicita (un docente no ve el observador de estudiantes que no son suyos).

## Notas y pendientes

- Definir si el observador soporta etiquetas o categorías personalizadas por colegio (ej. "bullying", "rendimiento", "salud mental").
- Definir si las anotaciones tienen visibilidad selectiva (ej. una observación interna entre coordinadores que no aparece al estudiante).
