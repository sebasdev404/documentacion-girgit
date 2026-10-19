---
tags:
  - arquitectura
  - rol/rector
  - permisos
aliases:
  - Permisos ROL-02
---

# Permisos Detallados — Rector / Administrador del Colegio

Detalle granular de permisos. Para la vista cruzada ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Identidad** | Configurar logo, NIT, MEN, contactos | Editar | Datos institucionales |
| **Matrículas por enlace** | Configurar política institucional, convocatorias y requisitos | `ingreso.configurar` | Requiere plan `academico`; rangos permanentes por grado y aviso versionado en Ajustes institucionales > Configuración de matrículas, con acceso directo desde Matrículas por enlace |
| **Calendario** | Definir periodos lectivos | Editar | Dentro del calendario habilitado |
| **Jornadas** | Configurar jornadas y bloques horarios | Editar | Manana / tarde / noche |
| **Modelo pedagogico** | Configurar por nivel | Editar | Docente unico vs rotacion |
| **Escala valorativa** | Configurar escala | Editar | Numerica o por imagenes |
| **Aprobacion** | Configurar metodo y nota minima | Editar | Promedio / ponderado / sumatoria |
| **Usuarios** | Crear/editar/desactivar usuarios | CRUD | Todos los roles del tenant |
| **Roles** | Asignar roles | Editar | A los usuarios |
| **Roles** | Ajustar permisos configurables | Editar | De los roles del tenant |
| **Reportes** | Acceso total a reportes | Ver | Academicos, financieros, KPIs |
| **Auditoria** | Acceder a logs del tenant | Ver | Inmutables |
| **Operacion** | Hacer todo lo que hacen los demas roles internos | CRUD | Como respaldo / supervision |

## Permisos configurables por el colegio

El Rector tiene poder total, pero el colegio puede decidir delegar algunas funciones a otros roles. Esa delegacion se hace ampliando permisos al otro rol, no quitandoselos al Rector.

| Permiso delegable | A quien tipicamente |
|---|---|
| Edicion directa de notas | Coordinador Academico |
| Cierre de periodo academico | Coordinador Academico |
| Aprobacion de boletines | Coordinador Academico o Director de Grupo |
| Generacion de constancias | Secretaria Academica |
| Configuración de matrículas (`ingreso.configurar`) | Secretaría Académica, inicialmente desactivado; exige plan `academico` |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Crear o eliminar tenants | Solo el Superadmin (ROL-01) |
| Cambiar calendario A/B habilitado | Solo el Superadmin (RR-13) |
| Acceder a datos de otros colegios | RR-01 Aislamiento total |

## Reglas asociadas

- RR-04 Asignacion de roles por el Rector.
- RR-05 Configurabilidad acotada de permisos.
- RR-13 Cambio de calendario A/B es del Superadmin (el Rector solo elige dentro del habilitado).
- Política de matrículas aceptada el 14 de octubre de 2026: [[../../Logica del negocio/04-procesos-academicos/matriculas|RN-MA-015 y RN-MA-018 a RN-MA-021]]. La delegación válida de `ingreso.configurar` permite usar el mismo formulario institucional, incluida la elección explícita ante conflictos heredados; no habilita cuentas de acudiente.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio.md`
