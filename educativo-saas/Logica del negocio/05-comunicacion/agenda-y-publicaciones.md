---
titulo: Agenda y publicaciones
modulo: 05-comunicacion
tipo: proceso
estado: borrador
tags: [agenda, publicaciones, comunicacion, muro]
---

# Agenda y publicaciones

## Descripción

La **agenda** es un tablón institucional de publicaciones unidireccionales (de la institución hacia los estudiantes y/o acudientes). NO es un chat ni un foro: los receptores no responden dentro de la agenda.

Se usa para informar sobre actividades, tareas, eventos, recordatorios, cambios de horario y comunicados ligeros que no ameritan un [[circulares-y-comunicados|comunicado formal]].

## Quién puede publicar

Los permisos de publicación son **configurables por rol** en cada colegio. La configuración por defecto es:

| Rol | Alcance permitido por defecto |
| --- | --- |
| [[roles/01-rector-administrador-colegio\|Administrador / Rector]] | Toda la institución, cualquier sede / nivel / grado / grupo. |
| [[roles/05-secretaria-academica\|Secretaría Académica]] | Toda la institución. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Niveles / grados a su cargo. |
| [[roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Niveles / grados a su cargo. |
| [[roles/06-docente\|Docente]] | Solo los grupos / asignaturas a los que está asignado. |
| [[roles/07-director-de-grupo\|Director de grupo]] | Su grupo dirigido (además de sus grupos como docente). |

El colegio puede ampliar o restringir estos alcances en su configuración.

## Tipos de contenido en una publicación

Una publicación admite combinar:

- Texto enriquecido (negrita, cursiva, listas, enlaces).
- Imágenes (jpg, png, webp).
- Vídeo embebido o enlazado.
- Archivos adjuntos (PDF, doc, hojas de cálculo).

Los adjuntos consumen cuota de almacenamiento del tenant.

## Atributos de una publicación

| Atributo | Descripción |
| --- | --- |
| Título | Obligatorio. |
| Cuerpo | Texto enriquecido. |
| Adjuntos | Opcionales. |
| Alcance | Toda institución / sede / nivel / grado / grupo / asignatura. |
| Audiencia | Estudiantes, acudientes o ambos. |
| Fecha de publicación | Inmediata o programada. |
| Fecha de expiración | Opcional. La publicación deja de mostrarse en el muro vigente al expirar, pero queda en el historial. |
| Marca de urgente | Si está activa, dispara notificación inmediata sin agrupar. |
| Permite comentarios | Por defecto **no**. La agenda es unidireccional. |

## Vista del muro

- El usuario ve sus publicaciones ordenadas por fecha de publicación descendente.
- Se filtran automáticamente por su contexto (grupos en los que está, sede, nivel).
- Las publicaciones expiradas se muestran en una pestaña separada \"Histórico\".

## Eliminación y edición

- El autor puede editar y eliminar **sus propias** publicaciones.
- El [[roles/01-rector-administrador-colegio|Administrador del Colegio]] puede editar o eliminar **cualquier** publicación de su tenant, dejando rastro en el log de auditoría.
- Las publicaciones eliminadas quedan **archivadas, no borradas físicamente**.
- Se conserva el historial completo (versiones, autores, fechas) para trazabilidad institucional.

## Notificaciones

- Una publicación normal genera notificación según las preferencias y throttling del usuario (ver [[notificaciones]]).
- Una publicación marcada como **urgente** salta el throttling y se notifica de inmediato.
- Las publicaciones programadas notifican en el momento de la publicación efectiva, no al programarlas.

## Reglas de negocio

- **RN-AG-001 — Unidireccional por diseño:** la agenda no admite respuestas ni hilos. Para flujos bidireccionales se usa la mensajería de flujos o las citaciones.
- **RN-AG-002 — Permisos configurables por rol:** los alcances permitidos para publicar son configurables por colegio.
- **RN-AG-003 — Docente limitado a sus grupos:** un docente solo puede publicar para los grupos / asignaturas en los que está asignado.
- **RN-AG-004 — Audiencia controlada:** una publicación llega solo a los usuarios dentro del alcance y la audiencia configurados.
- **RN-AG-005 — Edición y borrado restringidos:** un usuario solo puede editar o borrar sus publicaciones; el administrador del colegio puede sobre cualquiera.
- **RN-AG-006 — Archivado, no borrado físico:** los borrados se archivan; el historial se preserva.
- **RN-AG-007 — Urgente salta throttling:** la marca de urgente fuerza notificación inmediata sin agrupar.
- **RN-AG-008 — Adjuntos consumen cuota:** los adjuntos suman al uso de almacenamiento del tenant.
- **RN-AG-009 — Expiración no borra:** la fecha de expiración solo retira la publicación del muro vigente; no la elimina.

## Notas y pendientes

- Definir el límite recomendado de tamaño por publicación (cuerpo + adjuntos).
- Validar si el sistema soportará menciones (`@grupo`, `@usuario`) en el cuerpo de la publicación.
- Definir si el rector puede activar comentarios por excepción para publicaciones específicas.
