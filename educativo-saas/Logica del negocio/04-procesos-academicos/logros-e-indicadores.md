---
titulo: Logros e indicadores
modulo: procesos-academicos
tipo: referencia
estado: vigente en desarrollo local
tags: [logros, indicadores, desempeno]
---

# Logros e indicadores

Un indicador describe el aprendizaje esperado de una asignatura para un grado y un período. No se califica por separado para cada estudiante. El desempeño individual se expresa mediante las notas calculadas según el SIEE y las observaciones del boletín. La corrección de esta regla, decidida el 19 de octubre de 2026, reemplaza las propuestas anteriores de escalas, caritas y estados «alcanzado / en proceso / no alcanzado» para indicadores.

## Alcance del texto

| Elemento | Comportamiento |
| --- | --- |
| Base institucional | Texto reutilizable, con revisión y orden. |
| Vínculo curricular | Año lectivo, grado, asignatura y todos los períodos reales o los seleccionados. |
| Variante por grupo | Redacción específica para un grupo y período, sin alterar otros grupos ni la base común. |
| Histórico | Un vínculo conserva su revisión institucional hasta que un gestor adopte expresamente otra; la emisión del boletín conserva el texto visible en su snapshot. |

El Rector o un rol autorizado con `indicadores.base.gestionar` administra el catálogo institucional. Un docente con asignación activa puede consultar los indicadores de su asignatura y grupo. Solo puede redactar una variante de **ese grupo** si el Rector habilita `docente_edita_indicadores_grupo` y el rol tiene `indicadores.grupo.editar`; el mismo permiso no autoriza editar la base ni otro grupo.

## Relación con la evaluación y el boletín

El boletín presenta el texto descriptivo aplicable al período, grado, asignatura y grupo. La nota de la asignatura, la escala SIEE y la observación individual son datos distintos; ningún indicador tiene opción, número, porcentaje, estado de logro o umbral propio. Una asignatura reprobada se reconoce por su resultado académico, no por una supuesta valoración pendiente del indicador. La emisión individual no se bloquea por falta de una valoración inexistente.

## Reglas de negocio

- **RN-LI-001 — Texto reutilizable:** la base institucional puede vincularse a otro año sin duplicar el texto y un vínculo puede limitarse a períodos concretos.
- **RN-LI-002 — Alcance docente:** la consulta exige asignación vigente de asignatura y grupo; la variante requiere además permiso efectivo y política institucional activa. La API comprueba el alcance aunque la interfaz oculte controles.
- **RN-LI-003 — Revisión histórica:** una redacción nueva no reescribe vínculos anteriores ni snapshots ya emitidos.
- **RN-LI-004 — Cierre:** no se modifica ordinariamente una variante que afecte un período cerrado. Una corrección histórica exige un procedimiento auditado específico.
- **RN-LI-005 — Sin valoración independiente:** no existen escalas ni registros de logro por estudiante para indicadores; las notas siguen las reglas SIEE y las observaciones conservan su propio flujo.

La implementación local y la retirada de las tablas y permisos anteriores se describen en `colegio-saas-backend/docs/INDICADORES_ACADEMICOS.md`. Una implementación en otro entorno con datos antiguos de valoración debe respaldarlos y definir su tratamiento antes de aplicar la migración correctiva; esa migración se detiene si encuentra registros.
