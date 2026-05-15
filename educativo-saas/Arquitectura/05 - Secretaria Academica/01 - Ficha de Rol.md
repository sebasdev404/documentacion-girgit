---
tags:
  - arquitectura
  - rol/secretaria
aliases:
  - Ficha ROL-06
  - Secretaria Ficha
---

# Ficha de Rol — Secretaria Academica

| Campo | Valor |
|---|---|
| ID Rol | ROL-06 |
| Nombre | Secretaria Academica |
| Tipo | Principal — Tenant |
| Reporta a | Rector (ROL-02) |
| Supervisa a | — |

## Descripcion

Gestiona los procesos administrativos del colegio: matricula, registro de estudiantes y acudientes, emision de documentos oficiales, control de documentos pendientes y reporte SIMAT. No tiene acceso a registrar ni editar notas.

## Objetivo en el sistema

Garantizar que la matricula sea trazable, los documentos oficiales se emitan con consecutivo y firma, y el reporte oficial al SIMAT se entregue en plazo y forma.

## Acciones principales

- Registrar y actualizar estudiantes y acudientes.
- Gestionar matricula: inscripcion, recepcion de documentos, asignacion de grupo.
- Control de documentos de matricula pendientes (con bloqueos configurables).
- Generar constancias de estudio, certificados de notas y paz y salvos.
- Mantener consecutivos y trazabilidad de documentos emitidos.
- Preparar reportes para el SIMAT.

## Permisos clave

CRUD sobre estudiantes y acudientes. Reportar (generar) documentos oficiales. Lectura de notas para emitir certificados (no edicion). Bloqueo de emision por pendientes: configurable. Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Alto en operacion administrativa. Sin acceso a notas como datos editables, sin acceso al observador disciplinario.

## Dispositivo

Desktop principalmente (impresion de documentos, formularios extensos).

## Frecuencia de uso

Diaria. Picos en epoca de matricula (inicio del ano) y al final del ano (certificados, paz y salvos).

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/05-secretaria-academica.md`
