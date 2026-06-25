---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-15
---

# ID: RF-15
**Nombre:** Construir horarios de clase

**Historia:**
Como Coordinador Academico y de Convivencia necesito construir los horarios de clase de cada grupo a partir del plan de estudios y de los docentes ya asignados, para que cada grupo tenga su distribucion semanal de materias por bloque. El horario es la base operativa del periodo: ordena el dia a dia del colegio y debe evitar choques de docente, de grupo y de aula antes de publicarse.

**Criterios de aceptacion:**
El coordinador solo puede armar horarios sobre grupos que ya tienen docentes asignados a sus materias (RF-13) y dentro de las jornadas y bloques definidos en la configuracion base del tenant, sin poder modificar esa configuracion. El sistema valida en tiempo real que un mismo docente no quede en dos grupos en el mismo bloque, que un grupo no tenga dos materias en el mismo bloque y que el aula no quede duplicada; si detecta un choque bloquea la publicacion y senala el conflicto. Cada horario respeta la intensidad horaria semanal del plan de estudios (RF-11): si una materia queda por debajo o por encima de su intensidad, el sistema advierte. Al publicar, el horario queda visible para los docentes y directores de grupo afectados, y la accion queda registrada en el log de auditoria del tenant (RR-03). Todo el flujo opera dentro del aislamiento del propio colegio (RR-01).

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Construccion y publicacion de horarios
- Prototipo: (link de Figma)

**Flujo:**
`Grupo con docentes asignados (RF-13)` -> MANUAL -> `Coordinador ubica cada materia en su bloque dentro de la jornada del tenant` -> AUTOMATICO -> `Sistema valida choques de docente / grupo / aula e intensidad horaria contra el plan de estudios` -> MANUAL -> `Coordinador resuelve conflictos y publica el horario` -> AUTOMATICO -> `Horario publicado, visible para docentes y director de grupo, registrado en el log de auditoria`
