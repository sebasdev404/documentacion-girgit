---
tags:
  - arquitectura
  - rol/rector
  - caso-de-uso
aliases:
  - CU RF-39
---

# ID: RF-39
**Nombre:** Aprobar y firmar boletines

**Historia:**
Como Rector necesito revisar y firmar los boletines del periodo una vez que las notas estan cerradas, porque mi firma es el acto que oficializa los resultados academicos ante familias y autoridades. Antes de firmar quiero confirmar que el cierre del periodo se completo y que los consolidados estan consistentes, de modo que mi aprobacion sea trazable y los boletines queden disponibles para entrega.

**Criterios de aceptacion:**
El Rector solo puede firmar boletines de periodos cuyo cierre academico ya fue coordinado y completado (RF-20); si hay periodos abiertos o notas pendientes, el sistema bloquea la firma y lo indica. La aprobacion puede ser por grupo o por el colegio entero, y al firmar el sistema genera la version oficial de los boletines, registra la firma con autor, fecha y alcance en el log de auditoria inmutable (RR-03, RNF-03) y habilita los boletines para consulta y entrega a las familias. La accion se valida en frontend y backend (RR-02, RNF-02) y queda restringida al tenant del Rector (RR-01). Si despues de firmar se requiere editar una nota, esta solo procede con permiso configurable y justificacion (RR-07, RF-17), y la correccion queda igualmente auditada.

**Documentacion:**
- PRD: PRD-03 Rector
- Flow: Aprobacion y firma de boletines de periodo
- Prototipo: (link de Figma)

**Flujo:**
`Periodo academico cerrado con consolidados disponibles (RF-20)` -> MANUAL -> `Rector revisa los consolidados y firma los boletines por grupo o del colegio entero` -> AUTOMATICO -> `Sistema verifica que el periodo este cerrado, genera la version oficial de los boletines, registra la firma en el log de auditoria con autor/fecha/alcance (RR-03) y los habilita para consulta y entrega a las familias`
