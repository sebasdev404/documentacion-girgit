---
titulo: Notificaciones
modulo: comunicacion
tipo: referencia
estado: borrador
tags: [notificaciones, comunicacion]
---

# Notificaciones

## Canales

| Canal | Descripción | Disponibilidad |
| --- | --- | --- |
| Portal | Buzón de notificaciones dentro del portal del colegio. | Todos los planes. |
| Correo electrónico | Envío al correo registrado del usuario. | Todos los planes. |
| Push (web/móvil) | Notificaciones push del navegador. | Plan estándar y superior. |
| WhatsApp | Mensaje al número registrado del usuario. | Plan premium. |
| SMS | Mensaje de texto. | Plan premium (alternativa a WhatsApp). |

## Catálogo de eventos notificables

| Evento | Canal(es) por defecto | Destinatarios |
| --- | --- | --- |
| Publicación de notas de un periodo | Portal + correo | Estudiante + acudiente |
| Registro de una inasistencia | Portal | Estudiante + acudiente |
| Disponibilidad de un nuevo boletín | Portal + correo | Estudiante + acudiente |
| Publicación de un comunicado | Portal + correo | Según alcance del comunicado |
| Publicación en agenda | Portal | Según alcance de la publicación |
| Publicación urgente en agenda | Portal + correo (inmediato) | Según alcance |
| Confirmación de un pago | Portal + correo | Estudiante + acudiente |
| Pago próximo a vencer | Portal + correo | Estudiante + acudiente |
| Pago vencido | Portal + correo | Estudiante + acudiente |
| Aprobación / rechazo de documento de matrícula | Portal + correo | Aspirante |
| Anotación en observador que requiere confirmación | Portal + correo | Estudiante + acudiente |
| Justificación de inasistencia aprobada / rechazada | Portal | Estudiante + acudiente |
| Citación a reunión | Portal + correo | Acudiente o destinatario |
| Asignación a un grupo (al matricular o al cambiar) | Portal + correo | Estudiante + acudiente |
| Bloqueo de cuenta por intentos fallidos | Correo | Usuario afectado |
| Cambio de contraseña | Correo | Usuario afectado |
| Acceso a datos por superadmin | Portal | Administrador del colegio |
| Cuota de almacenamiento al 80% / 100% | Portal + correo | Administrador del colegio |
| Backup completado / fallido | Portal | Administrador del colegio |

Cada tipo de notificación puede activarse o desactivarse por configuración del colegio.

## Preferencias del usuario

- Cada usuario puede ajustar sus preferencias de notificación por canal y por tipo de evento, dentro de los límites configurados por el colegio.
- Las notificaciones marcadas como **críticas** por la plataforma (ej. cambio de contraseña, bloqueo) no pueden desactivarse.

## Reglas de envío y throttling

- Las notificaciones por correo se envían en lotes para evitar saturar el buzón del usuario, excepto las marcadas como **urgentes** o **críticas**, que se envían inmediatamente.
- El sistema agrupa notificaciones similares dentro de una ventana de tiempo (ej. "3 nuevas notas publicadas en lugar de 3 correos separados").
- Las notificaciones push respetan los horarios de "no molestar" del usuario si están configurados.

## Plantillas de notificación

- Cada evento tiene una plantilla por canal.
- Las plantillas son personalizables por colegio dentro de límites: el colegio puede ajustar el saludo, el cierre y el cuerpo, pero no las variables dinámicas obligatorias.
- Las plantillas tienen variables: `{nombre_estudiante}`, `{periodo}`, `{materia}`, `{nota}`, `{fecha}`, `{enlace}`, etc.
- Para plantillas completamente personalizadas, aplica el mismo modelo de servicio que las plantillas de boletín.

## Reglas de negocio

- **RN-NO-001 — Eventos críticos no desactivables:** ciertos eventos (cambio de contraseña, bloqueo, acceso del superadmin) no pueden desactivarse.
- **RN-NO-002 — Urgencia salta throttling:** las notificaciones marcadas como urgentes se envían inmediatamente, sin agrupar.
- **RN-NO-003 — Configuración por colegio:** el colegio activa o desactiva eventos enteros y define los canales por defecto.
- **RN-NO-004 — Preferencias dentro de límites:** el usuario solo puede ajustar sus preferencias dentro de los canales habilitados por el colegio.
- **RN-NO-005 — Trazabilidad de envíos:** los envíos quedan registrados con destinatario, canal, fecha y resultado (entregado / fallido).

## Notas y pendientes

- **[Decisión tomada]** Ventanas de agrupamiento **configurables por colegio dentro de límites del sistema**:
  - **Correo electrónico:** agrupamiento entre **5 y 15 minutos** (default 10 min) para evitar saturación de la bandeja del usuario.
  - **Portal y push:** **entrega inmediata**, sin agrupamiento.
  Regla: **RN-NT-190 — Agrupamiento configurable por canal con tope del sistema**.
- **[Decisión tomada]** Comportamiento ante rebotes de correo:
  - **Rebote temporal (4xx):** reintentar conforme a la política del proveedor SMTP, sin suspender el canal.
  - **Rebote permanente (5xx) o 3 rebotes temporales consecutivos:** **suspender el canal correo** del usuario y **notificar al administrador del colegio** para corrección del email. El canal portal y push permanecen activos.
  Regla: **RN-NT-191 — Suspensión automática del canal correo tras rebotes y notificación al administrador, distinguiendo rebotes temporales y permanentes**.
