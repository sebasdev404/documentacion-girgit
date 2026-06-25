---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - caso-de-uso
aliases:
  - CU RF-44
---

# ID: RF-44
**Nombre:** Recibir notificaciones de remisiones, citas y vencimientos

**Historia:**
Como personal de apoyo necesito recibir notificaciones de las remisiones que me llegan, las citas agendadas en mi modulo de servicio y los vencimientos propios de mi perfil (devoluciones de biblioteca, controles de salud o seguimientos de bienestar), para responder a tiempo sin tener que vigilar manualmente cada modulo. Las notificaciones deben informarme el evento sin exponer datos sensibles del motivo, ya que el detalle vive protegido dentro del modulo correspondiente.

**Criterios de aceptacion:**
El sistema genera una notificacion automatica cuando ocurre un evento que involucra a este funcionario (remision interna recibida, cita agendada o vencimiento de su perfil) y la entrega solo al destinatario correcto segun su perfil (`RN-TU-004`); la notificacion muestra el tipo de evento, el estudiante o item afectado y la fecha, pero no expone el motivo sensible en el cuerpo del aviso; al abrir la notificacion el funcionario es llevado a la ficha acotada o al item dentro de su propio modulo de servicio, nunca al de otro perfil; el rol no decide a partir de la notificacion, solo atiende o remite (`RN-TU-010`); la generacion y entrega de la notificacion queda registrada para trazabilidad (`RR-03`).

**Documentacion:**
- PRD: PRD-11 Personal de Apoyo
- Flow: Notificaciones de remisiones, citas y vencimientos
- Prototipo: (link de Figma)

**Flujo:**
`Evento generado (remision recibida / cita agendada / vencimiento del perfil)` -> AUTOMATICO -> `Sistema identifica al destinatario por su perfil y crea la notificacion sin motivo sensible` -> MANUAL -> `Personal de apoyo abre la notificacion y atiende el item dentro de su modulo de servicio` -> AUTOMATICO -> `Sistema marca la notificacion como leida y registra la entrega en el log`
