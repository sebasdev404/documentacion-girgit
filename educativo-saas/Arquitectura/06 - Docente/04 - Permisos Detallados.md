---
tags:
  - arquitectura
  - rol/docente
  - permisos
aliases:
  - Permisos ROL-07
---

# Permisos Detallados — Docente

Detalle granular. Vista cruzada en [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Notas** | Registrar y editar notas | Editar | Solo en sus materias y grupos asignados, dentro del periodo abierto |
| **Asistencia** | Registrar asistencia | Editar | En sus clases |
| **Observador academico** | Agregar observaciones academicas | Editar | Por estudiante, en su materia |
| **Horario** | Consultar su horario | Ver | |
| **Estudiantes** | Ver listado de estudiantes | Ver | De sus grupos asignados |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
|---|---|---|
| Editar notas despues del cierre de periodo | desactivado | Algunos colegios lo permiten con ventana o justificacion |
| Cargar archivos / evidencias de evaluaciones | configurable | Depende del modulo de evidencias |
| Comunicarse con acudientes via portal | configurable | Algunos colegios obligan a usar canales formales |
| Ver el plan de estudios completo | configurable | Por defecto solo ve sus materias |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Acceder a notas o materias que no dicta | RR-10. Salvo complemento ROL-08 + configuracion |
| Modificar configuracion del colegio | Es del Rector |
| Emitir documentos oficiales | Es de la Secretaria |
| Acceder al observador disciplinario | Es del Coord. de Convivencia / Director de Grupo |
| Acceder a datos de otros tenants | RR-01 |

## Reglas asociadas

- RR-07 Notas se editan dentro del periodo abierto.
- RR-10 Docente ve solo grupos y materias asignados.

## Variantes segun modelo pedagogico

El sistema presenta horario y grupos de forma distinta segun el modelo:
- **Docente unico por salon** (primaria): un solo grupo principal con muchas materias.
- **Docente con rotacion** (bachillerato): multiples grupos a lo largo del dia.

Los permisos no cambian. Solo cambia el UI.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/06-docente.md`
