---
tags:
  - arquitectura
  - rol/personal-de-apoyo
aliases:
  - Ficha ROL-12
  - Personal de Apoyo Ficha
---

# Ficha de Rol — Personal de Apoyo

| Campo | Valor |
|---|---|
| ID Rol | ROL-12 |
| Nombre | Personal de Apoyo |
| Tipo | Principal — Servicio no docente (bajo privilegio) |
| Reporta a | Rector (ROL-02) o la coordinacion que el colegio designe (`RN-TU-008`) |
| Supervisa a | — (no supervisa a otros roles) |

## Descripcion

Rol transversal de **bajo privilegio** para funcionarios que acompanan al estudiante desde un servicio especifico, sin dictar clase ni administrar el colegio. Se especializa por **perfil**: orientador/psicologo (Bienestar), enfermeria (Salud) o bibliotecario (Biblioteca). Todos los perfiles comparten un nucleo comun: consultar la **ficha acotada** del estudiante y **aportar anotaciones al observador** con la visibilidad de `RN-OB-081`. No accede a notas ni a la configuracion del colegio.

## Objetivo en el sistema

Prestar el servicio de su perfil (atencion de salud, acompanamiento de bienestar o gestion de biblioteca) con trazabilidad, y dejar constancia en el observador del estudiante cuando un hecho deba quedar en su seguimiento, sin intervenir en lo academico ni en lo administrativo.

## Acciones principales

- Consultar la ficha acotada del estudiante (identificacion, grupo, contacto del acudiente, alertas basicas).
- Aportar anotaciones al observador con seleccion de visibilidad (`RN-OB-081`), por defecto interna.
- Operar **su** modulo de servicio segun el perfil asignado (Bienestar / Salud / Biblioteca).
- Gestionar su agenda/bandeja (citas, atenciones o prestamos a cargo).
- Generar remisiones internas cuando el caso excede su servicio.

## Permisos clave

Permisos minimos y acotados. Acceso de **consulta** a la ficha del estudiante y de **operacion** unicamente sobre su modulo de servicio. Sin acceso academico, financiero ni de configuracion. Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]] (columna `D-04`).

## Nivel de acceso

Bajo. Es el rol interno con el conjunto de permisos mas acotado (`RN-TU-001`). Solo ve datos de su propio tenant.

## Dispositivo

Desktop y tablet (mostrador de biblioteca, enfermeria o consultorio de orientacion).

## Frecuencia de uso

Diaria durante la jornada escolar, concentrada en su modulo de servicio.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo.md`
