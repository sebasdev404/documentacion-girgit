---
tags:
  - arquitectura
  - rol/coordinador-academico
  - caso-de-uso
aliases:
  - CU RF-15
---

# ID: RF-15
**Nombre:** Construir horarios de clase

**Historia:**
Como Coordinador Academico, al inicio del ano lectivo necesito armar el horario de cada grupo distribuyendo las materias y los docentes ya asignados a lo largo de la jornada definida por el Rector. El horario es la columna vertebral de la operacion diaria, asi que debe respetar la carga horaria del plan de estudios y no generar cruces de docentes ni de aulas antes de publicarse a docentes y estudiantes.

**Criterios de aceptacion:**
El sistema permite construir el horario solo sobre las jornadas y bloques definidos en la configuracion base del tenant (no editables por el Coordinador). Al ubicar una materia en un bloque, el sistema valida en tiempo real que el docente asignado no este ya ocupado en otro grupo en ese mismo bloque y que el aula no este duplicada; si detecta un cruce, bloquea la accion y muestra el conflicto especifico. El horario no puede publicarse mientras existan cruces sin resolver o si la suma de horas por materia no coincide con la intensidad del plan de estudios (RF-11). Al publicar, el horario queda visible para docentes y estudiantes del grupo y la accion queda registrada en auditoria (RR-03).

**Documentacion:**
- PRD: PRD-04 Coordinador Academico
- Flow: Construccion y publicacion de horarios
- Prototipo: (link de Figma)

**Flujo:**
`Plan de estudios definido + docentes asignados (RF-13) + jornadas de config base` -> MANUAL -> `Coordinador arrastra materias/docentes a los bloques de la jornada del grupo` -> AUTOMATICO -> `Sistema valida cruces de docente y aula y carga horaria vs plan; bloquea si hay conflicto` -> MANUAL -> `Coordinador resuelve conflictos y pulsa Publicar` -> AUTOMATICO -> `Horario publicado y visible para docentes y estudiantes del grupo; accion registrada en auditoria`
