---
titulo: Nivelaciones y habilitaciones
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [nivelacion, habilitacion, recuperacion, plan-de-mejoramiento]
---

# Nivelaciones y habilitaciones

Procesos de recuperación cuando un estudiante pierde una materia. Difieren en el momento del año en que se ejecutan.

## Conceptos

| Concepto | Cuándo se dispara | Alcance |
| --- | --- | --- |
| **Nivelación** | Al cierre de un periodo académico, si el estudiante perdió una materia. | Recupera la nota del periodo. |
| **Habilitación** | Al cierre del año lectivo, si el estudiante perdió una materia en el cómputo anual. | Recupera la nota anual de la materia. |

## Flujo principal

### Nivelación

1. Al cierre del periodo, el sistema identifica los estudiantes que perdieron alguna materia.
2. Para cada caso, se genera automáticamente un proceso de nivelación asociado a la materia y al periodo.
3. El docente titular registra la nota de la nivelación.
4. El sistema determina si el estudiante aprueba o no según la configuración del colegio (nota mínima, regla específica de nivelación si aplica).
5. Si aprueba, la nota del periodo queda corregida o se marca como recuperada según política del colegio.
6. El proceso queda registrado en el historial académico del estudiante.

### Habilitación

1. Al cierre del año lectivo, el sistema identifica los estudiantes con materias perdidas en el cómputo anual.
2. Genera automáticamente el proceso de habilitación.
3. El docente titular registra la nota de la habilitación.
4. El sistema evalúa el resultado según la configuración del colegio.
5. El resultado de la habilitación se considera en el [[promocion-y-reprobacion|proceso de promoción]] del estudiante.

## Plan de mejoramiento

Asociado a cualquier proceso de nivelación o habilitación, el docente puede registrar el plan de mejoramiento del estudiante:

- Descripción de las actividades de refuerzo.
- Fechas de ejecución.
- Compromisos específicos del estudiante.

Queda registrado en el sistema como parte del historial académico del estudiante.

## Estados y transiciones

```
Pendiente (autogenerado) → En proceso → Aprobada
                                      → No aprobada
                                      → Anulada (con motivo)
```

## Datos involucrados

- Estudiante.
- Materia.
- Periodo (para nivelación) o año lectivo (para habilitación).
- Nota original (la que disparó el proceso).
- Nota de la nivelación / habilitación.
- Resultado (aprobada / no aprobada).
- Plan de mejoramiento asociado (descripción, fechas, compromisos).
- Docente que registra.
- Fecha y hora del registro.

## Reglas de negocio

- **RN-NH-001 — Generación automática:** el sistema genera automáticamente los procesos de nivelación al cierre del periodo y de habilitación al cierre del año, sin intervención manual.
- **RN-NH-002 — Solo el docente titular registra:** la nota de nivelación / habilitación la registra exclusivamente el docente con asignación activa en la materia × grupo.
- **RN-NH-003 — Resultado afecta promoción:** el resultado de la habilitación se considera al ejecutar el [[promocion-y-reprobacion|proceso de promoción]].
- **RN-NH-004 — Plan de mejoramiento opcional:** el plan de mejoramiento es opcional pero recomendado. Si se registra, queda asociado al proceso.
- **RN-NH-005 — Inmutabilidad post-cierre del año:** los procesos de nivelación y habilitación de años cerrados son inmutables.
- **RN-NH-006 — Auditoría obligatoria:** registro y edición de notas de nivelación / habilitación quedan en el log.

## Notas y pendientes

- Definir si una nivelación aprobada sustituye la nota original del periodo o se promedia con ella (depende de política del colegio; por defecto sustituye).
- Definir si la habilitación tiene una fecha límite de ejecución antes del cierre definitivo del año.
- Definir si un estudiante puede tener múltiples nivelaciones simultáneas (recomendado: sí, una por materia perdida).
