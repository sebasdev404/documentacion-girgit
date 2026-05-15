---
tags:
  - arquitectura
  - portada
aliases:
  - Portada Plataforma
  - Indice Arquitectura
---

# Portada — SaaS de Gestion Academica

| Documento | Portada |
|---|---|
| Version | 0.1 |
| Estado | Borrador |
| Relacionado a | [[02 - PRD - Plataforma\|PRD-01]] |
| Fuente de verdad | `Logica del negocio/02-usuarios-roles-y-permisos/` |

---

## Roles definidos en este documento

Los roles siguen el orden jerarquico de `Logica del negocio/02-usuarios-roles-y-permisos/roles/`.

| ID | Rol | Descripcion breve | Ambito |
|---|---|---|---|
| ROL-01 | Superadministrador de la Plataforma | Equipo interno del SaaS. Crea tenants, asigna planes, cambia calendario A↔B | Global |
| ROL-02 | Rector / Administrador del Colegio | Maxima autoridad dentro del tenant. Configura calendario, jornadas, escala valorativa | Tenant |
| ROL-03 | Coordinador Academico | Plan de estudios, grupos, horarios, asignacion docente, cierre de periodo | Tenant |
| ROL-04 | Coordinador de Convivencia | Observador del estudiante, anotaciones, reportes de convivencia | Tenant |
| ROL-05 | Coordinador Academico y Convivencia | Combinado para colegios pequenos. Mutuamente excluyente con ROL-03/ROL-04 | Tenant |
| ROL-06 | Secretaria Academica | Matricula, documentos oficiales, reporte SIMAT, gestion de acudientes | Tenant |
| ROL-07 | Docente | Notas, asistencia y observaciones de sus materias asignadas | Tenant |
| ROL-08 | Director de Grupo (complemento) | Permisos extra sobre el grupo dirigido. No es rol principal | Tenant |
| ROL-09 | Estudiante / Acudiente | Solo consulta. Acudiente ve datos del estudiante asociado | Tenant |
| ROL-10 | Sistema | Automatizaciones del sistema (no es persona) | Plataforma |
| ROL-11 | Administrador Tecnico | Gestion tecnica del tenant (en pausa) | Plataforma |

---

## Jerarquias

| Nivel | Roles |
|---|---|
| Plataforma | ROL-01, ROL-10, ROL-11 |
| Direccion del colegio | ROL-02 |
| Coordinacion academica | ROL-03 o ROL-05 |
| Coordinacion de convivencia | ROL-04 o ROL-05 |
| Administrativo | ROL-06 |
| Operativo (aulas) | ROL-07 (+ complemento ROL-08) |
| Consulta | ROL-09 |

---

## Notas clave

> **Multi-tenant:** cada colegio es un schema separado en PostgreSQL. Aislamiento total a nivel BD y autenticacion.
>
> **Configurabilidad:** cada rol distingue permisos **estructurales** (no modificables) y **permisos configurables** por el colegio.
>
> **Coordinador combinado vs separados:** son mutuamente excluyentes. Un colegio elige el esquema, no ambos.
>
> **Director de Grupo** es complemento, no rol principal. Se asigna sobre ROL-07.

---

## Documentos relacionados

- [[02 - PRD - Plataforma|PRD del proyecto]]
- [[03 - Tabla de Requerimientos|Tabla de Requerimientos]]
- [[06 - Matriz de Permisos|Matriz de Permisos]]
- [[07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/02-usuarios-roles-y-permisos/`
