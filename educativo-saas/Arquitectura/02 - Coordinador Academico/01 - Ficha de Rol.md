---
tags:
  - arquitectura
  - rol/coord-academico
aliases:
  - Ficha ROL-03
  - Coord. Academico Ficha
---

# Ficha de Rol — Coordinador Academico

| Campo | Valor |
|---|---|
| ID Rol | ROL-03 |
| Nombre | Coordinador Academico |
| Tipo | Principal — Tenant |
| Reporta a | Rector (ROL-02) |
| Supervisa a | Docentes (ROL-07) en lo academico |

## Descripcion

Gestiona la estructura academica operativa del colegio: plan de estudios, grupos, asignacion docente, horarios y procesos de cierre de periodo. No puede modificar la configuracion base del sistema (eso es del Rector).

## Objetivo en el sistema

Asegurar que la operacion academica este organizada: cada grado con su plan, cada grupo con sus docentes asignados, cada periodo con su cierre limpio.

## Acciones principales

- Crear y gestionar plan de estudios (materias por grado, intensidad horaria, areas).
- Crear y gestionar grupos por grado y ano lectivo.
- Asignar docentes a materias y grupos.
- Designar directores de grupo.
- Construir y administrar horarios de clase.
- Ver consolidados de notas de todos los grupos.
- Gestionar nivelaciones y habilitaciones.
- Coordinar cierre de periodos academicos.

## Permisos clave

CRUD sobre plan de estudios, grupos, horarios. Lectura completa sobre consolidados. Edicion de notas: configurable. Sin acceso al observador disciplinario (salvo configuracion especial). Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Alto en operacion academica. Sin acceso a configuracion base ni a documentos oficiales.

## Dispositivo

Desktop principalmente.

## Frecuencia de uso

Alta al inicio del ano y en cada cierre de periodo. Media en operacion estable.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/02-coordinador-academico.md`
