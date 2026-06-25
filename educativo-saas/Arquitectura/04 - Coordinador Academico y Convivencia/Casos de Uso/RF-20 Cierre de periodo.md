---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-20
---

# ID: RF-20
**Nombre:** Cierre de periodo academico

**Historia:**
Como Coordinador Academico y de Convivencia necesito ejecutar el cierre del periodo academico una vez que los docentes han cargado todas las notas y los consolidados estan validados, para consolidar oficialmente las calificaciones del periodo y disparar los procesos derivados. El cierre es un hito sensible: a partir de el las notas dejan de ser editables salvo excepcion configurada, y se generan automaticamente las nivelaciones de quienes perdieron materia.

**Criterios de aceptacion:**
El coordinador solo puede ejecutar el cierre del periodo dentro de su propio colegio (RR-01) y solo cuando el sistema confirma que no quedan notas faltantes obligatorias en los consolidados de los grupos; si hay faltantes, el sistema bloquea el cierre e indica que grupos y materias estan incompletos. Al ejecutar el cierre, las notas del periodo quedan bloqueadas para edicion: editarlas despues exige el permiso configurable activado por el colegio mas una justificacion obligatoria (RR-07), y ese cambio queda en el log. El cierre dispara automaticamente la generacion de las nivelaciones para los estudiantes que perdieron materia (RN-NH-001), sin que el coordinador las cree manualmente. El cierre es una accion sensible que queda registrada en el log de auditoria del tenant (RR-03) con autor y fecha. El coordinador puede ver el consolidado de todos los grupos del tenant antes de cerrar (RF-19).

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Cierre de periodo academico y disparo de nivelaciones
- Prototipo: (link de Figma)

**Flujo:**
`Periodo abierto con consolidados cargados por los docentes (RF-18, RF-19)` -> MANUAL -> `Coordinador valida los consolidados y activa el cierre del periodo` -> AUTOMATICO -> `Sistema verifica que no haya notas faltantes obligatorias y bloquea el cierre si las hay` -> MANUAL -> `Coordinador confirma el cierre del periodo` -> AUTOMATICO -> `Notas bloqueadas para edicion (RR-07), nivelaciones generadas automaticamente (RN-NH-001) y cierre registrado en el log de auditoria (RR-03)`
