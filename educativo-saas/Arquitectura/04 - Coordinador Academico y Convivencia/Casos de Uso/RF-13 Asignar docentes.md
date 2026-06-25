---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-13
---

# ID: RF-13
**Nombre:** Asignar docentes a materias y grupos

**Historia:**
Como Coordinador Academico y de Convivencia necesito asignar el docente titular de cada materia en cada grupo, para que cada clase tenga responsable y para que el docente vea unicamente lo que le corresponde. Esta asignacion es la que conecta el plan de estudios con las personas: alimenta los horarios, la carga de notas, la asistencia y el observador de cada grupo.

**Criterios de aceptacion:**
El coordinador puede asignar un docente del propio colegio a una materia x grupo y quitar o cambiar esa asignacion dentro de su tenant (RR-01). El sistema solo permite asignar materias que existen en el plan de estudios del grado del grupo (RF-11) y docentes activos del tenant. Como consecuencia de la asignacion, el docente ve unicamente los grupos y materias que se le asignaron y nada mas (RR-10); el sistema no le expone otros grupos. Una materia x grupo no puede quedar con dos docentes titulares simultaneos; el sistema lo impide. Si se quita una asignacion con horario ya publicado o notas ya cargadas, el sistema advierte del impacto antes de confirmar. Toda asignacion, cambio o retiro queda registrado en el log de auditoria del tenant (RR-03).

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Asignacion de docentes a materias y grupos
- Prototipo: (link de Figma)

**Flujo:**
`Grupo creado y plan de estudios del grado definido (RF-11, RF-12)` -> MANUAL -> `Coordinador selecciona una materia del grupo y le asigna un docente titular activo` -> AUTOMATICO -> `Sistema valida que la materia pertenezca al plan del grado y que no exista otro titular para esa materia x grupo` -> MANUAL -> `Coordinador confirma la asignacion` -> AUTOMATICO -> `Docente habilitado para ver solo ese grupo y materia (RR-10); asignacion registrada en el log de auditoria (RR-03) y disponible para horarios, notas y asistencia`
