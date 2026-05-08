---
titulo: Comunicación con padres
modulo: comunicacion
tipo: proceso
estado: borrador
tags: [padres, acudientes, comunicacion]
---

# Comunicación con padres

## Descripción

Flujos específicos para mantener informados a los acudientes sobre el desempeño, asistencia, comportamiento y obligaciones financieras de los estudiantes a su cargo.

No es un canal nuevo: usa los mecanismos existentes ([[notificaciones|notificaciones]], [[circulares-y-comunicados|comunicados]], [[agenda-y-publicaciones|agenda]]) con segmentación hacia acudientes.

## Canales habilitados

- Portal del colegio (acceso del acudiente).
- Correo electrónico.
- WhatsApp (plan premium).

## Eventos clave que se comunican

Por defecto el acudiente recibe notificaciones para los siguientes eventos del estudiante a su cargo:

| Evento | Canal default |
| --- | --- |
| Publicación de notas de un periodo | Portal + correo |
| Registro de una inasistencia | Portal + correo (configurable) |
| Disponibilidad de un nuevo boletín | Portal + correo |
| Anotación disciplinaria que requiere confirmación | Portal + correo |
| Confirmación de un pago | Portal + correo |
| Pago de pensión próximo a vencer | Portal + correo |
| Pago vencido | Portal + correo |
| Aprobación / rechazo de un documento de matrícula | Portal + correo |
| Citación a reunión | Portal + correo |

## Citaciones y reuniones

- El docente, director de grupo o coordinación puede generar una **citación** dirigida al acudiente.
- La citación incluye: motivo, fecha, hora, lugar (físico o virtual), enlace de la reunión virtual si aplica.
- El acudiente recibe la notificación y puede confirmar asistencia desde el portal.
- El sistema registra la confirmación del acudiente y la asistencia efectiva (registrada por el citante).

## Acuse de recibo

- Las comunicaciones que el colegio considere críticas pueden requerir confirmación de lectura por parte del acudiente.
- El acuse queda registrado con fecha, hora e IP.
- El sistema genera un reporte de comunicaciones sin acuse para seguimiento.

## Reglas de negocio

- **RN-CP-001 — Acudiente vinculado al estudiante:** las comunicaciones a acudientes se enrutan a las cuentas vinculadas al estudiante en el sistema.
- **RN-CP-002 — Acudiente con varios estudiantes:** un acudiente con varios hijos en el colegio recibe las comunicaciones de cada uno; en el portal puede ver consolidado o por estudiante.
- **RN-CP-003 — Eventos notificables configurables:** el colegio puede activar o desactivar la notificación automática para cada tipo de evento.
- **RN-CP-004 — Privacidad entre acudientes:** un acudiente solo ve la información del estudiante o estudiantes que tiene vinculados, nunca de otros estudiantes.
- **RN-CP-005 — Citaciones registran asistencia:** las citaciones registran tanto la confirmación previa del acudiente como la asistencia efectiva.

## Notas y pendientes

- Validar el flujo de "acudiente principal" cuando hay varios acudientes registrados (quién recibe primero, quién debe confirmar).
- Definir si las citaciones permiten reagendamiento desde el portal del acudiente.
