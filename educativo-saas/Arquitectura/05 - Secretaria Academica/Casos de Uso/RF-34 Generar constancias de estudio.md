---
tags:
  - arquitectura
  - rol/secretaria-academica
  - caso-de-uso
aliases:
  - CU RF-34
---

# ID: RF-34
**Nombre:** Generar constancias de estudio

**Historia:**
Como secretaria academica necesito emitir constancias de estudio para los estudiantes que las solicitan (tramites de subsidio, EPS, transporte o cambio de colegio). Hoy las redacto a mano en Word y las firmo sin consecutivo, lo que dificulta saber cuantas se emitieron y para quien. Quiero que el sistema genere la constancia con los datos oficiales del estudiante, le asigne consecutivo y la deje registrada para consulta posterior.

**Criterios de aceptacion:**
La secretaria selecciona un estudiante activo de su colegio, elige el tipo "Constancia de estudio" y el sistema genera el documento con la identidad del colegio (nombre, NIT, logo), los datos del estudiante (nombre, documento, grado y grupo vigente) y la fecha de emision. El documento recibe un consecutivo unico e irrepetible dentro del tenant, queda guardado en el modulo de gestion documental y la accion se registra en el log de auditoria (RR-03) con usuario, fecha y estudiante. Si el estudiante tiene documentos o pagos pendientes y el bloqueo esta activado (RR-08), el sistema advierte o bloquea la emision segun la configuracion del Rector. La constancia solo puede generarse para estudiantes del propio colegio (RR-01) y queda disponible para reimpresion sin generar un consecutivo nuevo.

**Documentacion:**
- PRD: PRD-07 Secretaria Academica
- Flow: Emision de documento oficial (constancia)
- Prototipo: (link de Figma)

**Flujo:**
`Estudiante activo seleccionado` -> MANUAL -> `Elegir tipo "Constancia de estudio" y confirmar emision` -> AUTOMATICO -> `Sistema valida pendientes (RR-08), genera el documento con datos oficiales, asigna consecutivo unico, lo archiva en gestion documental y registra la accion en el log (RR-03)`
