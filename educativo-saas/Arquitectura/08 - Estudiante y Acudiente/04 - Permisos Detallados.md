---
tags:
  - arquitectura
  - rol/estudiante-acudiente
  - permisos
aliases:
  - Permisos ROL-09
---

# Permisos Detallados — Estudiante / Acudiente

Rol de solo consulta. Mismos permisos para estudiante y acudiente, distinto scope.

Vista cruzada en [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Notas** | Consultar notas propias / del estudiante asociado | Ver | Por materia y por periodo |
| **Horario** | Consultar horario | Ver | Del grupo correspondiente |
| **Boletines** | Consultar boletines emitidos | Ver | |
| **Comunicaciones** | Recibir comunicados | Ver | Del colegio y de los docentes |
| **Observador academico** | Consultar observaciones academicas | Ver | Registradas por los docentes |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
|---|---|---|
| Acceso al portal | activado | El colegio puede desactivarlo completamente |
| Ver el observador disciplinario | configurable | Algunos colegios prefieren que el observador sea interno |
| Descargar boletines en PDF | configurable | |
| Recibir notificaciones por correo | configurable | |
| Comunicarse con docentes via portal | configurable | Por defecto restringido |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Modificar cualquier dato del sistema | Rol exclusivamente de consulta |
| Acceder a notas u observaciones de otros estudiantes | RR-14 |
| Acceder a configuracion del colegio | No es su ambito |
| Acceder a datos de otros tenants | RR-01 |

## Reglas asociadas

- RR-11 Estudiante y Acudiente comparten rol.
- RR-14 Acudiente accede solo a datos de estudiantes vinculados.

## Scope por tipo de usuario

| Tipo de usuario | Scope |
|---|---|
| Estudiante | Sus propios datos unicamente |
| Acudiente | Datos del/los estudiantes vinculados a el (uno o varios hijos) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente.md`
