---
tags:
  - arquitectura
  - rol/coordinador-academico
  - caso-de-uso
aliases:
  - CU RF-20
---

# ID: RF-20
**Nombre:** Cierre de periodo academico

**Historia:**
Como Coordinador Academico, al terminar cada periodo necesito cerrarlo para consolidar las notas que los docentes cargaron y habilitar la generacion de boletines. El cierre es una accion sensible e irreversible por la via normal: una vez cerrado, las notas quedan congeladas y solo pueden tocarse bajo permiso configurable y justificacion (RR-07), por lo que debo confirmar que todo este completo antes de activarlo.

**Criterios de aceptacion:**
El sistema solo permite iniciar el cierre cuando el periodo esta en estado abierto dentro del calendario academico de la configuracion base. Antes de confirmar, el sistema verifica que todos los grupos y materias tengan sus notas cargadas y muestra un consolidado de pendientes (RF-18); si existen materias sin nota, advierte y lista los faltantes sin bloquear necesariamente, segun la politica del tenant. Al confirmar el cierre, el sistema cambia el estado del periodo a cerrado, congela las notas para edicion directa, habilita la generacion de boletines (RF-39) y registra la accion con autor y fecha en auditoria (RR-03). Tras el cierre, cualquier edicion de notas requiere el permiso configurable de edicion post-cierre mas una justificacion (RR-07).

**Documentacion:**
- PRD: PRD-04 Coordinador Academico
- Flow: Cierre de periodo y consolidacion de notas
- Prototipo: (link de Figma)

**Flujo:**
`Periodo abierto + docentes cargaron notas durante el periodo` -> MANUAL -> `Coordinador revisa consolidados y pulsa Cerrar periodo` -> AUTOMATICO -> `Sistema valida notas pendientes por grupo/materia y muestra faltantes (RF-18)` -> MANUAL -> `Coordinador confirma el cierre` -> AUTOMATICO -> `Periodo pasa a estado cerrado; notas congeladas (RR-07); boletines habilitados (RF-39); accion registrada en auditoria (RR-03)`
