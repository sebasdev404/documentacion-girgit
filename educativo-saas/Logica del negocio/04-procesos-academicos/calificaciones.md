---
titulo: Calificaciones
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [calificaciones, notas, proceso]
---

# Calificaciones

## Descripción

Proceso por el cual los docentes registran las notas de los estudiantes en las materias y grupos a los que están asignados, y el sistema calcula las notas finales del periodo y del año según la configuración del colegio.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[roles/06-docente\|Docente]] | Registra las notas de las materias en las que tiene asignación activa. |
| [[roles/07-director-de-grupo\|Director de Grupo]] | Si el colegio activa el permiso, puede editar notas de otras materias del grupo que dirige. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Supervisa el registro, identifica pendientes, autoriza ventanas de corrección. |
| [[roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Acceso completo de consulta y configuración. |

## Quién puede registrar

Solo los docentes que tienen una asignación formal a una materia y grupo pueden registrar notas en esa combinación específica. **No es posible que un docente registre notas en materias o grupos a los que no ha sido asignado.**

Si el director de grupo tiene habilitado el permiso de editar notas de otras materias de su grupo, puede hacerlo, pero ese permiso es **opcional** y lo activa el colegio en su configuración (ver [[roles/07-director-de-grupo|Director de Grupo]]).

## Escalas de calificación soportadas

- **Numérica:** rango configurable (ej. 1.0–5.0, 0–10, 1–10) con la cantidad de decimales que el colegio decida.
- **Por imágenes (caritas):** usado en preescolar. Cada nivel tiene una imagen y un valor numérico interno para cálculos.

La escala puede variar por nivel educativo dentro del mismo colegio. Detalle de configuración en [[../03-multi-tenancy/configuracion-por-colegio|Configuración por colegio]].

## Tipos de evaluación

| Tipo | Descripción |
| --- | --- |
| Componente evaluativo del periodo | Cada parte que compone la nota del periodo (quiz, taller, examen parcial). Aplica si el método es porcentajes ponderados o sumatoria. |
| Nota final del periodo | Calculada automáticamente al cierre del periodo. |
| Nivelación | Recuperación de una materia perdida al cierre de un periodo. Ver [[nivelaciones-y-habilitaciones]]. |
| Habilitación | Recuperación de una materia perdida al cierre del año lectivo. Ver [[nivelaciones-y-habilitaciones]]. |
| Nota final del año | Calculada al cierre del año promediando los periodos según la configuración. |

## Cómo se registran

Las notas se registran por estudiante, materia, periodo y componente evaluativo.

- Si el método de aprobación del colegio es **promedio simple**, el docente registra varias notas y el sistema promedia.
- Si es **porcentajes ponderados**, cada componente tiene su propio peso y el docente registra la nota de cada componente por separado. El sistema calcula la nota final aplicando los pesos.
- Si es **sumatoria dividida**, el docente registra notas y el sistema divide la sumatoria entre la cantidad registrada.

Al cierre del año, el sistema calcula la nota definitiva de cada materia según la configuración de cómo se promedian los periodos entre sí.

## Reglas de cálculo de promedios

- **Por periodo:** según el método configurado (promedio simple / ponderado / sumatoria dividida).
- **Anual por materia:** según la configuración del colegio (promedio simple de los periodos, ponderado entre periodos, etc.).
- **Por área:** opcional, agrupando las materias del área según la configuración.
- **General del estudiante:** opcional, promediando todas las materias.

Los decimales y el redondeo se aplican según la configuración de la escala valorativa del colegio.

## Reglas de aprobación / reprobación

- Cada materia se aprueba si la nota final es **≥ nota mínima de aprobación** configurada por el colegio.
- Una materia perdida en un periodo dispara [[nivelaciones-y-habilitaciones|nivelación]] al cierre del periodo.
- Una materia perdida en el año dispara [[nivelaciones-y-habilitaciones|habilitación]] al cierre del año.
- La promoción del estudiante al grado siguiente depende de las reglas configuradas (cuántas materias puede perder, materias que no pueden perderse, promedio mínimo). Ver [[promocion-y-reprobacion|Promoción y reprobación]].

## Estados y transiciones

### Nota de un componente evaluativo

```
No registrada → Registrada → Editada (auditada) → Bloqueada (cierre de periodo)
```

### Nota final del periodo

```
No calculada → Calculada → Bloqueada (cierre de periodo)
```

## Edición y corrección de notas

- Mientras el periodo esté `Abierto`, el docente puede editar libremente las notas de los componentes evaluativos.
- Al cierre del periodo, las notas quedan bloqueadas.
- El [[roles/02-coordinador-academico|Coordinador Académico]] puede abrir una **ventana de corrección** puntual con motivo registrado, que permite al docente corregir notas en un rango de tiempo controlado.
- Toda edición queda en el log de auditoría con valor anterior, nuevo, usuario, fecha, hora.

## Trazabilidad

Toda edición de una nota queda registrada en el log de auditoría con:

- Valor anterior y valor nuevo.
- Usuario que realizó el cambio.
- Fecha y hora.
- IP desde la que se realizó.
- Motivo si se hizo durante una ventana de corrección autorizada.

Esta trazabilidad es **inviolable y no puede desactivarse**.

## Datos involucrados

- Estudiante.
- Materia.
- Grupo.
- Periodo académico.
- Componente evaluativo (si aplica).
- Valor de la nota.
- Docente que registra.
- Fecha y hora del registro.
- Observaciones del docente sobre el estudiante en esa materia y periodo.

## Reglas de negocio

- **RN-CA-001 — Registro solo con asignación activa:** un docente solo puede registrar notas en combinaciones materia × grupo donde tiene asignación activa.
- **RN-CA-002 — Director de grupo con permiso opcional:** la edición de notas de otras materias del grupo por parte del director es un permiso configurable, desactivado por defecto.
- **RN-CA-003 — Nota dentro del rango de la escala:** el sistema rechaza notas fuera del rango definido por la escala valorativa del nivel educativo.
- **RN-CA-004 — Recalculo automático:** al registrar o editar un componente, el sistema recalcula la nota final del periodo aplicando el método configurado.
- **RN-CA-005 — Bloqueo al cierre del periodo:** las notas de un periodo cerrado no se pueden editar, salvo en una ventana de corrección autorizada por el coordinador.
- **RN-CA-006 — Inmutabilidad post-cierre del año:** las notas de un año lectivo cerrado son completamente inmutables.
- **RN-CA-007 — Auditoría obligatoria:** toda escritura sobre notas queda en el log con valor anterior y nuevo. No se puede desactivar.

## Notas y pendientes

- Definir el máximo de duración de una ventana de corrección y si requiere aprobación del rector.
- Definir si las notas se pueden importar masivamente desde un archivo (recomendado para colegios grandes).
