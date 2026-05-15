---
titulo: Horarios
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [horarios, clases, bloques]
---

# Horarios

El horario define con exactitud **qué docente dicta qué materia, a qué grupo, en qué aula, en qué día de la semana y en qué bloque horario**.

## Estructura del horario

Cada entrada del horario es una tupla:

```
(día de la semana, bloque horario, jornada, grupo, materia, docente, espacio físico)
```

Con esta información el sistema puede responder en cualquier momento:

- Dónde está cada grupo en este momento.
- Qué docente está en cada aula.
- Qué grupos tiene asignados cada docente y en qué horario.
- Qué aulas están ocupadas y cuáles libres en cada bloque.

## Requisitos previos

Antes de poder construir un horario:

1. Configuración de jornadas y bloques horarios completa (ver [[../03-multi-tenancy/configuracion-por-colegio|Configuración por colegio]]).
2. [[plan-de-estudios|Plan de estudios]] del año lectivo definido.
3. Grados, grupos y [[espacios-fisicos|espacios físicos]] registrados.
4. [[asignacion-docentes|Asignaciones de docentes]] creadas.

## Detección de conflictos

El sistema valida y alerta automáticamente sobre los siguientes conflictos al crear o modificar una entrada de horario:

| Conflicto | Descripción |
| --- | --- |
| Docente en dos lugares | Un mismo docente asignado a dos clases simultáneas en el mismo bloque horario. |
| Aula doble-ocupada | Una misma aula asignada a dos grupos distintos en el mismo bloque horario. |
| Grupo con dos clases | Un mismo grupo con dos materias programadas en el mismo bloque horario. |
| Excede intensidad horaria | El total de horas semanales programadas para una materia × grupo no coincide con la intensidad horaria definida en el plan de estudios. |
| Fuera de jornada | Un bloque programado fuera del rango horario de la jornada del grupo. |

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
- **RN-HO-002 — Validación contra asignaciones:** una entrada de horario solo puede crearse para combinaciones materia × grupo × docente que tengan una [[asignacion-docentes|asignación]] activa.
- **RN-HO-003 — Aula opcional:** si un grupo no tiene salón fijo, el aula se asigna por bloque. Si tiene salón fijo, el aula se prellena pero puede sobreescribirse para clases especializadas.
- **RN-HO-004 — Cambios auditados:** las modificaciones al horario quedan registradas con usuario, fecha, hora, valor anterior y nuevo.
- **RN-HO-005 — Horario inmutable en años cerrados:** no se puede modificar el horario de un año lectivo cerrado.
- **RN-HO-006 — Reasignación afecta horario:** al inactivar una asignación de docente, las entradas de horario dependientes quedan marcadas como pendientes de reasignación y el sistema notifica al coordinador.

## Notas y pendientes

- **[Decisión tomada]** El sistema **soporta excepciones puntuales** (ej. una clase movida a otro aula solo un día específico) sobre el horario recurrente. Regla: **RN-HR-040 — Excepciones puntuales sobre horario recurrente con auditoría y notificación al docente y al grupo**.
- **[Decisión tomada]** El sistema **soporta rotación quincenal "semanas A / semanas B"**. Regla: **RN-HR-041 — Rotación quincenal A/B opcional por colegio**.
