---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-28
---

# ID: RF-28
**Nombre:** Citar formalmente a acudientes

**Historia:**
Como Coordinador Academico y de Convivencia necesito citar formalmente a los acudientes de un estudiante en el marco de un caso de convivencia o de un seguimiento academico, para dejar constancia oficial de la convocatoria dentro de la Ruta de Atencion Integral (Ley 1620). La citacion es un paso clave del debido proceso: documenta que la familia fue convocada, cuando y por que, sin exponer datos sensibles del caso en la notificacion.

**Criterios de aceptacion:**
La citacion formal es un permiso configurable: el sistema la habilita al coordinador segun la configuracion del colegio. Dentro de su propio colegio (RR-01), el coordinador puede generar una citacion asociada a un estudiante y a un caso de convivencia o seguimiento, indicando motivo, fecha y hora. El sistema notifica al acudiente por el portal y por correo (RF-43, RF-44) sin exponer informacion sensible en el cuerpo de la notificacion. El acudiente no es usuario de la plataforma con sesion propia para gestionar el caso: recibe la citacion como destinatario. Cada citacion queda registrada como actuacion del caso y en el log de auditoria del tenant (RR-03), de modo que sirva como evidencia del debido proceso. Si la citacion deriva de un caso tipo III, el coordinador la genera pero el caso sigue escalado al Rector (RN-CVE-004). El sistema permite registrar la confirmacion de asistencia del acudiente.

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Citacion formal a acudientes en la Ruta de Atencion Integral
- Prototipo: (link de Figma)

**Flujo:**
`Caso de convivencia clasificado o seguimiento academico abierto (RN-CVE-002)` -> MANUAL -> `Coordinador con permiso configurable genera la citacion con motivo, fecha y hora` -> AUTOMATICO -> `Sistema notifica al acudiente por portal y correo sin exponer datos sensibles (RF-43, RF-44)` -> MANUAL -> `Coordinador registra la confirmacion o inasistencia del acudiente` -> AUTOMATICO -> `Citacion guardada como actuacion del caso y registrada en el log de auditoria (RR-03) como evidencia del debido proceso`
