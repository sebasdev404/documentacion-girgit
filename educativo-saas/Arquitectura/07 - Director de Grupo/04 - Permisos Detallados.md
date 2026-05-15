---
tags:
  - arquitectura
  - rol/director-de-grupo
  - permisos
aliases:
  - Permisos ROL-08
---

# Permisos Detallados — Director de Grupo (complemento)

Permisos **adicionales** sobre el grupo dirigido. Se SUMAN a los del Docente. En otros grupos, sigue siendo solo Docente.

Vista cruzada en [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]].

## Permisos estructurales adicionales (no modificables)

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Consolidados** | Ver consolidado completo del grupo | Ver | Todas las materias del grupo dirigido |
| **Boletines** | Generar boletines del grupo | Reportar | Del grupo dirigido |
| **Boletines** | Agregar observacion general en boletin | Editar | Por estudiante, sobre el grupo dirigido |
| **Observador disciplinario** | Registrar anotaciones | Editar | De estudiantes del grupo dirigido |
| **Asistencia** | Consultar asistencia del grupo | Ver | Del grupo dirigido |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
|---|---|---|
| Editar notas de materias que no dicta | desactivado | Algunos colegios lo permiten con justificacion; otros lo prohiben |
| Aprobar / firmar boletines del grupo | configurable | Puede quedar en el director, en el Coord. Academico o en el Rector |
| Citar acudientes formalmente | configurable | Puede ser potestad exclusiva del Coord. de Convivencia |
| Ver promedios historicos de los estudiantes del grupo | configurable | |
| Descargar boletin del grupo en PDF | activado | |
| Comunicarse con acudientes via portal | configurable | |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Aplicar estos permisos a otros grupos | RR-09. Solo sobre el grupo dirigido |
| Acceder a configuraciones del colegio | Es del Rector |
| Emitir documentos oficiales | Es de la Secretaria |

## Reglas asociadas

- RR-09 Director de Grupo solo opera sobre su grupo.
- Pre-requisito: la persona debe tener ROL-07 (Docente) para poder recibir este complemento.

## Variantes segun modelo pedagogico

- **Docente unico por salon**: el director es ese mismo docente; sus permisos extra se traslapan con los del Docente sobre el mismo grupo.
- **Rotacion**: el director es uno de los varios docentes que rotan; los permisos extra se notan mas.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/07-director-de-grupo.md`
