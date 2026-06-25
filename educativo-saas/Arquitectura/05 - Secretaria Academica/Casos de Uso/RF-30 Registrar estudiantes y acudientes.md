---
tags:
  - arquitectura
  - rol/secretaria-academica
  - caso-de-uso
aliases:
  - CU RF-30
---

# ID: RF-30
**Nombre:** Registrar estudiantes y acudientes

**Historia:**
Como secretaria academica necesito crear la ficha de cada estudiante nuevo y registrar a su acudiente operativo cuando una familia llega a matricular. Hoy capturo los datos en hojas de calculo y formularios fisicos, lo que duplica informacion y dificulta encontrar al contacto responsable del menor. Quiero registrar al estudiante con sus datos personales y al acudiente como contacto dentro de la misma ficha, dejando todo listo para iniciar el proceso de matricula.

**Criterios de aceptacion:**
La secretaria crea la ficha del estudiante con sus datos personales (nombre completo, tipo y numero de documento, fecha de nacimiento, grado al que aspira) y registra al menos un acudiente operativo como contacto dentro de la ficha (nombre, parentesco, telefono, correo), sin crear un usuario para el acudiente (RR-11, `RN-TU-410`). El menor queda con una unica cuenta de Estudiante. El sistema impide registrar un estudiante con un documento ya existente en el mismo colegio y el registro solo es visible dentro del propio tenant (RR-01). La creacion y posteriores ediciones quedan en el log de auditoria (RR-03) con usuario, fecha y registro afectado. Al guardar, el sistema solicita capturar el consentimiento de tratamiento de datos del menor (`RN-HD-001`) antes de continuar a matricula.

**Documentacion:**
- PRD: PRD-07 Secretaria Academica
- Flow: Alta de estudiante y acudiente operativo
- Prototipo: (link de Figma)

**Flujo:**
`Inscripcion de familia nueva` -> MANUAL -> `Capturar datos del estudiante y del acudiente operativo como contacto` -> AUTOMATICO -> `Sistema valida documento unico en el tenant (RR-01), crea la ficha del estudiante con el acudiente como contacto (RR-11), solicita el consentimiento de habeas data (RN-HD-001) y registra el alta en el log (RR-03)`
