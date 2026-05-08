---
titulo: "Rol: Coordinador Académico y de Convivencia (combinado)"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, coordinador, combinado, academico, convivencia, tenant]
---

# Rol: Coordinador Académico y de Convivencia (combinado)

## Identificación

- **Nombre del rol:** Coordinador Académico y de Convivencia
- **Tipo de usuario asociado:** Personal directivo del colegio que asume ambas responsabilidades
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — el colegio decide si lo activa en lugar de tener los dos coordinadores separados
- **Tipo:** principal

## Descripción

Rol **combinado** que une las responsabilidades del [[02-coordinador-academico|Coordinador Académico]] y del [[03-coordinador-convivencia|Coordinador de Convivencia]]. Pensado para colegios pequeños o medianos donde no existe la división organizacional entre ambas coordinaciones.

## Responsabilidades

Hereda **todas las responsabilidades** de los dos roles base:

### Académicas (ver [[02-coordinador-academico|Coordinador Académico]])
- Plan de estudios, intensidad horaria y áreas del conocimiento.
- Crear y gestionar grupos por grado y año lectivo.
- Asignar docentes a materias y grupos; designar directores de grupo.
- Construir y administrar horarios de clase.
- Ver consolidados de notas, gestionar nivelaciones y habilitaciones.
- Coordinar el cierre de períodos académicos.

### De convivencia (ver [[03-coordinador-convivencia|Coordinador de Convivencia]])
- Gestionar el observador del estudiante.
- Registrar llamados de atención, compromisos y seguimientos.
- Generar reportes de convivencia.
- Coordinar con directores de grupo las situaciones que escalan.

## Scope / alcance de visibilidad

- Ve **todos los grupos, materias, docentes, estudiantes y consolidados** del tenant.
- Ve el **observador de todos los estudiantes** del tenant.
- No ve datos de otros tenants.

## Permisos estructurales (no modificables)

Son la unión de los permisos estructurales del Coordinador Académico y del Coordinador de Convivencia. Ver cada archivo para el detalle.

## Permisos configurables por el colegio

Hereda los permisos configurables de ambos roles. Aplican las mismas reglas:

| Permiso | Default | Notas |
| --- | --- | --- |
| Editar notas directamente | configurable | Hereda del Coord. Académico |
| Aprobar / firmar boletines | configurable | Hereda del Coord. Académico |
| Citaciones formales a acudientes | configurable | Hereda del Coord. de Convivencia |
| Definir sanciones formales | configurable | Hereda del Coord. de Convivencia |

## Permisos explícitamente NO otorgados

- No modifica la configuración base del sistema (escala valorativa, jornadas, modelo pedagógico, calendario académico) — sigue siendo del Rector.
- No emite documentos oficiales (constancias, certificados) — sigue siendo de la Secretaría.
- No accede a datos de otros tenants.

## Reglas de asignación

- Lo asigna el Rector / Administrador del Colegio.
- **Mutualmente exclusivo**: si el tenant activa el rol combinado, normalmente no usa los dos coordinadores por separado. La política recomendada es **o uno, o los otros dos**, no ambos esquemas simultáneamente.
- Cantidad típica: 1 por tenant.

## Compatibilidad con otros roles

- No es compatible con tener simultáneamente Coordinador Académico y Coordinador de Convivencia separados (ver "Reglas de asignación").
- Sigue siendo compatible con el complemento Director de Grupo si el coordinador también dicta clase y dirige un grupo.

## Variantes según configuración del colegio

- Activar este rol es una decisión organizacional del colegio. Muchos colegios pequeños lo prefieren por simplicidad.
- En colegios grandes lo común es separar las dos coordinaciones.

## Notas y pendientes

- Definir si el sistema bloquea automáticamente la asignación de los dos roles separados cuando ya hay alguien con el rol combinado, o solo lanza una advertencia.
