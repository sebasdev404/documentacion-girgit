---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - caso-de-uso
aliases:
  - CU RF-28
---

# ID: RF-28
**Nombre:** Citar formalmente a acudientes

**Historia:**
Como Coordinador de Convivencia necesito citar formalmente al acudiente de un estudiante cuando una situacion de convivencia requiere su presencia, dejando constancia de la citacion y su motivo. La citacion debe registrarse en el observador del estudiante y notificarse por el canal correspondiente, para sustentar el seguimiento del caso y cumplir el protocolo.

**Criterios de aceptacion:**
El sistema permite generar una citacion para el acudiente de un estudiante del propio tenant (RR-01), capturando motivo, fecha y hora propuestas y, si aplica, el caso de convivencia asociado. La funcionalidad de citacion es configurable por el colegio: si esta desactivada en la configuracion del tenant, la accion no esta disponible (RR-05). Al confirmar, el sistema notifica al acudiente a traves del modulo de Comunicaciones, deja constancia de la citacion en el observador del estudiante y registra la accion en el log inmutable (RR-03). El sistema rechaza el envio si falta el motivo o la fecha. El Coordinador no firma actas del Comite Escolar ni reporta casos tipo III a la autoridad; esas acciones quedan reservadas al Rector (ROL-02).

**Documentacion:**
- PRD: PRD-05 Coordinador de Convivencia
- Flow: Citacion formal a acudiente
- Prototipo: (link de Figma)

**Flujo:**
`Caso de convivencia que requiere presencia del acudiente` -> MANUAL -> `Coordinador genera la citacion con motivo, fecha/hora y caso asociado (si la funcionalidad esta habilitada, RR-05)` -> AUTOMATICO -> `Notificacion al acudiente via Comunicaciones, constancia en el observador del estudiante y registro en log inmutable (RR-03)`
