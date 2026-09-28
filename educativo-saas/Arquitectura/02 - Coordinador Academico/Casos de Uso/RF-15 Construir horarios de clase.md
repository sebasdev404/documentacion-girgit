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
Como Coordinador Academico, al inicio del ano lectivo necesito armar el horario de cada grupo distribuyendo las materias a lo largo de su jornada, aun cuando todavia no se hayan creado los docentes. Puedo elegir el docente de cada clase ahora o despues. El horario debe respetar la carga horaria del plan de estudios y no generar cruces de grupos, docentes asignados ni aulas.

**Criterios de aceptacion:**
El sistema permite construir el horario dentro de la jornada de cada grupo. Cada clase puede seleccionar un bloque de esa jornada o indicar directamente hora de inicio y fin, incluso si hay bloques configurados. Los bloques son franjas compartidas, no horarios obligatorios para todos los grupos. La sede y la jornada se obtienen del grupo. El docente es opcional y se edita en la clase sin exigir una asignacion academica previa. Al ubicar una materia, el sistema valida los intervalos reales para evitar cruces de grupo, docente asignado y aula, incluso entre clases con y sin bloque. Si detecta un cruce, bloquea la accion y muestra el conflicto especifico. La clase se registra con auditoria (RR-03).

**Documentacion:**
- PRD: PRD-04 Coordinador Academico
- Flow: Construccion y publicacion de horarios
- Prototipo: (link de Figma)

**Flujo:**
`Plan de estudios definido + jornada del grupo` -> MANUAL -> `Coordinador programa la clase con bloque o con horas propias; docente opcional` -> AUTOMATICO -> `Sistema valida cruces de grupo, aula y docente si existe, y carga horaria vs plan` -> MANUAL -> `Coordinador puede editar la clase y asignarle docente despues` -> AUTOMATICO -> `Clase visible en el horario del grupo y para su docente cuando se le asigne; cambios auditados`
