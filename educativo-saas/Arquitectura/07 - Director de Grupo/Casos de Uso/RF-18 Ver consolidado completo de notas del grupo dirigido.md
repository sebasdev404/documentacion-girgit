---
tags:
  - arquitectura
  - rol/director-de-grupo
  - caso-de-uso
aliases:
  - CU RF-18
---

# ID: RF-18
**Nombre:** Ver consolidado completo de notas del grupo dirigido

**Historia:**
Como Director de Grupo necesito ver el consolidado completo de notas de mi grupo, con todas las materias y no solo las que dicto, para acompanar el desempeno academico integral de cada estudiante. Esta vista es exclusiva del grupo que dirijo (RR-09) y va mas alla del acceso que tengo como Docente, que solo me muestra lo asignado (RR-10). Con ella detecto a tiempo a los estudiantes en riesgo antes del cierre de periodo.

**Criterios de aceptacion:**
El sistema muestra al Director de Grupo el consolidado de su grupo dirigido con todas las materias, sus notas por periodo y el promedio por estudiante y por materia, sin permitir editar las notas de materias que no dicta cuando ese permiso esta desactivado por defecto; el acceso queda restringido unicamente al grupo dirigido (RR-09) y cualquier intento sobre otro grupo solo expone las materias que el usuario dicta como Docente (RR-10); la consulta es de solo lectura, queda registrada en el log de auditoria del tenant (RR-03) y el cruce con asistencia y observador alimenta las alertas tempranas del grupo (RN-VA-101).

**Documentacion:**
- PRD: PRD-09 Director de Grupo
- Flow: Consolidado del grupo dirigido
- Prototipo: (link de Figma)

**Flujo:**
`Grupo dirigido con notas cargadas` -> MANUAL -> `Director abre el consolidado de su grupo` -> AUTOMATICO -> `El sistema valida que el grupo es el dirigido (RR-09), arma la matriz de todas las materias x estudiantes, calcula promedios, marca alertas (RN-VA-101) y registra la consulta en el log (RR-03)`
