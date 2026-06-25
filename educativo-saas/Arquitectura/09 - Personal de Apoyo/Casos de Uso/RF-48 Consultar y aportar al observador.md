---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - caso-de-uso
aliases:
  - CU RF-48
---

# ID: RF-48
**Nombre:** Consultar y aportar al observador del estudiante

**Historia:**
Como personal de apoyo (orientador, enfermeria o bibliotecario) necesito consultar la ficha acotada de un estudiante y dejar constancia de mi intervencion en el observador, para que el equipo correcto tenga el contexto sin que yo acceda al expediente academico completo. Cada anotacion debe nacer con un nivel de visibilidad controlado (`RN-OB-081`), por defecto interna, porque manejo informacion sensible de bienestar y salud. La consulta y el aporte quedan auditados (`RN-TU-009`) para garantizar trazabilidad.

**Criterios de aceptacion:**
El funcionario solo ve la ficha acotada del estudiante (identificacion, grupo, contacto del acudiente y alertas basicas) y nunca calificaciones, boletines ni configuracion del tenant (`RN-TU-002`, `RN-TU-006`); al crear una anotacion el sistema exige seleccionar un nivel de visibilidad de `RN-OB-081` y propone "interna" por defecto (`RN-TU-005`); la anotacion se guarda asociada al estudiante, al autor y a la marca de tiempo; tanto la consulta de la ficha como el aporte se registran en el log de auditoria inmutable con quien, que, cuando e IP (`RR-03`, `RNF-02`); el rol no puede decidir sanciones ni promocion a partir de la anotacion, solo dejar constancia o remitir (`RN-TU-010`).

**Documentacion:**
- PRD: PRD-11 Personal de Apoyo
- Flow: Consulta de ficha acotada y aporte al observador
- Prototipo: (link de Figma)

**Flujo:**
`Estudiante con ficha acotada disponible` -> MANUAL -> `Personal de apoyo abre la ficha y redacta la anotacion eligiendo visibilidad RN-OB-081` -> AUTOMATICO -> `Sistema guarda la anotacion con visibilidad (default interna), la asocia al estudiante y registra consulta y aporte en el log de auditoria (anotacion publicada en el observador)`
