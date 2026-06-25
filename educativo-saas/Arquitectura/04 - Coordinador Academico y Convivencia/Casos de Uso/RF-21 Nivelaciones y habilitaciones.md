---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-21
---

# ID: RF-21
**Nombre:** Gestion de nivelaciones y habilitaciones

**Historia:**
Como Coordinador Academico y de Convivencia necesito supervisar las nivelaciones del periodo y las habilitaciones del ano que el sistema genera automaticamente al cierre, para asegurar que los docentes titulares registren las notas de recuperacion dentro del plazo y que los planes de mejoramiento queden cargados. Mi rol aqui es coordinar y hacer seguimiento, no calificar: la nota de recuperacion siempre la pone el docente titular de la materia.

**Criterios de aceptacion:**
El coordinador puede ver, dentro de su propio colegio (RR-01), todos los procesos de nivelacion (al cierre de periodo) y de habilitacion (al cierre de ano) que el sistema genero automaticamente para los estudiantes que perdieron materia (RN-NH-001), filtrandolos por grupo, materia y estado. El coordinador NO puede registrar ni modificar la nota de recuperacion: esa accion esta reservada al docente titular de la materia x grupo (RN-NH-002, RF-04 / restriccion del rol); el sistema le impide editar la nota. El coordinador puede hacer seguimiento del avance, revisar que el plan de mejoramiento este cargado y anular un proceso con motivo obligatorio cuando proceda, quedando la anulacion en el log. El sistema muestra los procesos vencidos o sin nota dentro del plazo para alertar al coordinador. Toda anulacion o cambio de estado queda registrado en el log de auditoria del tenant (RR-03).

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Seguimiento de nivelaciones y habilitaciones
- Prototipo: (link de Figma)

**Flujo:**
`Cierre de periodo o de ano ejecutado (RF-20)` -> AUTOMATICO -> `Sistema genera nivelaciones / habilitaciones para los estudiantes que perdieron materia (RN-NH-001)` -> MANUAL -> `Coordinador supervisa los procesos, revisa planes de mejoramiento y plazos sin registrar notas (RN-NH-002)` -> MANUAL -> `Docente titular registra la nota de recuperacion; coordinador anula con motivo si procede` -> AUTOMATICO -> `Estado del proceso actualizado y cambios registrados en el log de auditoria (RR-03)`
