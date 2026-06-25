---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - caso-de-uso
aliases:
  - CU RF-23
---

# ID: RF-23
**Nombre:** Consultar registro de asistencia y justificar inasistencias

**Historia:**
Como estudiante (o acudiente que opera su cuenta) quiero ver el registro de asistencia del estudiante y, cuando hay una inasistencia, adjuntar la justificacion desde el portal en lugar de llevar un papel a secretaria. Quiero entender que la justificacion no cambia el registro por si sola: queda pendiente hasta que el colegio la revise. Asi atiendo las inasistencias a tiempo y dejo trazabilidad.

**Criterios de aceptacion:**
El usuario autenticado por subdominio (RR-06) ve solo la asistencia del estudiante en contexto y, con varios hijos, debe seleccionarlo primero (RR-14, RR-01). El usuario puede consultar el detalle de cada falta pero no puede modificar el registro de asistencia: solo adjunta una justificacion (RN-PE-002). Al enviar la justificacion, la inasistencia no se marca como excusada de inmediato: queda en estado pendiente hasta que el Docente o Coordinador la apruebe o rechace (RN-PE-005), y el usuario recibe la notificacion del resultado por correo segun la configuracion del colegio (RF-44).

**Documentacion:**
- PRD: PRD-10 Estudiante y Acudiente
- Flow: Consulta de asistencia y justificacion de inasistencia
- Prototipo: (link de Figma)

**Flujo:**
`Inasistencia registrada por Docente (ROL-07)` -> MANUAL -> `Usuario inicia sesion, selecciona estudiante si aplica y abre el registro de asistencia` -> AUTOMATICO -> `Sistema valida scope (RR-14, RR-01) y muestra las faltas del estudiante en solo lectura` -> MANUAL -> `Usuario adjunta la justificacion de una inasistencia y la envia` -> AUTOMATICO -> `Sistema crea la justificacion en estado pendiente (RN-PE-005), enruta a revision (ROL-07/ROL-08) y notifica al usuario (RF-44)` -> `Resultado: inasistencia justificada pendiente de aprobacion/rechazo`
