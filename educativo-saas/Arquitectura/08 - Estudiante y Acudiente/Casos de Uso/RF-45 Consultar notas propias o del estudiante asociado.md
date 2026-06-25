---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - caso-de-uso
aliases:
  - CU RF-45
---

# ID: RF-45
**Nombre:** Consultar notas propias o del estudiante asociado

**Historia:**
Como estudiante (o acudiente que opera su cuenta) quiero entrar al portal y ver las notas del estudiante en contexto, por periodo y por asignatura, sin pedirselas a la secretaria ni esperar la entrega fisica del boletin. Cuando hay varios hijos vinculados al mismo correo, primero elijo a cual estudiante quiero consultar. Asi sigo el desempeno academico al dia y con autonomia.

**Criterios de aceptacion:**
El usuario autenticado por el subdominio del colegio (RR-06) ve unicamente las notas del estudiante en contexto; si tiene varios estudiantes vinculados, el sistema exige usar el selector antes de mostrar datos y nunca fusiona expedientes (RR-14). Las notas se muestran agrupadas por periodo y asignatura, en modo de solo lectura: el usuario no puede crear, editar ni eliminar ninguna calificacion (RN-PE-002). El portal jamas expone notas de otro estudiante ni de otro colegio (RR-01), y si el colegio desactivo el portal el acceso queda bloqueado (RN-PE-001).

**Documentacion:**
- PRD: PRD-10 Estudiante y Acudiente
- Flow: Consulta de notas del estudiante
- Prototipo: (link de Figma)

**Flujo:**
`Notas publicadas por Docente (ROL-07)` -> MANUAL -> `Usuario inicia sesion por subdominio y, si tiene varios hijos, elige estudiante en el selector` -> AUTOMATICO -> `Sistema valida scope (RR-14, RR-01) y consulta calificaciones del estudiante en contexto` -> MANUAL -> `Usuario filtra por periodo / asignatura` -> AUTOMATICO -> `Sistema renderiza las notas en solo lectura, sin habilitar edicion (RN-PE-002)` -> `Resultado: notas del estudiante consultadas en pantalla`
