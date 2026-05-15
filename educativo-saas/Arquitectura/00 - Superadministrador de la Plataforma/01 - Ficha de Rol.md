---
tags:
  - arquitectura
  - rol/superadmin
aliases:
  - Ficha ROL-01
  - Superadmin Ficha
---

# Ficha de Rol — Superadministrador de la Plataforma

| Campo | Valor |
|---|---|
| ID Rol | ROL-01 |
| Nombre | Superadministrador de la Plataforma |
| Tipo | Principal — Global |
| Reporta a | — (rol mas alto del sistema) |
| Supervisa a | Todos los tenants y sus Rectores (ROL-02) |

## Descripcion

Unico rol que vive sobre todos los colegios. Pertenece al equipo interno del SaaS (programadores / operaciones). Crea tenants, asigna planes, configura tecnicamente los colegios y proporciona soporte cross-tenant cuando se requiere. No interviene en la operacion academica diaria de ningun colegio.

## Objetivo en el sistema

Provisionar y mantener la infraestructura multi-tenant. Habilitar a cada colegio para que opere autonomamente desde el primer dia.

## Acciones principales

- Crear / eliminar tenants (colegios).
- Asignar planes de licencia (basico, estandar, premium).
- Cambiar calendario A/B de un tenant.
- Definir subdominio del colegio.
- Gestionar cuota de almacenamiento.
- Acceder cross-tenant para soporte (auditado).
- Ver logs globales de la plataforma.

## Permisos clave

CRUD completo sobre el modulo "Plataforma". Sin permisos de operacion academica. Ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Nivel de acceso

Maximo (global). Es el unico rol con visibilidad cross-tenant.

## Dispositivo

Desktop (panel administrativo de plataforma).

## Frecuencia de uso

Esporadica. Picos al crear tenants nuevos o atender incidentes.

## Fuente de verdad

`Logica del negocio/02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma.md`
