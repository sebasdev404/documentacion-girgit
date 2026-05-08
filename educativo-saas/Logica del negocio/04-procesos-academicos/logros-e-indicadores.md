---
titulo: Logros e indicadores
modulo: procesos-academicos
tipo: referencia
estado: borrador
tags: [logros, indicadores, desempeno]
---

# Logros e indicadores

Cada materia tiene definidos por periodo sus logros o indicadores de desempeño esperados. El docente marca por cada estudiante si alcanzó o no cada logro durante el periodo. Esta información aparece en el boletín junto a las notas.

## Estructura

| Atributo | Descripción |
| --- | --- |
| Logro / indicador | Descripción del objetivo de aprendizaje. |
| Materia | A qué materia pertenece. |
| Periodo | A qué periodo académico aplica. |
| Año lectivo | Año lectivo activo. |
| Orden | Posición dentro del listado de logros del periodo. |

Por cada estudiante del grupo, el docente registra el estado del logro:

- **Alcanzado**
- **No alcanzado**
- **En proceso** (opcional, si el colegio lo activa)

## Quién gestiona

Los logros son configurables por el [[roles/02-coordinador-academico|Coordinador Académico]] **o por el propio docente** según los permisos que el colegio haya definido para cada rol. La política por defecto es:

- El coordinador académico define el catálogo institucional de logros por materia y periodo (si el colegio quiere uniformidad).
- El docente puede agregar logros adicionales a sus asignaciones (si el colegio lo permite).
- El docente registra el estado por estudiante.

## Implicación en el boletín

Los logros aparecen en el boletín del estudiante junto a las notas, agrupados por materia. El colegio puede configurar:

- Mostrar logros con su estado por estudiante.
- Mostrar solo los logros no alcanzados (para resaltar áreas de refuerzo).
- Ocultar la sección de logros completamente.

## Reglas de negocio

- **RN-LI-001 — Logros por periodo:** cada logro pertenece a un periodo específico. No hay logros transversales al año lectivo desde la estructura de datos.
- **RN-LI-002 — Marcado por estudiante:** el estado del logro se registra por estudiante. No es agregado por grupo.
- **RN-LI-003 — Edición restringida al docente titular:** solo el docente con asignación activa en la materia × grupo puede marcar el estado de logros.
- **RN-LI-004 — Inmutabilidad histórica:** logros de periodos cerrados son inmutables.
- **RN-LI-005 — Cierre de periodo bloquea edición:** una vez cerrado el periodo, no se pueden modificar los estados de los logros de ese periodo (excepto por intervención del superadministrador bajo solicitud formal).

## Notas y pendientes

- Definir si el colegio puede configurar más estados además de "alcanzado / no alcanzado" (ej. niveles cualitativos: superior, alto, básico, bajo).
- Definir si los logros pueden ser ponderados para incidir en la nota final (recomendado: no en el lanzamiento, mantenerlos como información cualitativa).
