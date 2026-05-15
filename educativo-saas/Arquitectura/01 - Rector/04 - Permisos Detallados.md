---
tags:
  - arquitectura
  - rol/rector
  - permisos
aliases:
  - Permisos ROL-02
---

# Permisos Detallados — Rector / Administrador del Colegio

Detalle granular de permisos. Para la vista cruzada ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Identidad** | Configurar logo, NIT, MEN, contactos | Editar | Datos institucionales |
| **Calendario** | Definir periodos lectivos | Editar | Dentro del calendario habilitado |
| **Jornadas** | Configurar jornadas y bloques horarios | Editar | Manana / tarde / noche |
| **Modelo pedagogico** | Configurar por nivel | Editar | Docente unico vs rotacion |
| **Escala valorativa** | Configurar escala | Editar | Numerica o por imagenes |
| **Aprobacion** | Configurar metodo y nota minima | Editar | Promedio / ponderado / sumatoria |
| **Usuarios** | Crear/editar/desactivar usuarios | CRUD | Todos los roles del tenant |
| **Roles** | Asignar roles | Editar | A los usuarios |
| **Roles** | Ajustar permisos configurables | Editar | De los roles del tenant |
| **Reportes** | Acceso total a reportes | Ver | Academicos, financieros, KPIs |
| **Auditoria** | Acceder a logs del tenant | Ver | Inmutables |
| **Operacion** | Hacer todo lo que hacen los demas roles internos | CRUD | Como respaldo / supervision |

## Permisos configurables por el colegio

El Rector tiene poder total, pero el colegio puede decidir delegar algunas funciones a otros roles. Esa delegacion se hace ampliando permisos al otro rol, no quitandoselos al Rector.

| Permiso delegable | A quien tipicamente |
|---|---|
| Edicion directa de notas | Coordinador Academico |
| Cierre de periodo academico | Coordinador Academico |
| Aprobacion de boletines | Coordinador Academico o Director de Grupo |
| Generacion de constancias | Secretaria Academica |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Crear o eliminar tenants | Solo el Superadmin (ROL-01) |
| Cambiar calendario A/B habilitado | Solo el Superadmin (RR-13) |
| Acceder a datos de otros colegios | RR-01 Aislamiento total |

## Reglas asociadas

- RR-04 Asignacion de roles por el Rector.
- RR-05 Configurabilidad acotada de permisos.
- RR-13 Cambio de calendario A/B es del Superadmin (el Rector solo elige dentro del habilitado).

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`
