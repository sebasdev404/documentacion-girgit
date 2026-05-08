---
titulo: Mensajería interna
modulo: comunicacion
tipo: proceso
estado: borrador
tags: [mensajeria, comunicacion]
---

# Mensajería interna

## Descripción

La mensajería interna NO es el canal principal del sistema. La plataforma se concibe como una herramienta de **gestión y difusión**, no como un chat bidireccional. Sin embargo, existen flujos limitados de mensajería para casos puntuales.

> **Nota de alcance:** la mensajería libre tipo chat entre estudiantes y docentes está fuera del alcance del lanzamiento (ver [[../01-vision-y-alcance/alcance-y-no-alcance|Alcance y no-alcance]]).

## Qué sí se incluye

- **Solicitud de cita** del estudiante o acudiente hacia un docente o coordinación.
- **Respuesta de citación** del personal hacia el estudiante o acudiente.
- **Hilos de revisión** asociados a flujos del sistema (justificación de inasistencia, apelación de anotación, observación sobre documento de matrícula).

Estos hilos no son chat libre: son intercambios estructurados ligados a un flujo concreto.

## Qué NO se incluye

- Conversaciones libres 1 a 1 entre estudiantes y docentes fuera de un flujo del sistema.
- Conversaciones grupales tipo chat.
- Reacciones, hilos en cascada, intercambio de archivos sin contexto de flujo.

## Estructura de un hilo de revisión

Cada hilo está asociado a:

- Un flujo del sistema (justificación, apelación, documento de matrícula, citación).
- El estudiante o acudiente involucrado.
- El personal del colegio que revisa.
- Estado del flujo (pendiente, aprobado, rechazado).

Los mensajes dentro del hilo siguen una estructura simple: autor, contenido, fecha, adjunto opcional.

## Moderación y reportes de abuso

- El [[roles/01-rector-administrador-colegio|Administrador del Colegio]] tiene acceso completo a los hilos para moderación.
- Cualquier usuario puede reportar un mensaje. El reporte llega al administrador.
- El administrador puede ocultar mensajes con motivo registrado.

## Retención y privacidad

- Los hilos forman parte del registro del flujo asociado y se retienen junto con él.
- Al cerrarse el año lectivo, los hilos asociados a flujos del año quedan inmutables.
- Eliminación de un mensaje no es física: queda marcado como oculto con auditoría.

## Reglas de negocio

- **RN-MI-001 — Mensajería ligada a flujo:** no existen mensajes fuera de un flujo concreto del sistema.
- **RN-MI-002 — Privacidad por contexto:** un mensaje solo es visible para los participantes del flujo y para los roles con autoridad de moderación.
- **RN-MI-003 — Auditoría obligatoria:** creación, ocultamiento y reporte de mensajes quedan en el log.
- **RN-MI-004 — Adjuntos consumen cuota:** los adjuntos cuentan contra la cuota de almacenamiento del tenant.

## Matriz de quién puede mensajear a quién

| Origen | Destino permitido |
| --- | --- |
| Estudiante / acudiente | Docente (en contexto de cita) / Coordinación / Secretaría |
| Docente | Estudiantes / acudientes de sus grupos asignados (en contexto de flujo) |
| Director de grupo | Estudiantes / acudientes de su grupo |
| Coordinación / Secretaría | Cualquier usuario del tenant en contexto de flujo |
| Administrador | Cualquier usuario |

## Notas y pendientes

- Validar si una segunda fase incluirá mensajería libre con moderación automática.
- Definir si la "solicitud de cita" del portal genera automáticamente un hilo de mensajería asociado.
