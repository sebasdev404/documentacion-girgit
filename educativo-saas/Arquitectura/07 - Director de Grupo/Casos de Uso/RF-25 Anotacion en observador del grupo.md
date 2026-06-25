---
tags:
  - arquitectura
  - rol/director-de-grupo
  - caso-de-uso
aliases:
  - CU RF-25
---

# ID: RF-25
**Nombre:** Anotacion en observador del grupo

**Historia:**
Como Director de Grupo necesito registrar anotaciones en el observador disciplinario de los estudiantes de mi grupo cuando ocurre una situacion academica o de convivencia que debe quedar documentada. La anotacion deja constancia del hecho, su tipologia segun el manual de convivencia del colegio y, si corresponde, la articula con un caso de convivencia (RN-CVE-007). Esta accion solo aplica sobre estudiantes del grupo que dirijo (RR-09); sobre otros estudiantes no puedo anotar.

**Criterios de aceptacion:**
El sistema permite al Director de Grupo crear una anotacion en el observador unicamente para estudiantes de su grupo dirigido (RR-09) y la bloquea para cualquier estudiante fuera de ese grupo; la anotacion exige seleccionar el estudiante, el tipo segun la tipologia del colegio y una descripcion del hecho, y admite adjuntar evidencia y solicitar la confirmacion del acudiente; cada anotacion respeta la visibilidad configurada por anotacion (RN-OB-081), de modo que el acudiente ve solo lo que le corresponde a traves de la cuenta del Estudiante (RR-11); toda anotacion queda registrada en el log de auditoria del tenant (RR-03) con autor, fecha y estudiante; y si la situacion se articula con convivencia, el sistema genera la anotacion correspondiente vinculada al caso (RN-CVE-007).

**Documentacion:**
- PRD: PRD-09 Director de Grupo
- Flow: Registro de anotacion en el observador del grupo
- Prototipo: (link de Figma)

**Flujo:**
`Estudiante del grupo dirigido con una situacion a documentar` -> MANUAL -> `Director abre el observador del estudiante, clasifica el tipo segun la tipologia del colegio, redacta la anotacion y adjunta evidencia` -> AUTOMATICO -> `El sistema valida que el estudiante pertenece al grupo dirigido (RR-09), guarda la anotacion aplicando la visibilidad configurada (RN-OB-081), notifica al acudiente via la cuenta del Estudiante (RR-11) si se solicita confirmacion, articula la anotacion con el caso de convivencia cuando aplica (RN-CVE-007) y registra el evento en el log del tenant (RR-03)`
