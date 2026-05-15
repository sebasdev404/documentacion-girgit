---
tags:
  - arquitectura
  - rol/estudiante-acudiente
aliases:
  - Ficha ROL-09
  - Estudiante Acudiente Ficha
---

# Ficha de Rol — Estudiante / Acudiente

| Campo | Valor |
|---|---|
| ID Rol | ROL-09 |
| Nombre | Estudiante / Acudiente |
| Tipo | Principal — Tenant (solo consulta) |
| Reporta a | — |
| Supervisa a | — |

## Descripcion

Rol de solo consulta. Dos tipos de usuario lo comparten:
- **Estudiante**: ve sus propios datos.
- **Acudiente / Padre**: ve los datos del / los estudiantes vinculados a el.

Ambos tienen exactamente los mismos permisos; el scope los diferencia (RR-11, RR-14). Ningun usuario con este rol modifica datos del sistema.

## Objetivo en el sistema

Permitir consulta autonoma de notas, horario, boletines y comunicaciones por parte de estudiantes y acudientes, reduciendo carga administrativa del colegio.

## Acciones principales

- Consultar notas por materia y por periodo.
- Consultar horario.
- Recibir y leer comunicados y notificaciones.
- Consultar boletines emitidos.
- Consultar observaciones academicas registradas.
- Consultar anotaciones del observador (si el colegio lo habilita).

## Permisos clave

Solo lectura sobre datos propios / del estudiante asociado. Acceso al portal: configurable (puede estar desactivado por colegio). Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Minimo. No modifica nada. Ve solo lo propio o lo de su(s) hijo(s).

## Dispositivo

Mobile principalmente. Desktop para descargas de boletines.

## Frecuencia de uso

Variable. Picos en publicacion de notas y boletines.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente.md`
