---
tags:
  - arquitectura
  - rol/director-de-grupo
  - caso-de-uso
aliases:
  - CU RF-38
---

# ID: RF-38
**Nombre:** Generar boletin del grupo dirigido

**Historia:**
Como Director de Grupo necesito generar los boletines de mi grupo al cierre de cada periodo para entregar a las familias un informe consolidado del desempeno de cada estudiante. El boletin reune las notas de todas las materias, la asistencia y las observaciones, y es la base sobre la cual luego agrego la observacion general (RF-40). Esta accion solo aplica sobre el grupo que dirijo (RR-09).

**Criterios de aceptacion:**
El sistema permite al Director de Grupo generar los boletines de su grupo dirigido solo cuando el periodo esta cerrado y las notas estan consolidadas, produciendo un boletin por estudiante con notas de todas las materias, promedios, asistencia y observaciones; la generacion se restringe al grupo dirigido (RR-09) y queda bloqueada para cualquier otro grupo; el sistema impide generar si faltan notas obligatorias o el periodo sigue abierto (RR-07) y muestra el detalle de lo que falta; cada generacion queda registrada en el log de auditoria del tenant (RR-03) y respeta la visibilidad configurada de las anotaciones del observador hacia el acudiente (RN-OB-081). La aprobacion o firma del boletin es un paso configurable aparte (RF-39).

**Documentacion:**
- PRD: PRD-09 Director de Grupo
- Flow: Generacion de boletines del grupo
- Prototipo: (link de Figma)

**Flujo:**
`Periodo cerrado y notas consolidadas` -> MANUAL -> `Director solicita generar los boletines de su grupo` -> AUTOMATICO -> `El sistema valida el grupo dirigido (RR-09) y el cierre del periodo (RR-07), reune notas, asistencia y observaciones por estudiante respetando la visibilidad (RN-OB-081), arma un boletin por estudiante, los deja listos para observacion general (RF-40) y firma (RF-39), y registra la generacion en el log (RR-03)`
