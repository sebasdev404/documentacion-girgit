---
tags:
  - arquitectura
  - rol/coord-convivencia
aliases:
  - Ficha ROL-04
  - Coord. Convivencia Ficha
---

# Ficha de Rol — Coordinador de Convivencia

| Campo | Valor |
|---|---|
| ID Rol | ROL-04 |
| Nombre | Coordinador de Convivencia (o Disciplinario) |
| Tipo | Principal — Tenant |
| Reporta a | Rector (ROL-02) |
| Supervisa a | Directores de grupo (ROL-08) en lo disciplinario |

## Descripcion

Su ambito es el seguimiento del comportamiento y la convivencia escolar. Gestiona el observador del estudiante, registra anotaciones, compromisos y seguimientos, y coordina con los directores de grupo las situaciones que escalan. No tiene acceso a la gestion de notas ni al modulo academico operativo.

## Objetivo en el sistema

Mantener un registro completo y oportuno de la convivencia escolar. Detectar y dar seguimiento a casos disciplinarios.

## Acciones principales

- Leer el observador de cualquier estudiante.
- Registrar llamados de atencion, compromisos y seguimientos.
- Cerrar / archivar anotaciones.
- Generar reportes de convivencia por estudiante o por grupo.
- Configurar tipologias de anotacion (leve/grave/gravisima, etc.).
- Coordinar con directores de grupo las situaciones que escalan.

## Permisos clave

CRUD sobre observador y tipologias. Sin acceso al modulo academico (notas, consolidados) salvo configuracion. Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Alto en convivencia. Sin acceso a notas ni configuracion base.

## Dispositivo

Desktop principalmente. Mobile para anotaciones rapidas.

## Frecuencia de uso

Diaria. Picos en epocas de evaluacion / cierres.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia.md`
