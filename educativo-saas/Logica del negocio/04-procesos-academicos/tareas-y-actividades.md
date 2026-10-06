---
titulo: Tareas y actividades
modulo: procesos-academicos
tipo: proceso
estado: implementacion-en-curso
tags: [tareas, actividades, lms-lite, entregas, proceso]
---

# Tareas y actividades

## Descripción

Proceso por el cual los docentes publican tareas y actividades en el Aula por asignatura, adjuntan recursos de apoyo, reciben entregas y devuelven retroalimentación y calificación. El Aula también incluye cuestionarios nativos (ver [[plan-aula-virtual-y-ayuda-asistencia-2026-10-06|Plan de Aula]]). **No es un chat**: el intercambio se limita a la entrega del estudiante y la retroalimentación del docente sobre esa entrega.

## Objetivo del proceso

Dar a los docentes una vía dentro de la plataforma para asignar trabajo, recibirlo y devolver una valoración trazable, de modo que esa valoración pueda alimentar la nota del componente evaluativo correspondiente en [[calificaciones|Calificaciones]] sin doble digitación.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[roles/06-docente\|Docente]] | Crea y publica tareas en las materias × grupo donde tiene asignación activa; adjunta recursos; revisa entregas; retroalimenta y califica. |
| [[roles/08-estudiante-y-acudiente\|Estudiante]] | Consulta la tarea, adjunta su entrega y la envía antes de la fecha límite. |
| [[roles/08-estudiante-y-acudiente\|Acudiente]] | Consulta (no entrega) las tareas y el estado de entrega de su acudido desde el portal. |
| [[roles/07-director-de-grupo\|Director de Grupo]] | Visibilidad consolidada de las tareas y el cumplimiento de su grupo. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Supervisión; consulta de actividad por área/grado. No publica tareas. |

## Precondiciones

- El docente tiene asignación activa en la combinación materia × grupo (ver [[asignacion-docentes|Asignación de docentes]]).
- El periodo académico al que se imputa la tarea está `Abierto`.
- El colegio tiene habilitado el módulo de tareas (es configurable, ver más abajo).

## Flujo principal

1. El docente crea una tarea: título, instrucciones, materia, grupo(s) destino y fecha límite.
2. Opcionalmente adjunta recursos de apoyo (PDF, imagen, enlace) que **consumen la cuota de almacenamiento del colegio** (ver [[../11-plataforma-y-operacion/almacenamiento-y-cuotas|Almacenamiento y cuotas]]).
3. El docente decide si la tarea es **calificable** y, si lo es, a qué componente evaluativo del periodo se vinculará.
4. El docente publica la tarea. El sistema notifica a los estudiantes del grupo (y a sus acudientes, según configuración del colegio).
5. El estudiante abre la tarea, adjunta su entrega (archivo y/o texto) y la envía. La entrega también consume cuota del colegio.
6. El sistema marca la entrega como `Entregada` o `Entregada con retraso` según la hora frente a la fecha límite.
7. El docente revisa cada entrega, escribe retroalimentación y, si la tarea es calificable, asigna una valoración.
8. La tarea puede quedar sin vincular. Si se vincula a Planilla, la calificación docente se registra allí como nota oficial con versión y auditoría. Para cuestionarios objetivos la transferencia puede ser automática o requerir confirmación docente, según la opción del recurso.
9. El sistema notifica al estudiante (y acudiente) que su entrega fue retroalimentada/calificada.

## Flujos alternativos

- **Entrega tardía:** si el colegio permite entregas tras la fecha límite, el estudiante puede entregar y el sistema la marca `Entregada con retraso`; si no las permite, el botón de entrega se cierra a la fecha límite.
- **Reentrega:** si el docente lo habilita en la tarea, el estudiante puede reemplazar su entrega antes de la fecha límite (o de la ventana de retraso). Cada versión queda registrada.
- **Devolución para corregir:** el docente puede devolver una entrega con observaciones para que el estudiante la corrija y reenvíe, sin calificar todavía.
- **Sin entrega:** vencida la fecha límite, las entregas faltantes quedan `No entregada`; el docente puede calificarlas con la nota mínima si la tarea es calificable, según la política del colegio.

## Configurabilidad por colegio

- Activación del módulo de tareas (un colegio puede operar sin esta capa).
- Si se permiten **entregas tardías** y si descuentan valoración automáticamente.
- Si las tareas calificables alimentan la nota **automáticamente** o solo como propuesta que el docente confirma.
- Si los **acudientes** reciben notificación de cada tarea publicada o solo del estado de entrega.
- Tamaño y tipo de adjunto permitido (heredado de la política de almacenamiento del plan).

## Visibilidad

- Una tarea es visible **solo para el grupo (o grupos) destino** y para los roles con supervisión sobre ese grupo. Un estudiante nunca ve las entregas de sus compañeros.
- El docente ve todas las entregas de sus grupos; el director de grupo ve las de su grupo en modo consulta.
- El acudiente ve únicamente lo correspondiente a su acudido.

