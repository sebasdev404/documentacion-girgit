---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-11
---

# ID: RF-11
**Nombre:** Gestionar plan de estudios

**Historia:**
Como Coordinador Academico y de Convivencia necesito definir y mantener el plan de estudios del colegio: que materias existen por grado, su intensidad horaria semanal y el area del conocimiento a la que pertenecen. Esta es la base estructural del ano: sobre el plan de estudios se construyen luego los grupos, las asignaciones de docentes, los horarios y las notas. Si el plan de estudios esta mal definido, todo lo que viene despues queda inconsistente.

**Criterios de aceptacion:**
El coordinador puede crear, editar y archivar materias por grado dentro de su propio colegio (RR-01), asignando a cada una su intensidad horaria semanal y el area del conocimiento del catalogo del tenant. El sistema no permite guardar una materia sin grado, sin intensidad horaria o sin area asociada. El coordinador NO puede modificar la escala valorativa, el modelo pedagogico ni el calendario, porque son configuracion base del tenant que solo administra el Rector (ROL-02); el sistema bloquea cualquier intento. Archivar una materia no la elimina: se conserva para la trazabilidad de anos anteriores y deja de estar disponible para nuevas asignaciones. La intensidad horaria definida aqui es la referencia que el modulo de horarios (RF-15) usa para advertir si una materia queda por debajo o por encima de su carga. Toda creacion, edicion o archivo de materia queda registrada en el log de auditoria del tenant (RR-03).

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Definicion y mantenimiento del plan de estudios
- Prototipo: (link de Figma)

**Flujo:**
`Configuracion base del tenant definida por el Rector (areas, grados, calendario)` -> MANUAL -> `Coordinador crea o edita una materia indicando grado, intensidad horaria semanal y area del conocimiento` -> AUTOMATICO -> `Sistema valida grado, intensidad y area obligatorios y bloquea cambios sobre la configuracion base` -> MANUAL -> `Coordinador guarda o archiva la materia` -> AUTOMATICO -> `Materia disponible para grupos, asignaciones y horarios; cambio registrado en el log de auditoria (RR-03)`
