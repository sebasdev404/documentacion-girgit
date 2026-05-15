---
tags:
  - arquitectura
  - rol/coord-combinado
aliases:
  - Ficha ROL-05
  - Coord. Combinado Ficha
---

# Ficha de Rol — Coordinador Academico y Convivencia

| Campo | Valor |
|---|---|
| ID Rol | ROL-05 |
| Nombre | Coordinador Academico y de Convivencia (combinado) |
| Tipo | Principal — Tenant |
| Reporta a | Rector (ROL-02) |
| Supervisa a | Docentes (ROL-07) y directores de grupo (ROL-08) |

## Descripcion

Rol combinado que une las responsabilidades del [[../02 - Coordinador Academico/01 - Ficha de Rol|Coord. Academico]] y del [[../03 - Coordinador de Convivencia/01 - Ficha de Rol|Coord. de Convivencia]]. Pensado para colegios pequenos o medianos donde no existe la division organizacional entre ambas coordinaciones. Es **mutuamente excluyente** con el esquema separado (no se asignan ambos esquemas a la vez — ver RR-12).

## Objetivo en el sistema

Cubrir tanto la gestion academica operativa como el seguimiento de convivencia desde un solo rol, en colegios que no tienen el equipo para separar las dos coordinaciones.

## Acciones principales

Heredadas del Coord. Academico:
- Plan de estudios, grupos, asignacion docente, horarios.
- Consolidados, nivelaciones, cierre de periodo.

Heredadas del Coord. de Convivencia:
- Observador del estudiante, tipologias, anotaciones.
- Reportes de convivencia.

## Permisos clave

Union de los permisos del Coord. Academico y del Coord. de Convivencia. Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Alto, equivalente a la suma de ROL-03 + ROL-04. Sin acceso a configuracion base ni documentos oficiales.

## Dispositivo

Desktop principalmente.

## Frecuencia de uso

Alta. Cubre dos ambitos a la vez.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/04-coordinador-academico-y-convivencia.md`
