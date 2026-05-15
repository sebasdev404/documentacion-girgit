---
tags:
  - arquitectura
  - rol/coord-combinado
  - permisos
aliases:
  - Permisos ROL-05
---

# Permisos Detallados — Coordinador Academico y Convivencia

Combinacion de los permisos de ROL-03 + ROL-04. Detalles cruzados en [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

Hereda todos los permisos estructurales de:
- [[../02 - Coordinador Academico/04 - Permisos Detallados|ROL-03 Coord. Academico]]: plan de estudios, grupos, asignacion docente, horarios, consolidados, cierre de periodo, nivelaciones.
- [[../03 - Coordinador de Convivencia/04 - Permisos Detallados|ROL-04 Coord. de Convivencia]]: observador, anotaciones, tipologias, reportes de convivencia.

## Permisos configurables por el colegio

Hereda los configurables de ambos roles base. Las mismas reglas aplican.

| Permiso | Origen | Default | Notas |
|---|---|---|---|
| Editar notas directamente | ROL-03 | configurable | |
| Aprobar / firmar boletines | ROL-03 | configurable | |
| Citaciones formales a acudientes | ROL-04 | configurable | |
| Definir sanciones formales | ROL-04 | configurable | |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Modificar configuracion base del sistema | Es del Rector |
| Emitir documentos oficiales | Es de la Secretaria |
| Acceder a datos de otros tenants | RR-01 |

## Reglas asociadas

- RR-12 Mutuamente excluyente con ROL-03 + ROL-04 separados. Si el tenant activa ROL-05, no debe asignar ROL-03 ni ROL-04 simultaneamente.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/04-coordinador-academico-y-convivencia.md`