## Estados y transiciones

### Tarea

```
Borrador → Publicada → Cerrada (fecha límite vencida) → Archivada
```

### Entrega del estudiante

```
Pendiente → Entregada / Entregada con retraso → Retroalimentada → Calificada
Pendiente → No entregada (al vencer la fecha límite sin envío)
Entregada → Devuelta para corregir → Entregada (reenvío)
```

## Integraciones con otros módulos

- [[calificaciones|Calificaciones]] (`RN-CA`): una tarea calificable propone la nota de un componente evaluativo; la confirmación final la hace el docente.
- [[../11-plataforma-y-operacion/almacenamiento-y-cuotas|Almacenamiento y cuotas]] (`RN-AC`): recursos y entregas consumen la cuota del tenant; aplican antivirus, whitelist de tipos y bloqueo al 100%.
- [[../05-comunicacion/notificaciones|Notificaciones]]: avisos de publicación, vencimiento y retroalimentación.
- [[observador-del-estudiante|Observador del estudiante]]: el incumplimiento reiterado puede originar una anotación, pero la tarea en sí no escribe en el observador automáticamente.
- [[periodos-academicos|Periodos académicos]]: una tarea se imputa a un periodo `Abierto`; al cierre del periodo se bloquea su edición.

## Reglas de negocio

- **RN-TA-001 — Publicación solo con asignación activa:** un docente solo puede crear y publicar tareas en combinaciones materia × grupo donde tiene asignación activa.
- **RN-TA-002 — Visibilidad acotada al grupo:** una tarea y sus entregas son visibles solo para el grupo destino y los roles con supervisión; un estudiante nunca ve la entrega de otro.
- **RN-TA-003 — Adjuntos consumen cuota del tenant:** recursos del docente y entregas del estudiante se almacenan en el bucket del colegio y consumen su cuota; aplican las validaciones de [[../11-plataforma-y-operacion/almacenamiento-y-cuotas|Almacenamiento y cuotas]].
- **RN-TA-004 — Fecha límite configurable:** una tarea puede tener fecha y hora límite o quedar sin restricción. Si existe límite, el servidor lo aplica; entregas posteriores solo si el recurso lo permite expresamente.
- **RN-TA-005 — Planilla como registro oficial:** vincular un recurso es opcional y crea una única actividad. Las tareas calificadas por docente transfieren la valoración al guardarse; un cuestionario objetivo puede configurarse con confirmación docente o transferencia automática. La calificación oficial reside en Planillas; el vínculo posterior incorpora notas previas idempotentemente y no reemplaza una nota oficial ya editada.
- **RN-TA-006 — Imputación a periodo abierto:** una tarea solo puede crearse o editarse contra un periodo `Abierto`; al cierre del periodo la tarea y sus valoraciones quedan bloqueadas.
- **RN-TA-007 — Entrega tardía configurable:** la aceptación de entregas tras la fecha límite y su eventual descuento de valoración los define el colegio en su configuración.
- **RN-TA-008 — No es canal de mensajería:** el intercambio se limita a entrega y retroalimentación sobre esa entrega; no existe conversación libre entre estudiante y docente dentro de la tarea.
- **RN-TA-009 — Versionado de entregas:** cada reenvío o devolución para corregir conserva la versión anterior para trazabilidad; no se sobrescribe sin historial.
- **RN-TA-010 — Auditoría de la valoración:** registrar o editar la valoración de una entrega queda en el log con valor anterior y nuevo, usuario, fecha y hora.

## Notas y pendientes

- **[Decisión actualizada]** El vínculo tarea → actividad de Planilla es opcional y la Planilla es el registro oficial. El cuestionario objetivo admite transferencia inmediata solo si se configuró así; por defecto requiere confirmación.
- **[Decisión actualizada]** El Aula incorpora cuestionarios construidos dentro de Coscolegios; no integra motores de examen externos. Las preguntas abiertas requieren revisión docente.
- **[Pendiente — producto]** Definir si la **acumulación de incumplimientos** de tareas dispara una alerta automática (semáforo) y si esa alerta sugiere o no una anotación en el observador. Candidata a regla `RN-TA-020`.
- **[Pendiente — producto]** Validar durante el piloto si los acudientes deben recibir notificación de **cada** tarea publicada o solo de vencimientos y resultados, para no saturar el canal.

## Documentos relacionados

- [[calificaciones|Calificaciones]]
- [[asignacion-docentes|Asignación de docentes]]
- [[periodos-academicos|Periodos académicos]]
- [[observador-del-estudiante|Observador del estudiante]]
- [[../11-plataforma-y-operacion/almacenamiento-y-cuotas|Almacenamiento y cuotas]]
- [[../05-comunicacion/notificaciones|Notificaciones]]
- [[roles/06-docente|Docente]]
- [[roles/08-estudiante-y-acudiente|Estudiante y acudiente]]
