---
titulo: "Rol: Coordinador de Convivencia / Disciplinario"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, coordinador, convivencia, disciplina, tenant]
---

# Rol: Coordinador de Convivencia / Disciplinario

## Identificación

- **Nombre del rol:** Coordinador de Convivencia (también llamado Coordinador Disciplinario en algunos colegios)
- **Tipo de usuario asociado:** Personal directivo del colegio con responsabilidad sobre la disciplina y convivencia escolar
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — permisos configurables dentro de límites del sistema
- **Tipo:** principal

## Descripción

Su ámbito es el **seguimiento del comportamiento y la convivencia escolar**. Gestiona el observador del estudiante, registra anotaciones disciplinarias, compromisos y seguimientos, y coordina con los directores de grupo las situaciones que escalan. No tiene acceso a la gestión de notas ni al módulo académico operativo.

## Responsabilidades

- Gestionar el **observador del estudiante** (documento donde quedan registradas todas las anotaciones disciplinarias y compromisos a lo largo del año).
- Registrar llamados de atención, compromisos y seguimientos.
- Generar reportes de convivencia por estudiante o por grupo.
- Coordinar con los directores de grupo las situaciones disciplinarias que escalan.
- Hacer seguimiento a casos crónicos o estudiantes con observaciones reiteradas.

## Scope / alcance de visibilidad

- Ve el **observador de todos los estudiantes del tenant**.
- Ve los listados de estudiantes por grupo.
- **No ve notas académicas** ni consolidados.
- No ve datos de otros tenants.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Leer observador de cualquier estudiante | Del tenant |
| Registrar llamados de atención y compromisos | En el observador |
| Cerrar / archivar anotaciones | Marcar resoluciones |
| Generar reportes de convivencia | Por estudiante o por grupo |
| Configurar tipologías de anotación | Catálogo del colegio (leve, grave, gravísima, etc.) |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
| --- | --- | --- |
| Acceso al módulo académico (notas) | desactivado | El colegio puede activarlo si decide unificar coordinaciones |
| Citaciones formales a acudientes | configurable | Puede ser exclusivo del Rector |
| Definir sanciones formales | configurable | Algunos colegios lo separan en un comité de convivencia |

## Permisos explícitamente NO otorgados

- No registra ni edita notas académicas.
- No gestiona el plan de estudios ni los horarios.
- No emite documentos oficiales (constancias, certificados).
- No accede a datos de otros tenants.

## Reglas de asignación

- Lo asigna el Rector / Administrador del Colegio.
- Cantidad típica: 1–2 por tenant según el tamaño del colegio.

## Compatibilidad con otros roles

- Un usuario con este rol no requiere roles adicionales.
- Si el colegio fusiona ambas coordinaciones, usar el rol [[04-coordinador-academico-y-convivencia|Coordinador Académico y de Convivencia]].

## Variantes según configuración del colegio

- En colegios pequeños, este rol puede no existir y ser absorbido por el Rector o por el Coordinador Académico (vía rol combinado).
- Algunos colegios prefieren llamarlo "Coordinador de Disciplina" en lugar de "de Convivencia"; el sistema permite renombrarlo.

## Notas y pendientes

- Definir el flujo formal del observador del estudiante: quién registra, quién aprueba, quién notifica al acudiente.
- Definir taxonomía base de tipos de anotación (leve / grave / gravísima) y si es configurable por colegio.
