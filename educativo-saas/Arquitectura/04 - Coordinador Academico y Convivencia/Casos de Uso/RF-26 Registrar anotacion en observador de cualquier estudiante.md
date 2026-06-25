---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-26
---

# ID: RF-26
**Nombre:** Registrar anotacion en observador de cualquier estudiante

**Historia:**
Como Coordinador Academico y de Convivencia necesito registrar anotaciones en el observador de cualquier estudiante del colegio, no solo de un grupo, para dejar constancia de hechos academicos o de convivencia que requieren seguimiento. A diferencia del docente, que solo anota sobre sus grupos, mi alcance es transversal a todo el tenant, lo que me permite documentar situaciones que escalan o que cruzan varios grupos dentro del marco de la Ley 1620.

**Criterios de aceptacion:**
El coordinador puede abrir el observador de cualquier estudiante de su propio colegio (RR-01) y registrar una anotacion eligiendo una tipologia del catalogo de tipologias de anotacion (RF-27) y una visibilidad obligatoria: publica, solo docentes o interna (RN-OB-081). El sistema no permite guardar una anotacion sin tipologia ni sin nivel de visibilidad. Cada anotacion registrada queda asociada al estudiante, al autor y a la fecha, y se escribe en el log de auditoria del tenant (RR-03) por ser una accion sensible. Si la anotacion corresponde a un hecho de convivencia que debe convertirse en caso, el sistema permite escalarla al flujo de convivencia donde se exige clasificacion I/II/III antes de avanzar (RN-CVE-002). La anotacion respeta su visibilidad: una marcada como interna no es visible para el acudiente ni para los docentes no autorizados.

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Registro de anotacion en el observador del estudiante
- Prototipo: (link de Figma)

**Flujo:**
`Coordinador abre el observador de cualquier estudiante del colegio` -> MANUAL -> `Selecciona estudiante, tipologia (RF-27) y visibilidad publica / docentes / interna (RN-OB-081)` -> AUTOMATICO -> `Sistema valida tipologia y visibilidad obligatorias y bloquea el guardado si faltan` -> MANUAL -> `Coordinador redacta y guarda la anotacion` -> AUTOMATICO -> `Anotacion asociada al estudiante con autor y fecha, registrada en el log de auditoria y disponible para escalar al flujo de convivencia (RN-CVE-002)`
