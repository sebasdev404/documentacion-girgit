---
tags:
  - arquitectura
  - rol/docente
  - caso-de-uso
aliases:
  - CU RF-24
---

# ID: RF-24
**Nombre:** Registrar observacion academica en su materia

**Historia:**
Como docente quiero dejar una anotacion academica sobre un estudiante en la materia que dicto (un avance, una dificultad o un compromiso pedagogico), para que quede constancia del desempeno mas alla de la nota y el acudiente y el Director de Grupo tengan contexto del proceso. Solo puedo observar a estudiantes de los grupos y materias que el Coordinador me asigno (RR-10); escribo en el observador ACADEMICO, no en el disciplinario, y la anotacion queda asociada al estudiante con la visibilidad que el colegio configuro.

**Criterios de aceptacion:**
El docente solo puede registrar observaciones sobre estudiantes de los grupos y materias que tiene asignados (RR-10); cualquier intento fuera de su asignacion se rechaza en frontend y backend (RR-02). La observacion es de caracter academico (avance, dificultad, compromiso, felicitacion), nunca disciplinaria ni clasificatoria de convivencia: el docente no abre casos ni define sanciones (RN-CVE-002). Cada observacion queda asociada al estudiante, a la materia y al docente autor, con fecha y registro de auditoria de quien la creo o edito y cuando (RR-03). El docente puede editar unicamente las observaciones que el mismo registro mientras la observacion siga abierta; no ve ni modifica observaciones de otros docentes ni el observador disciplinario.

**Documentacion:**
- PRD: PRD-08 Docente
- Flow: Registro de observacion academica por estudiante
- Prototipo: (link de Figma)

**Flujo:**
`Estudiante de grupo y materia asignados / Docente en su materia` -> MANUAL -> `Selecciona al estudiante, escribe la observacion academica (tipo y detalle) y confirma` -> AUTOMATICO -> `Valida asignacion (RR-10), persiste la observacion asociada al estudiante y la materia, registra auditoria (RR-03) y la publica con la visibilidad configurada por el colegio`
