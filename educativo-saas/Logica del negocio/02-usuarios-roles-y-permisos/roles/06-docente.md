---
titulo: "Rol: Docente"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, docente, profesor, tenant]
---

# Rol: Docente

## Identificación

- **Nombre del rol:** Docente
- **Tipo de usuario asociado:** Profesor del colegio
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — varios permisos son configurables, especialmente los del complemento [[07-director-de-grupo|Director de Grupo]]
- **Tipo:** principal (puede combinarse con el complemento Director de Grupo)

## Descripción

Es el actor **más numeroso y con el acceso más acotado**. Sin embargo, su comportamiento varía significativamente según la configuración del colegio y sus asignaciones específicas. En términos generales, **un docente solo puede ver y actuar sobre los grupos y materias que le han sido asignados explícitamente** por el Coordinador Académico.

## Responsabilidades

- Registrar **notas** de los estudiantes en las materias y grupos que tiene asignados.
- Registrar **asistencia** en sus clases.
- Agregar **observaciones académicas** por estudiante en su materia.
- Consultar el horario propio.
- Ver el listado de estudiantes de sus grupos asignados.

## Scope / alcance de visibilidad

- Ve **únicamente** los grupos y materias que le han sido asignados.
- Ve los estudiantes inscritos en esos grupos.
- **No ve consolidados generales** del grupo (solo si tiene el complemento Director de Grupo).
- **No ve notas de materias que no dicta** (salvo que tenga el complemento de director y la configuración del colegio lo permita).
- No ve datos de otros tenants.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Registrar y editar notas | Solo en sus materias y grupos asignados, dentro del período abierto |
| Registrar asistencia | En sus clases |
| Agregar observaciones académicas | Por estudiante, en su materia |
| Consultar su horario | |
| Ver listado de estudiantes | De sus grupos asignados |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
| --- | --- | --- |
| Editar notas después del cierre de período | desactivado | Algunos colegios lo permiten con ventana o con justificación |
| Cargar archivos / evidencias de evaluaciones | configurable | Depende de si el colegio usa el módulo de evidencias |
| Comunicarse con acudientes vía portal | configurable | Algunos colegios lo restringen y obligan a usar canales formales |
| Ver el plan de estudios completo | configurable | Por defecto solo ve sus materias |

## Permisos explícitamente NO otorgados

- No accede a notas ni a la operación de materias que no dicta (salvo complemento Director de Grupo + configuración).
- No modifica la configuración del colegio.
- No emite documentos oficiales.
- No accede al observador disciplinario (esto es del Coordinador de Convivencia y, parcialmente, del Director de Grupo).
- No accede a datos de otros tenants.

## Reglas de asignación

- Lo asigna el Rector o el Coordinador Académico (según configuración).
- Las asignaciones de **grupos y materias** las hace el Coordinador Académico.
- Cantidad: la que el colegio necesite — es el rol más numeroso.

## Compatibilidad con otros roles

- Un docente puede tener el complemento [[07-director-de-grupo|Director de Grupo]] sobre uno o más grupos. Esto **no cambia su rol base**, le suma permisos sobre el grupo dirigido.
- En colegios pequeños, una persona podría ser Docente y Coordinador Académico simultáneamente, pero se recomienda separar para auditoría.

## Variantes según configuración del colegio

Existe la distinción entre dos modelos pedagógicos que el colegio define en su configuración base:

- **Docente único por salón** (típico en primaria): un solo docente dicta todas o casi todas las materias del grupo. Suele ser también el director de grupo.
- **Docente que rota entre grupos** (típico en bachillerato): múltiples docentes dictan las distintas materias de un grupo.

Esta distinción **no cambia los permisos del docente**, sino la forma en que el sistema le presenta su horario y sus grupos:
- En modo "único por salón", el docente ve un solo grupo principal con muchas materias.
- En modo "rotación", el docente ve un horario con múltiples grupos a lo largo del día.

## Notas y pendientes

- Definir ventana de tolerancia para edición de notas dentro del período abierto.
- Definir si el docente puede ver el promedio histórico del estudiante en su materia (tendencia).
- Casos de uso: registrar nota, registrar asistencia, agregar observación académica.
