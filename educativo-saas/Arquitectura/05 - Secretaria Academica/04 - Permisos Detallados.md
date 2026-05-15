---
tags:
  - arquitectura
  - rol/secretaria
  - permisos
aliases:
  - Permisos ROL-06
---

# Permisos Detallados — Secretaria Academica

Detalle granular. Vista cruzada en [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Estudiantes** | Crear y editar estudiantes | CRUD | Datos personales, contacto, ficha de matricula |
| **Acudientes** | Crear y editar acudientes | CRUD | Vincularlos a estudiantes |
| **Matricula** | Asignar estudiante a grupo | Editar | Como parte del proceso de matricula |
| **Documentos** | Cargar documentos de matricula | Editar | Y marcarlos como recibidos / pendientes |
| **Documentos oficiales** | Generar constancias | Reportar | Con consecutivo y trazabilidad |
| **Documentos oficiales** | Generar certificados de notas | Reportar | Con consecutivo |
| **Documentos oficiales** | Emitir paz y salvos | Reportar | Cuando aplica |
| **SIMAT** | Generar reporte SIMAT | Reportar | Formato oficial del MEN |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
|---|---|---|
| Bloquear emision por documentos pendientes | activado | Algunos colegios prefieren emitirlos igual con advertencia |
| Bloquear emision por pagos pendientes | configurable | Depende de si el colegio integra cartera con secretaria |
| Editar grupo del estudiante despues de matriculado | configurable | Algunos lo restringen al Coord. Academico |
| Generar paz y salvos sin pasar por contabilidad | configurable | |
| Ver notas como datos consultables | configurable | Por defecto solo lee para certificados |
| Comunicarse con acudientes via portal | configurable | |
| Enviar comunicados al colegio entero | configurable | |
| Ver historial de cambios de un registro | configurable | |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Registrar o editar notas academicas | No es su ambito |
| Registrar asistencia u observaciones disciplinarias | No es su ambito |
| Modificar configuracion base del sistema | Es del Rector |
| Acceder a datos de otros tenants | RR-01 |

## Reglas asociadas

- RR-08 Bloqueo de documentos por pendientes (configurable).
- RR-15 Reporte SIMAT obligatorio.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/05-secretaria-academica.md`
