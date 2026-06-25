---
tags:
  - arquitectura
  - rol/secretaria-academica
  - caso-de-uso
aliases:
  - CU RF-31
---

# ID: RF-31
**Nombre:** Asignar a grupo

**Historia:**
Como secretaria academica necesito asignar a cada estudiante inscrito a un grupo del grado correspondiente para completar su matricula. Hoy llevo el conteo de cupos por grupo en una hoja aparte y a veces se sobrepasa el cupo o se asigna a un grupo equivocado. Quiero asignar el grupo desde el sistema viendo el cupo disponible y cerrar la matricula cuando el estudiante quede ubicado.

**Criterios de aceptacion:**
La secretaria toma un estudiante inscrito con el checklist de documentos verificado y lo asigna a un grupo del grado que corresponde, eligiendo entre los grupos del catalogo del tenant (creado por Coordinador / Rector). El sistema muestra el cupo disponible del grupo e impide asignar por encima del cupo configurado. La asignacion solo puede hacerse con estudiantes y grupos del propio colegio (RR-01). El cambio de grupo despues de la matricula es una accion configurable (RR-05): si el Rector la restringio al Coordinador Academico, el sistema deshabilita esa accion para la secretaria. Toda asignacion o cambio de grupo queda en el log de auditoria (RR-03) con usuario, fecha, estudiante y grupo. Al asignar el grupo y estar completo el proceso, la secretaria puede marcar la matricula como completada.

**Documentacion:**
- PRD: PRD-07 Secretaria Academica
- Flow: Asignacion de grupo y cierre de matricula
- Prototipo: (link de Figma)

**Flujo:**
`Estudiante inscrito con documentos verificados` -> MANUAL -> `Seleccionar grupo del grado y confirmar asignacion` -> AUTOMATICO -> `Sistema valida cupo disponible y pertenencia al tenant (RR-01), aplica la regla configurable de cambio de grupo (RR-05), asigna el grupo y registra la accion en el log (RR-03)`
