---
tags:
  - arquitectura
  - rol/docente
  - caso-de-uso
aliases:
  - CU RF-22
---

# ID: RF-22
**Nombre:** Registrar asistencia en clase propia

**Historia:**
Como docente quiero tomar asistencia de cada clase desde el celular en el aula, marcando presentes, ausentes y tardanzas en pocos toques, para no perder tiempo de clase y dejar el registro al instante. Solo veo la lista de los grupos y materias que dicto (RR-10); el sistema me arma la clase del dia segun mi horario y guarda quien asistio sin que yo tenga que llevar planillas en papel.

**Criterios de aceptacion:**
El sistema muestra al docente unicamente las clases de su horario y los estudiantes del grupo y materia asignados (RR-10); no puede tomar asistencia de una clase que no dicta y la accion se valida en frontend y backend (RR-02). Cada estudiante admite un unico estado por sesion (presente, ausente o tardanza) y el registro queda asociado a la fecha, hora y materia de esa clase. Al guardar, el sistema persiste la asistencia, deja auditoria de quien la registro y cuando (RR-03) y refleja el consolidado de inasistencias del estudiante en su materia. Si el docente edita una asistencia ya guardada, el cambio queda trazado.

**Documentacion:**
- PRD: PRD-08 Docente
- Flow: Toma de asistencia por sesion de clase
- Prototipo: (link de Figma)

**Flujo:**
`Clase del dia en horario propio / Docente en su grupo asignado` -> MANUAL -> `Marca presente, ausente o tardanza por estudiante y confirma` -> AUTOMATICO -> `Valida asignacion y horario (RR-10), persiste la asistencia, registra auditoria (RR-03) y actualiza el consolidado de inasistencias`
