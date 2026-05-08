---
titulo: Reportes académicos
modulo: reportes-y-analitica
tipo: referencia
estado: borrador
tags: [reportes, academicos]
---

# Reportes académicos

## Catálogo

| Reporte | Audiencia | Frecuencia | Datos incluidos |
| --- | --- | --- | --- |
| Boletín por estudiante | Estudiante / acudiente. | Por periodo y final. | Notas por área / asignatura, comentarios, asistencia, observaciones. |
| Boletín por grupo | Director de grupo, coordinación. | Por periodo. | Boletines consolidados de todos los estudiantes del grupo. |
| Reporte de asistencia por grupo | Coordinación, director de grupo. | Diario / semanal / mensual. | % asistencia, ausencias justificadas vs no, retrasos. |
| Reporte de asistencia por estudiante | Acudiente, coordinación. | Bajo demanda. | Inasistencias por fecha y materia, justificaciones. |
| Reporte de aprobación / reprobación | Coordinación, rector. | Por periodo y final. | % aprobación por área, por grupo, por nivel. |
| Listado de estudiantes con materias en recuperación | Coordinación. | Por periodo y al cierre. | Estudiantes, materias, valor reprobado. |
| Listado de matrículas activas | Secretaría, rector. | Bajo demanda. | Estudiantes activos, retirados, nuevos. |
| Carpeta del estudiante | Secretaría. | Bajo demanda. | Documentos, contratos, soportes, observaciones. |
| Observador del estudiante | Director de grupo, coordinación. | Bajo demanda. | Anotaciones positivas y disciplinarias con seguimiento. |
| Reporte de comportamiento del grupo | Coordinación de convivencia. | Mensual. | Anotaciones por tipo, tendencias. |
| Certificado de notas | Estudiante / egresado. | Bajo demanda. | Notas finales por año cursado. |
| Certificado de estudio | Estudiante / acudiente. | Bajo demanda. | Constancia de matrícula y grado actual. |
| Listas oficiales por grupo | Director de grupo. | Inicio de año. | Lista nominal con foto y datos básicos. |
| Reporte de cumplimiento de plan de estudios | Coordinación académica. | Por periodo. | Logros / temas vistos vs planeados. |

## Filtros y parámetros disponibles

- Sede / nivel / grado / grupo / estudiante.
- Año lectivo (incluye años cerrados).
- Periodo (específico o consolidado anual).
- Área / asignatura / docente.
- Estado de matrícula (activos, retirados, todos).
- Rango de fechas (para asistencia y observador).

## Formatos de exportación

- PDF (con plantilla del colegio).
- Excel / CSV.
- Vista en pantalla con paginación.

## Reglas de negocio

- **RN-RA-001 — Visibilidad por rol:** un usuario solo ve datos a los que su rol tiene acceso (ver [[../02-usuarios-roles-y-permisos/matriz-de-permisos|Matriz de permisos]]).
- **RN-RA-002 — Reportes históricos consistentes:** los reportes de años cerrados usan la configuración vigente en ese año (escala, plan de estudios).
- **RN-RA-003 — Exportación auditada:** exportar reportes que contienen datos personales queda en el log.
- **RN-RA-004 — Datos sensibles enmascarables:** los reportes pueden ocultar identificación cuando se exportan para fines analíticos.

## Notas y pendientes

- Definir catálogo de plantillas oficiales por colegio para los certificados.
- Validar la lista exacta de reportes incluidos en plan Esencial vs Premium.
