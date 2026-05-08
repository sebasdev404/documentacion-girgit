---
titulo: "Rol: Director de Grupo (complemento)"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, director-de-grupo, complemento, docente, tenant]
---

# Rol: Director de Grupo (complemento)

## Identificación

- **Nombre del rol:** Director de Grupo
- **Tipo de usuario asociado:** Docente designado como director de un grupo específico
- **Ámbito:** Tenant — **complemento sobre un grupo concreto**
- **Configurable por el colegio:** sí — varios permisos del complemento son configurables
- **Tipo:** **complemento** (no rol principal). Solo se asigna sobre un usuario que ya tiene el rol de [[06-docente|Docente]].

## Descripción

Director de Grupo es un **complemento** que se asigna a un docente sobre un grupo específico. **No reemplaza** al rol Docente: se suma. Cuando un docente es director de un grupo, adquiere permisos adicionales **únicamente sobre ese grupo**.

## Responsabilidades

Sobre el grupo dirigido:
- Acompañar al grupo a lo largo del año lectivo.
- Generar y revisar los **boletines** del grupo.
- Agregar **observaciones generales** por estudiante en el boletín.
- Registrar anotaciones en el **observador del estudiante** del grupo.
- Coordinar con el Coordinador de Convivencia las situaciones disciplinarias que escalan.

## Scope / alcance de visibilidad

- Ve **el consolidado completo de notas** del grupo dirigido (todas las materias, no solo las que él mismo dicta).
- Ve el observador de los estudiantes de su grupo.
- Mantiene además todo el scope que tiene como Docente sobre sus materias asignadas (en otros grupos).
- No ve datos de otros tenants.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Ver consolidado completo de notas del grupo | Todas las materias del grupo dirigido |
| Agregar observaciones generales en boletín | Por estudiante, sobre el grupo dirigido |
| Gestionar la generación de boletines | Del grupo dirigido |
| Registrar anotaciones en el observador | De los estudiantes del grupo dirigido |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
| --- | --- | --- |
| Editar notas de materias que no dicta | desactivado | Algunos colegios lo permiten con justificación; otros lo prohíben totalmente |
| Aprobar / firmar boletines del grupo | configurable | Puede quedar en el director, en el Coord. Académico o en el Rector |
| Citar a acudientes formalmente | configurable | Puede ser potestad del Coord. de Convivencia |
| Ver promedios históricos de los estudiantes del grupo | configurable | |

## Permisos explícitamente NO otorgados

- Sus permisos adicionales aplican **solo sobre el grupo dirigido**. En otros grupos sigue siendo solo Docente sobre sus materias asignadas.
- No accede a configuraciones del colegio.
- No emite documentos oficiales (sigue siendo de la Secretaría).

## Reglas de asignación

- Lo asigna el Coordinador Académico al designar al docente como director del grupo.
- **Pre-requisito**: la persona debe tener ya el rol Docente.
- Un docente puede ser director de **uno o más grupos** simultáneamente (poco común, pero permitido).
- Un grupo tiene típicamente **un único director** activo.

## Compatibilidad con otros roles

- Es un complemento del rol **Docente**. Compatible con cualquier configuración del Docente.
- No es compatible asignar este complemento a un usuario que no sea docente.

## Variantes según configuración del colegio

- En el modelo de **docente único por salón** (típico en primaria), el director de grupo suele ser ese mismo docente y los permisos del complemento se traslapan con los del Docente sobre el mismo grupo.
- En el modelo de **rotación** (bachillerato), el director es uno de los varios docentes que rotan, y sus permisos adicionales sobre el grupo se notan más.

## Notas y pendientes

- Definir si al cambiar el director de un grupo a mitad de año se conservan o no las observaciones que el director saliente registró.
- Definir flujo de transición de director de grupo entre años lectivos.
