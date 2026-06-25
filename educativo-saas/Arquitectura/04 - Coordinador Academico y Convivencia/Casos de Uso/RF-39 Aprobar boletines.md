---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-39
---

# ID: RF-39
**Nombre:** Aprobar / firmar boletines

**Historia:**
Como Coordinador Academico y de Convivencia, cuando el colegio delega en mi la firma de boletines, necesito revisar y aprobar los boletines que generan los directores de grupo antes de que se publiquen a los acudientes. La aprobacion es el control de calidad final del periodo: garantiza que las notas, observaciones y el consolidado del estudiante esten correctos antes de hacerse oficiales para las familias.

**Criterios de aceptacion:**
La aprobacion / firma de boletines es un permiso configurable: el sistema solo habilita esta accion al coordinador si el colegio la delego en el; de lo contrario queda en el Rector. Dentro de su propio colegio (RR-01), el coordinador puede revisar los boletines generados por el Director de Grupo (RF-38) y, sobre cada uno, aprobarlo / firmarlo o devolverlo con una observacion obligatoria al director para correccion. El sistema solo permite aprobar boletines de periodos ya cerrados (RF-20) y bloquea la aprobacion si el boletin tiene notas faltantes. El boletin aprobado pasa al estado que habilita su publicacion a los acudientes; el devuelto vuelve a borrador con la observacion. El coordinador no genera el boletin, solo lo aprueba. Toda aprobacion, firma o devolucion queda registrada en el log de auditoria del tenant (RR-03) con autor y fecha.

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Revision y aprobacion de boletines
- Prototipo: (link de Figma)

**Flujo:**
`Director de grupo genera el boletin del grupo sobre un periodo cerrado (RF-38, RF-20)` -> MANUAL -> `Coordinador con permiso configurable revisa el boletin del estudiante` -> AUTOMATICO -> `Sistema valida que el periodo este cerrado y que no falten notas` -> MANUAL -> `Coordinador aprueba / firma el boletin o lo devuelve con observacion obligatoria` -> AUTOMATICO -> `Boletin aprobado habilitado para publicacion a acudientes o devuelto a borrador; accion registrada en el log de auditoria (RR-03)`
