---
titulo: "Rol: Coordinador Académico"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, coordinador, academico, tenant]
---

# Rol: Coordinador Académico

## Identificación

- **Nombre del rol:** Coordinador Académico
- **Tipo de usuario asociado:** Personal directivo del colegio con responsabilidad académica
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — permisos configurables dentro de límites del sistema
- **Tipo:** principal

## Descripción

Gestiona todo lo relacionado con la **estructura académica operativa del colegio**: plan de estudios, grupos, asignación docente, horarios, consolidados de notas y procesos de cierre de período. No puede modificar la configuración base del sistema (eso es solo del Rector).

## Responsabilidades

### Plan de estudios y currículo
- Crear y gestionar el plan de estudios: qué materias existen por grado, con qué intensidad horaria semanal y a qué área del conocimiento pertenecen.

### Grupos y asignaciones
- Crear y gestionar los grupos por grado y año lectivo.
- Asignar docentes a materias y grupos.
- Asignar directores de grupo (designar qué docente cumple ese complemento sobre qué grupo).

### Horarios
- Construir y administrar los horarios de clase: qué docente dicta qué materia, en qué aula, en qué bloque horario y qué día.

### Procesos académicos
- Ver consolidados de notas de todos los grupos.
- Gestionar los procesos de nivelación y habilitación de estudiantes que pierden materias.
- Coordinar el proceso de cierre de períodos académicos.

## Scope / alcance de visibilidad

- Ve **todos los grupos, materias, docentes y estudiantes del tenant**.
- Ve consolidados de notas de todos los grupos.
- No ve datos de otros tenants.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Gestionar plan de estudios | Crear, editar, archivar materias por grado |
| Crear y gestionar grupos | Por grado y año lectivo |
| Asignar docentes a materias y grupos | |
| Designar directores de grupo | |
| Construir y editar horarios de clase | |
| Ver consolidados de notas | De todos los grupos del tenant |
| Gestionar nivelaciones y habilitaciones | Para estudiantes que pierden materias |
| Coordinar cierre de períodos académicos | Activar/desactivar el cierre, validar consolidados |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
| --- | --- | --- |
| Editar notas directamente | configurable | Algunos colegios lo permiten al coordinador, otros lo restringen al docente titular |
| Aprobar / firmar boletines | configurable | Puede delegarse al Rector o quedar acá |
| Crear años lectivos nuevos | configurable | Puede ser exclusivo del Rector |

## Permisos explícitamente NO otorgados

- No modifica la configuración base del sistema (escala valorativa, jornadas, modelo pedagógico, calendario académico) — eso es del Rector.
- No accede al observador disciplinario salvo que el colegio tenga el rol combinado activo.
- No emite documentos oficiales (constancias, certificados) — eso es de la Secretaría.
- No accede a datos de otros tenants.

## Reglas de asignación

- Lo asigna el Rector / Administrador del Colegio.
- Cantidad típica: 1–3 por tenant según el tamaño del colegio.

## Compatibilidad con otros roles

- Un usuario con rol Coordinador Académico no necesita roles adicionales para sus responsabilidades habituales.
- Si el colegio fusiona ambas coordinaciones, usar el rol [[04-coordinador-academico-y-convivencia|Coordinador Académico y de Convivencia]] en lugar de asignar dos roles.

## Variantes según configuración del colegio

- En colegios pequeños, este rol puede no existir y ser absorbido por el Rector.
- En colegios donde académico y convivencia están unidos, se usa el rol combinado.

## Notas y pendientes

- Definir si el coordinador puede reabrir un período académico ya cerrado o si eso requiere intervención del Rector.
- Definir el flujo de nivelación / habilitación con detalle (caso de uso aparte).
