---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-14
---

# ID: RF-14
**Nombre:** Designar director de grupo

**Historia:**
Como Coordinador Academico y de Convivencia necesito designar que docente sera el director de cada grupo, para que ese docente asuma el seguimiento integral del grupo: observador, generacion de boletines del grupo y comunicacion con acudientes. El director de grupo es la cara visible del grupo ante las familias y un eslabon clave del seguimiento academico y de convivencia.

**Criterios de aceptacion:**
El coordinador puede designar como director de grupo a un docente activo del propio colegio (RR-01), preferentemente uno ya asignado a una materia del grupo. Un grupo solo puede tener un director de grupo vigente a la vez; al designar un nuevo director, el sistema reemplaza al anterior y deja constancia del cambio. Como consecuencia de la designacion, los permisos extendidos del director de grupo (anotar en el observador de todo el grupo, generar el boletin del grupo, comunicarse con sus acudientes) aplican unicamente sobre el grupo designado y no sobre otros (RR-09); el sistema acota ese alcance. El coordinador puede quitar la designacion dejando el grupo temporalmente sin director, lo que el dashboard reporta como pendiente. Toda designacion o cambio queda registrado en el log de auditoria del tenant (RR-03).

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Designacion del director de grupo
- Prototipo: (link de Figma)

**Flujo:**
`Grupo creado con docentes asignados (RF-12, RF-13)` -> MANUAL -> `Coordinador selecciona el grupo y designa un docente activo como director de grupo` -> AUTOMATICO -> `Sistema valida que sea docente activo del tenant y reemplaza al director anterior si existia` -> MANUAL -> `Coordinador confirma la designacion` -> AUTOMATICO -> `Director de grupo habilitado solo sobre ese grupo (RR-09); designacion registrada en el log de auditoria (RR-03) y reflejada en el dashboard`
