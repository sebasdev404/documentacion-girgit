---
titulo: Asistencia
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [asistencia, proceso]
---

# Asistencia

## Descripción

Proceso por el cual los docentes registran la presencia o inasistencia de los estudiantes en cada sesión de clase. El sistema acumula los conteos por estudiante, materia y periodo, y emite alertas cuando se superan los porcentajes máximos configurados.

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

## Justificaciones de inasistencia

1. El estudiante (o el acudiente) ingresa al portal y solicita justificar una inasistencia específica.
2. Adjunta una explicación y opcionalmente un soporte (incapacidad médica, carta del acudiente, etc.).
3. La solicitud queda en estado **pendiente de revisión**.
4. El docente o el coordinador (según configuración del colegio) revisa la justificación.
5. Aprueba o rechaza con observación.
6. Si es aprobada, la inasistencia queda marcada como `Justificada` en el registro pero **sigue contando para el historial**.

## Alertas por inasistencia

- El colegio configura un porcentaje máximo de inasistencias permitidas por materia y periodo (ej. 20%).
- Cuando un estudiante supera ese porcentaje en una materia, el sistema genera una alerta para el docente y el coordinador.
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
