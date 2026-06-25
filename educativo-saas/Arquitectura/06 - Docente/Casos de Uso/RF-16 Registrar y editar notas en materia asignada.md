---
tags:
  - arquitectura
  - rol/docente
  - caso-de-uso
aliases:
  - CU RF-16
---

# ID: RF-16
**Nombre:** Registrar y editar notas en materia asignada

**Historia:**
Como docente quiero cargar y editar las notas de las evaluaciones de mi materia mientras el periodo este abierto, para que el acumulado de cada estudiante se calcule solo y yo no tenga que llevar cuentas en hojas sueltas. Solo opero sobre los grupos y materias que el Coordinador Academico me asigno; el resto del colegio no me aparece. Cuando el periodo cierra, el sistema bloquea la edicion y mi nota queda firme.

**Criterios de aceptacion:**
El docente solo puede seleccionar grupos y materias que tiene asignados (RR-10); cualquier intento de cargar nota fuera de su asignacion se rechaza en frontend y backend (RR-02). Las notas se aceptan unicamente dentro de la escala valorativa configurada por el Rector y solo si el periodo esta abierto (RR-07); con el periodo cerrado el campo queda en solo lectura y editar exige el permiso configurable mas justificacion. Al guardar, el sistema recalcula el acumulado del estudiante segun el metodo de aprobacion vigente y deja registro de auditoria (quien, que, cuando) sobre cada cambio (RR-03). El docente no ve consolidados generales del grupo, solo el desempeno de su materia.

**Documentacion:**
- PRD: PRD-08 Docente
- Flow: Carga y edicion de notas por periodo
- Prototipo: (link de Figma)

**Flujo:**
`Periodo abierto / Docente en su materia asignada` -> MANUAL -> `Selecciona grupo, evaluacion y carga la nota dentro de la escala` -> AUTOMATICO -> `Valida asignacion (RR-10) y periodo (RR-07), recalcula acumulado, registra auditoria (RR-03) y confirma guardado`
