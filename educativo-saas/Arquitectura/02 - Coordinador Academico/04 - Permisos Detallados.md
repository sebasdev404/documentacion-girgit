---
tags:
  - arquitectura
  - rol/coord-academico
  - permisos
aliases:
  - Permisos ROL-03
---

# Permisos Detallados — Coordinador Academico

Detalle granular. Vista cruzada en [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Plan de estudios** | Gestionar materias por grado | CRUD | Intensidad horaria, areas |
| **Grupos** | Crear / gestionar grupos | CRUD | Por grado y ano lectivo |
| **Asignacion** | Asignar docentes a materias y grupos | Editar | Por periodo |
| **Asignacion** | Designar directores de grupo | Editar | Sobre docentes |
| **Horarios** | Construir / editar horarios | CRUD | Docente / materia / aula / bloque |
| **Consolidados** | Ver consolidados de notas del tenant | Ver | Todos los grupos |
| **Periodo** | Coordinar cierre de periodo | Editar | Activar/desactivar cierre, validar consolidados |
| **Nivelaciones** | Gestionar nivelaciones y habilitaciones | Editar | Para estudiantes que pierden materias |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
|---|---|---|
| Editar notas directamente | configurable | Algunos colegios lo permiten, otros lo restringen al docente |
| Aprobar / firmar boletines | configurable | Puede delegarse al Rector o quedar aca |
| Crear anos lectivos nuevos | configurable | Puede ser exclusivo del Rector |
| Asignar estudiante a grupo en matricula | configurable | Tipicamente lo hace la Secretaria |
| Cambiar grupo de un estudiante post-matricula | configurable | Tipicamente al Coord. Academico |
| Citar formalmente a acudientes | configurable | Tipicamente al Coord. de Convivencia |
| Comunicarse con acudientes via portal | configurable | |
| Ver historial de cambios de un registro | configurable | Auditoria parcial |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Modificar configuracion base del sistema | Es del Rector |
| Acceder al observador disciplinario | Es del Coord. de Convivencia (salvo combinado activo) |
| Emitir documentos oficiales | Es de la Secretaria |
| Acceder a datos de otros tenants | RR-01 |

## Reglas asociadas

- RR-12 Coordinador combinado excluye los separados.
- RR-07 Notas dentro del periodo abierto.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/02-coordinador-academico.md`
