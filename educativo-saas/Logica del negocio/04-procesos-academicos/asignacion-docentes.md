---
titulo: Asignación de docentes
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [docentes, asignacion, materias, grupos]
---

# Asignación de docentes

Una asignación es la combinación **materia × grupo × año lectivo** asignada a un docente. Esa asignación es la que determina en qué grupos y materias el docente puede registrar notas y asistencia.

## Conceptos

- Un docente puede tener **múltiples asignaciones simultáneas** en el mismo año lectivo.
- Una misma combinación materia × grupo solo puede tener **un docente titular** asignado.
- Si el [[roles/07-director-de-grupo|Director de Grupo]] también dicta una materia en su propio grupo, esa asignación se marca explícitamente para que el sistema lo trate correctamente en los permisos.

## Atributos de una asignación

| Atributo | Descripción |
| --- | --- |
| Docente | Usuario con rol [[roles/06-docente|Docente]]. |
| Materia | Una materia del [[plan-de-estudios|plan de estudios]] del año lectivo. |
| Grupo | Un grupo concreto del año lectivo. |
| Año lectivo | Año lectivo activo. |
| Es director de grupo de este grupo | Booleano para casos en que el docente sí es director del grupo donde dicta. |
| Estado | Activa / inactiva. |

## Quién gestiona

- **Crear / editar:** [[roles/02-coordinador-academico|Coordinador Académico]].
- **Consultar:** [[roles/01-rector-administrador-colegio|Administrador del Colegio]], [[roles/02-coordinador-academico|Coordinador Académico]], el propio [[roles/06-docente|Docente]] (sus asignaciones) y la secretaría académica.

## Implicaciones operativas

Al crear una asignación, el docente automáticamente:

- Aparece como responsable de la materia en el grupo.
- Puede registrar notas y asistencia en esa combinación.
- Puede registrar logros e indicadores en esa materia para ese grupo.
- Puede publicar en agenda con alcance a ese grupo y materia (si tiene permiso de publicación habilitado).

Al inactivar una asignación:

- El docente deja de ver el grupo y la materia en su lista operativa.
- Las notas y asistencia ya registradas se conservan asociadas a la asignación histórica.
- El sistema permite reasignar la materia × grupo a otro docente.

## Reasignación durante el año lectivo

- El coordinador académico puede reasignar una materia × grupo a otro docente durante el año.
- La asignación anterior se marca como inactiva con fecha de cierre.
- La nueva asignación toma efecto desde su fecha de inicio.
- Las notas y asistencia ya registradas por el docente anterior se mantienen y siguen asociadas a su asignación histórica.

## Reglas de negocio

- **RN-AD-001 — Una sola titularidad activa:** una combinación materia × grupo no puede tener dos docentes titulares activos al mismo tiempo en el mismo año lectivo.
- **RN-AD-002 — Asignación obligatoria para registro:** un docente solo puede registrar notas y asistencia en combinaciones donde tenga asignación activa.
- **RN-AD-003 — Reasignación preserva historial:** al reasignar una materia × grupo, las notas previas no se transfieren al nuevo docente; quedan asociadas a la asignación original (auditable).
- **RN-AD-004 — Director de grupo no implica asignación de materia:** ser director de grupo no otorga automáticamente la asignación de ninguna materia en ese grupo; son conceptos independientes.
- **RN-AD-005 — Asignación dentro del año lectivo activo:** no se pueden crear asignaciones para años lectivos cerrados.
- **RN-AD-006 — Validación contra plan de estudios:** la materia de la asignación debe existir en el plan de estudios del año lectivo activo y aplicar al grado del grupo.

## Notas y pendientes

- Definir si un docente puede tener una "co-titularidad" (dos docentes compartiendo una materia × grupo) o si siempre es uno solo.
- Definir el comportamiento si un docente es eliminado mientras tiene asignaciones activas (recomendado: bloquear eliminación hasta reasignar).
