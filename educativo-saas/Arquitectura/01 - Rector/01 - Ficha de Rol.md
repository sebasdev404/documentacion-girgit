---
tags:
  - arquitectura
  - rol/rector
aliases:
  - Ficha ROL-02
  - Rector Ficha
---

# Ficha de Rol — Rector / Administrador del Colegio

| Campo | Valor |
|---|---|
| ID Rol | ROL-02 |
| Nombre | Rector / Administrador del Colegio |
| Tipo | Principal — Tenant |
| Reporta a | Superadmin (ROL-01) en lo contractual |
| Supervisa a | Todos los roles internos del colegio (ROL-03 a ROL-09) |

## Descripcion

Actor con mayor nivel de acceso dentro del tenant. Tipicamente es el Rector del colegio, aunque puede ser otra figura directiva. Puede hacer todo lo que hacen los demas roles internos. Responsable directo de la configuracion del colegio, creacion de usuarios y ajuste de permisos configurables.

## Objetivo en el sistema

Configurar el colegio inicialmente y administrarlo en el dia a dia. Garantizar que la plataforma refleje la realidad organizacional, academica y normativa del colegio.

## Acciones principales

- Configurar identidad institucional (nombre, logo, NIT, MEN).
- Definir calendario lectivo y periodos.
- Configurar jornadas, bloques horarios y modelo pedagogico.
- Configurar escala valorativa y metodo de aprobacion.
- Crear, editar y desactivar usuarios; asignar roles.
- Ajustar permisos configurables de cada rol.
- Acceder a reportes, consolidados, boletines y logs de auditoria del tenant.

## Permisos clave

Acceso total dentro del tenant. CRUD sobre configuracion, usuarios, roles. Lectura completa sobre operacion. Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Maximo dentro del tenant. No tiene visibilidad cross-tenant.

## Dispositivo

Desktop principalmente. Mobile para consulta y aprobaciones puntuales.

## Frecuencia de uso

Alta al inicio del ano lectivo y en cambios de configuracion. Media-baja en operacion estable.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`
