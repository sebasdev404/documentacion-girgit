---
tags:
  - arquitectura
  - rol/coord-convivencia
  - permisos
aliases:
  - Permisos ROL-04
---

# Permisos Detallados — Coordinador de Convivencia

Detalle granular. Vista cruzada en [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Observador** | Leer observador de cualquier estudiante | Ver | Del tenant |
| **Observador** | Registrar llamados de atencion y compromisos | Editar | En el observador |
| **Observador** | Cerrar / archivar anotaciones | Editar | Marcar resoluciones |
| **Convivencia** | Generar reportes | Reportar | Por estudiante o por grupo |
| **Convivencia** | Configurar tipologias de anotacion | Editar | Catalogo del colegio (leve/grave/gravisima) |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
|---|---|---|
| Acceso al modulo academico (notas) | desactivado | Activable si el colegio unifica coordinaciones |
| Citaciones formales a acudientes | configurable | Puede ser exclusivo del Rector |
| Definir sanciones formales | configurable | Algunos colegios lo separan en un comite de convivencia |
| Comunicarse con acudientes via portal | configurable | |
| Enviar comunicados al colegio entero | configurable | |
| Ver historial de cambios de un registro | configurable | Auditoria parcial |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Registrar o editar notas academicas | No es su ambito |
| Gestionar plan de estudios u horarios | Es del Coord. Academico |
| Emitir documentos oficiales | Es de la Secretaria |
| Acceder a datos de otros tenants | RR-01 |

## Reglas asociadas

- RR-12 Coord. combinado excluye los separados.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia.md`
