---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - caso-de-uso
aliases:
  - CU RF-26
---

# ID: RF-26
**Nombre:** Registrar anotacion en observador de cualquier estudiante

**Historia:**
Como Coordinador de Convivencia necesito registrar una anotacion en el observador de cualquier estudiante del colegio cuando un docente o director de grupo reporta una situacion de comportamiento. Cada anotacion debe quedar tipificada, con un nivel de visibilidad definido y con trazabilidad total, para mantener un historial confiable y cumplir la Ley 1620.

**Criterios de aceptacion:**
El sistema permite seleccionar a cualquier estudiante del tenant y crear una anotacion eligiendo una tipologia (RF-27) y uno de los tres niveles de visibilidad: publica, docentes o interna (RN-OB-081). Al guardar, la anotacion se incorpora al observador del estudiante con fecha, autor y tipo, y queda registrada en el log inmutable de acciones sensibles (RR-03). El Coordinador solo puede operar sobre estudiantes de su propio colegio (RR-01). Una anotacion no se borra: si se anula, se conserva como anulada con justificacion (RN-OE-003). El sistema notifica segun la visibilidad elegida y rechaza el guardado si falta tipologia o nivel de visibilidad.

**Documentacion:**
- PRD: PRD-05 Coordinador de Convivencia
- Flow: Registro de anotacion en observador
- Prototipo: (link de Figma)

**Flujo:**
`Situacion reportada (docente / director de grupo)` -> MANUAL -> `Coordinador selecciona estudiante, elige tipologia y nivel de visibilidad, redacta y guarda la anotacion` -> AUTOMATICO -> `Anotacion incorporada al observador con fecha/autor/tipo, registro en log inmutable (RR-03) y notificacion segun visibilidad (RN-OB-081)`
