---
titulo: Espacios físicos
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [aulas, espacios, salones]
---

# Espacios físicos

El colegio registra todas sus aulas y espacios disponibles para usarlos en la construcción de horarios.

## Atributos de un espacio físico

| Atributo | Descripción |
| --- | --- |
| Nombre | Identificador visible (ej. "Aula 201", "Laboratorio de Química"). |
| Capacidad máxima | Número máximo de estudiantes que el espacio admite. |
| Tipo | Aula general / Laboratorio / Sala especializada / Sala de sistemas / Biblioteca / Otro. |
| Sede | A qué sede del colegio pertenece (si aplica). |
| Estado | Activo / inactivo (un aula en mantenimiento se marca inactiva). |

## Uso de los espacios

Un aula puede funcionar como:

- **Salón fijo de un grupo:** el grupo tiene asignado este aula como su lugar habitual; los docentes son quienes se desplazan.
- **Espacio especializado:** distintos grupos se desplazan a este aula según el horario (laboratorios, sala de sistemas, etc.).

Un mismo aula puede combinar ambos roles (sirve como salón fijo de un grupo, pero también es usada por otros grupos para clases especializadas).

## Reglas de negocio

- **RN-EF-001 — Capacidad mayor que cero:** la capacidad máxima debe ser un entero positivo.
- **RN-EF-002 — Detección de doble ocupación:** ver [[horarios|Horarios]] — el sistema bloquea entradas de horario que generen doble ocupación.
- **RN-EF-003 — Aulas inactivas no asignables:** un aula en estado inactivo no puede ser asignada a nuevas entradas de horario.
- **RN-EF-004 — Eliminación condicionada:** un aula con asignaciones activas en el horario no puede eliminarse hasta liberarla.

## Quién gestiona

- **Crear / editar:** [[roles/01-rector-administrador-colegio|Administrador del Colegio]] o [[roles/02-coordinador-academico|Coordinador Académico]].
- **Consultar:** todos los roles del tenant.

## Notas y pendientes

- **[Decisión tomada — MVP]** El sistema **solo soporta horarios recurrentes** sobre los espacios físicos. Las reservas puntuales (ej. auditorio para reunión de padres en una fecha específica) **no entran en MVP** y se evalúan como funcionalidad futura.
