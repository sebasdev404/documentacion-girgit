---
tags:
  - arquitectura
  - rol/docente
aliases:
  - Ficha ROL-07
  - Docente Ficha
---

# Ficha de Rol — Docente

| Campo | Valor |
|---|---|
| ID Rol | ROL-07 |
| Nombre | Docente |
| Tipo | Principal — Tenant (con complemento opcional [[../07 - Director de Grupo/01 - Ficha de Rol\|Director de Grupo]]) |
| Reporta a | Coordinador Academico (ROL-03) o combinado (ROL-05) |
| Supervisa a | Estudiantes asignados a sus grupos y materias |

## Descripcion

Actor mas numeroso y con el acceso mas acotado. Solo puede ver y actuar sobre los grupos y materias que le han sido asignados explicitamente por el Coordinador Academico. Su comportamiento varia segun el modelo pedagogico del colegio: docente unico por salon (primaria) vs docente que rota entre grupos (bachillerato).

## Objetivo en el sistema

Operar el aula: registrar notas, asistencia y observaciones academicas de sus estudiantes en las materias asignadas.

## Acciones principales

- Registrar y editar notas de sus estudiantes en sus materias asignadas, dentro del periodo abierto.
- Registrar asistencia en sus clases.
- Agregar observaciones academicas por estudiante en su materia.
- Consultar el horario propio.
- Ver el listado de estudiantes de sus grupos asignados.

## Permisos clave

Editar notas y asistencia SOLO en materias y grupos asignados. Sin acceso a otros grupos. Sin acceso a configuracion ni documentos oficiales. Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Limitado a sus asignaciones. RR-10 garantiza este aislamiento.

## Dispositivo

Mobile + desktop. Registrar asistencia y notas en mobile es comun.

## Frecuencia de uso

Diaria. Es el rol con mayor uso operativo.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/06-docente.md`
