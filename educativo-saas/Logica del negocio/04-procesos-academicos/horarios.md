---
titulo: Horarios
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [horarios, clases, bloques]
---

# Horarios

El horario define **qué materia recibe cada grupo, en qué espacio, en qué día de la semana y entre qué horas**. El docente puede asignarse después. Cada clase puede usar un bloque predefinido o sus propias horas.

## Estructura del horario

Cada entrada del horario es una tupla:

```
(día de la semana, bloque horario opcional o intervalo propio, jornada del grupo, grupo, materia, docente opcional, espacio físico opcional)
```

Con esta información el sistema puede responder en cualquier momento:

- Dónde está cada grupo en este momento.
- Qué docente está en cada aula.
- Qué grupos tiene asignados cada docente y en qué horario.
- Qué aulas están ocupadas y cuáles libres en cada intervalo.

La jornada y la sede se obtienen del grupo. Un bloque de la jornada representa una franja compartida que cualquier grupo compatible puede reutilizar; **no asigna por sí mismo una materia ni obliga a todos los grupos a utilizarla**. Aunque existan bloques, cada clase puede indicar horas propias. Ambas formas conviven en un colegio y cada clase usa exactamente una de ellas. Esto permite que dos grupos del mismo grado y jornada tengan horarios distintos.

## Requisitos previos

Antes de poder construir un horario:

1. Jornada del grupo configurada. Los bloques horarios son opcionales (ver [[../03-multi-tenancy/configuracion-por-colegio|Configuración por colegio]]).
2. [[plan-de-estudios|Plan de estudios]] del año lectivo definido.
3. Grados, grupos y [[espacios-fisicos|espacios físicos]] registrados.
4. La asignación de docente no es requisito para construir el horario. Se puede elegir el docente en la clase posteriormente; la pestaña [[asignacion-docentes|Asignaciones de docentes]] permanece para los procesos académicos que la necesitan.

## Detección de conflictos

El sistema valida y alerta automáticamente sobre los siguientes conflictos al crear o modificar una entrada de horario:

| Conflicto | Descripción |
| --- | --- |
| Docente en dos lugares | Un mismo docente asignado a dos clases cuyos intervalos se cruzan. |
| Aula doble-ocupada | Una misma aula asignada a dos grupos con intervalos cruzados. |
| Grupo con dos clases | Un mismo grupo con dos materias programadas en intervalos cruzados. |
| Excede intensidad horaria | El total de horas semanales programadas para una materia × grupo no coincide con la intensidad horaria definida en el plan de estudios. |
| Fuera de jornada | Una clase programada fuera del rango horario de la jornada del grupo. |

El sistema **bloquea** la creación de la entrada en conflicto e informa al usuario qué entrada existente choca.

## Vistas del horario

| Vista | Descripción |
| --- | --- |
| Por grupo | Horario semanal del grupo (la vista que ve el estudiante). |
| Por docente | Horario semanal del docente (la vista que ve el docente). |
| Por aula | Ocupación semanal del aula (útil para coordinación). |
| Por jornada | Mapa completo de una jornada en una vista de matriz. |

## Quién gestiona

- **Crear / editar:** [[roles/02-coordinador-academico|Coordinador Académico]].
- **Consultar:** todos los roles relevantes ven el horario en su contexto (estudiante el suyo, docente el suyo, etc.).

## Reglas de negocio

- **RN-HO-001 — Sin conflictos al guardar:** el sistema no permite guardar entradas de horario que generen conflictos de docente, aula o grupo.
- **RN-HO-002 — Clase independiente de asignaciones:** una entrada de horario se crea con grupo, materia, día y horas; el docente es opcional y puede agregarse al editar. Si se selecciona, debe ser docente activo. La asignación académica de la pestaña Asignaciones no es requisito del horario.
- **RN-HO-003 — Aula opcional:** si un grupo no tiene salón fijo, el aula se asigna por bloque. Si tiene salón fijo, el aula se prellena pero puede sobreescribirse para clases especializadas.
- **RN-HO-004 — Cambios auditados:** las modificaciones al horario quedan registradas con usuario, fecha, hora, valor anterior y nuevo.
- **RN-HO-005 — Horario inmutable en años cerrados:** no se puede modificar el horario de un año lectivo cerrado.
- **RN-HO-006 — Docente de la clase:** el docente del horario se gestiona directamente en cada clase. Cambiar una asignación académica independiente no modifica automáticamente clases ya programadas.
- **RN-HO-007 — Franjas flexibles:** cada clase usa un bloque de la jornada del grupo o un intervalo propio de inicio y fin. Los conflictos se calculan con las horas reales, incluso cuando una clase usa bloque y otra no.

## Notas y pendientes

- **[Decisión tomada]** El sistema **soporta excepciones puntuales** (ej. una clase movida a otro aula solo un día específico) sobre el horario recurrente. Regla: **RN-HR-040 — Excepciones puntuales sobre horario recurrente con auditoría y notificación al docente y al grupo**.
- **[Decisión tomada]** El sistema **soporta rotación quincenal "semanas A / semanas B"**. Regla: **RN-HR-041 — Rotación quincenal A/B opcional por colegio**.
