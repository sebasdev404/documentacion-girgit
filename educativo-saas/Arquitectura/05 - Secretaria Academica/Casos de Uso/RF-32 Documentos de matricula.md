---
tags:
  - arquitectura
  - rol/secretaria-academica
  - caso-de-uso
aliases:
  - CU RF-32
---

# ID: RF-32
**Nombre:** Documentos de matricula

**Historia:**
Como secretaria academica necesito controlar los documentos de matricula de cada estudiante (registro civil, certificados de grados anteriores, fotos, afiliacion a EPS, consentimientos) para saber quien esta completo y quien tiene pendientes. Hoy reviso carpetas fisicas una por una y no tengo forma rapida de saber a quien le falta que. Quiero cargar y marcar los documentos en el sistema y mantener una lista de pendientes que alimente el bloqueo de emision.

**Criterios de aceptacion:**
La secretaria define los documentos requeridos por grado y, por cada estudiante, carga los archivos y los marca como recibido, pendiente o vencido, registrando fecha de recepcion y quien lo cargo. El sistema muestra la lista de pendientes por estudiante y global, y esa lista alimenta el bloqueo configurable de emision de documentos oficiales (RR-08). Los documentos solo son visibles y editables dentro del propio colegio (RR-01) y cada carga o cambio de estado queda en el log de auditoria (RR-03) con usuario, fecha y documento afectado. Un documento marcado como recibido no puede quedar sin archivo adjunto asociado. Los consentimientos de habeas data se gestionan como documentos de matricula vinculados al estudiante (`RN-HD-001`).

**Documentacion:**
- PRD: PRD-07 Secretaria Academica
- Flow: Recepcion y control de documentos de matricula
- Prototipo: (link de Figma)

**Flujo:**
`Documentos fisicos o digitales recibidos de la familia` -> MANUAL -> `Cargar el documento y marcar su estado (recibido / pendiente / vencido)` -> AUTOMATICO -> `Sistema guarda el archivo restringido al tenant (RR-01), actualiza la lista de pendientes que alimenta el bloqueo (RR-08) y registra la accion en el log (RR-03)`
