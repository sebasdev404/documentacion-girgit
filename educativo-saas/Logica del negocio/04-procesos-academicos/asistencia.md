---
titulo: Asistencia
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [asistencia, proceso]
---

# Asistencia

## Descripción

Proceso por el cual los docentes registran la presencia o inasistencia de los estudiantes en cada sesión de clase. La captura por franja y la acumulación/alerta provisional ya están en código de trabajo; las consecuencias académicas por umbral siguen pendientes.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[roles/06-docente\|Docente]] | Registra la asistencia de las sesiones de las materias en las que tiene asignación activa. |
| [[roles/07-director-de-grupo\|Director de Grupo]] | Tiene visibilidad consolidada de la asistencia de su grupo. |
| [[roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Recibe alertas y gestiona casos de inasistencia recurrente. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Recibe alertas relacionadas a desempeño académico. |
| [[roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | Consulta el registro propio y puede justificar inasistencias. |

## Tipos de marca

| Marca | Descripción | Cuenta para inasistencia |
| --- | --- | --- |
| Presente | El estudiante asistió a la sesión. | No |
| Ausente | El estudiante no asistió ni hay justificación. | Sí |
| Tarde | El estudiante llegó después del inicio de la sesión. | Configurable: si supera N tardes equivale a una inasistencia. |
| Justificada | Inasistencia con justificación aprobada. | Sí (cuenta para historial pero generalmente no afecta aprobación). |

## Flujo principal

1. El docente abre la sesión correspondiente al bloque y materia que está dictando.
2. El sistema muestra el listado del grupo con cada estudiante.
3. El docente marca el estado de cada estudiante (presente / ausente / tarde).
4. El docente guarda el registro.
5. El sistema actualiza los conteos acumulados por estudiante, materia y periodo.
6. Si algún estudiante supera el porcentaje máximo de inasistencias configurado, el sistema genera una alerta para el docente y los coordinadores.

### Unidad de registro y política pendiente — decisión de producto del 5 de octubre de 2026

- Registrar la asistencia por **cada franja explícita programada del grupo y la asignatura**, incluso si el colegio no usa bloques horarios fijos. Una franja larga cuenta como una oportunidad, no como tantas horas dure. Dos faltas requieren dos franjas explícitas en Horarios; si asiste a una de ellas, solo hay una ausencia.
- La duración física de cada franja puede variar. No convertir automáticamente minutos de clase en "horas de inasistencia" sin una regla institucional explícita; la unidad inicial propuesta es la **sesión/franja** del horario.
- El colegio debe poder configurar si la asistencia solo informa y alerta, o si superar un umbral por asignatura repercute en su aprobación. La consecuencia nunca se aplica con un número fijo global como "tres faltas" para todos los colegios.
- Quedan por decidir con el colegio: umbral por cantidad o porcentaje, período o año, tratamiento de faltas justificadas y tardanzas, clases canceladas/festivos, correcciones y posibles excepciones autorizadas. Estas decisiones deben reflejarse coherentemente en el boletín y en la revisión de promoción.
- **Estado de implementación inicial:** existe captura de presente/ausente/tarde por franja y fecha, con instantánea de identidad y horario, auditoría, control de versión contra sobrescrituras concurrentes y bloqueo de edición cuando el período está cerrado. La primera versión no incluye aprobación de justificaciones ni consecuencias académicas automáticas.
- **Política de alerta implementada en código de trabajo:** por año lectivo se pueden configurar umbrales por cantidad y porcentaje, combinación «uno cualquiera» o «ambos», acumulación por período o año y equivalencia de N tardanzas a una falta. Se alerta cuando el valor **supera**, no cuando iguala, el máximo. El denominador usa exclusivamente las franjas cuya asistencia se registró para ese estudiante; los porcentajes son provisionales y la comparación usa el cociente antes de redondear el porcentaje mostrado. No se modifica ninguna nota, boletín ni decisión de promoción.
- Antes de activar consecuencias académicas faltan la aprobación de justificaciones, la exclusión de clases canceladas/festivos, la verificación de completitud de registro, el tratamiento normativo de las faltas justificadas y pruebas de cierre con la política vigente.

## Justificaciones de inasistencia

1. El estudiante (o el acudiente) ingresa al portal y solicita justificar una inasistencia específica.
2. Adjunta una explicación y opcionalmente un soporte (incapacidad médica, carta del acudiente, etc.).
3. La solicitud queda en estado **pendiente de revisión**.
4. El docente o el coordinador (según configuración del colegio) revisa la justificación.
5. Aprueba o rechaza con observación.
6. Si es aprobada, la inasistencia queda marcada como `Justificada` en el registro pero **sigue contando para el historial**.

## Alertas por inasistencia

- El colegio configura un máximo de faltas y/o porcentaje por materia, con alcance por período o año.
- Cuando un estudiante supera el umbral configurado, la lista de asistencia muestra una alerta provisional al docente y a los responsables que pueden consultar esa asignación. Todavía no se envían notificaciones automáticas.
- La consecuencia sobre la nota o la aprobación la define el colegio en su configuración (puede ser perder la materia automáticamente, requerir comité de evaluación, o ninguna).

## Estados y transiciones

### Marca de asistencia

```
No registrada → Registrada → Editada (mientras el periodo esté abierto)
```

### Justificación

```
No solicitada → Pendiente de revisión → Aprobada
                                       → Rechazada
```

## Datos involucrados

- Sesión (combinación de fecha + bloque + grupo + materia).
- Estudiante.
- Marca (presente / ausente / tarde / justificada).
- Docente que registra.
- Fecha y hora del registro.
- Adjuntos y observaciones de la justificación si aplica.

## Reportes asociados

- Asistencia por estudiante en un periodo / año.
- Asistencia por grupo y materia.
- % de inasistencia por estudiante (alerta si supera umbral).
- Listado de justificaciones pendientes.

Ver [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]].

## Reglas de negocio

- **RN-AS-001 — Registro solo con asignación activa:** un docente solo puede registrar asistencia en combinaciones materia × grupo donde tiene asignación activa.
- **RN-AS-002 — Asistencia por sesión:** el registro es por cada sesión del horario; no se permite consolidado diario sin granularidad por bloque.
- **RN-AS-003 — Justificación no elimina la inasistencia:** una justificación aprobada cambia la marca a `Justificada` pero la inasistencia permanece en el historial.
- **RN-AS-004 — Alertas automáticas:** el sistema genera alertas automáticas al superar el umbral configurado.
- **RN-AS-005 — Edición hasta cierre del periodo:** las marcas de asistencia se pueden editar hasta el cierre del periodo. Después solo con ventana de corrección autorizada.
- **RN-AS-006 — Festivos no generan asistencia:** las sesiones que caen en días marcados como festivo no generan registro de asistencia.
- **RN-AS-007 — Auditoría obligatoria:** ediciones de marcas de asistencia quedan registradas en el log con valor anterior y nuevo.

## Notas y pendientes

- **[Decisión tomada]** La acumulación de tardes/llegadas tarde como inasistencia es **configurable por colegio**: cada colegio define cuántas tardes equivalen a una inasistencia (puede dejarlo en cero si no quiere acumular). Regla: **RN-AS-020 — Acumulación de tardes configurable por colegio**.
- **[Pendiente UX]** Validar el flujo de "asistencia por toma rápida" para grupos grandes (marcar todo presente y solo individualizar ausentes) durante el piloto.
