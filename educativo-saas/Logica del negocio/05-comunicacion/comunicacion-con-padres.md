---
titulo: Comunicación con padres / acudientes (operada vía usuario del estudiante)
modulo: comunicacion
tipo: proceso
estado: borrador
tags: [padres, acudientes, comunicacion]
---

# Comunicación con padres / acudientes

> **Aclaración estructural:** en esta plataforma **"acudiente" / "padre de familia" NO es un tipo de usuario propio**. El **estudiante** posee la única cuenta del menor y el acudiente la utiliza en la práctica (gestionar pagos, recibir comunicados, confirmar citaciones). Toda referencia a "acudiente" en este archivo se traduce operacionalmente a **"el usuario del estudiante"**. Ver `RN-TU-410` en [[../02-usuarios-roles-y-permisos/tipos-de-usuario|Tipos de usuario]].

## Descripción

Flujos específicos para mantener informado al **usuario del estudiante** (operado por el acudiente) sobre el desempeño, asistencia, comportamiento y obligaciones financieras del menor.

No es un canal nuevo: usa los mecanismos existentes ([[notificaciones|notificaciones]], [[circulares-y-comunicados|comunicados]], [[agenda-y-publicaciones|agenda]]) con segmentación hacia los usuarios estudiantes.

## Canales habilitados

- Portal del colegio (acceso desde la cuenta del estudiante; en la práctica accede el acudiente).
- Correo electrónico (registrado en la cuenta del estudiante; suele ser el del acudiente).
- WhatsApp (plan Premium).

## Eventos clave que se comunican

Por defecto el **usuario del estudiante** recibe notificaciones para los siguientes eventos:

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

- El docente, director de grupo o coordinación puede generar una **citación** dirigida al **usuario del estudiante**.
- La citación incluye: motivo, fecha, hora, lugar (físico o virtual), enlace de la reunión virtual si aplica.
- El usuario del estudiante recibe la notificación y puede **confirmar asistencia** desde el portal.
- El sistema registra la confirmación y la asistencia efectiva (registrada por el citante).

## Acuse de recibo

- Las comunicaciones que el colegio considere críticas pueden requerir **confirmación de lectura** desde la cuenta del estudiante.
- El acuse queda registrado con fecha, hora e IP.
- El sistema genera un reporte de comunicaciones sin acuse para seguimiento.

## Reglas de negocio

- **RN-CP-001 — Notificación al usuario del estudiante:** las comunicaciones dirigidas a la familia se entregan a la **cuenta del estudiante**, que es el único punto de acceso del menor.
- **RN-CP-002 — Acudiente con varios hijos:** si el mismo acudiente atiende a varios estudiantes, **opera la cuenta de cada estudiante por separado**. La plataforma puede ofrecer un **selector de estudiante** en el portal cuando un mismo correo esté vinculado a varias cuentas para facilitar la navegación, sin fusionar expedientes ni permisos.
- **RN-CP-003 — Eventos notificables configurables:** el colegio puede activar o desactivar la notificación automática para cada tipo de evento (alineado con `RN-CC-220`).
- **RN-CP-004 — Privacidad por estudiante:** desde la cuenta de un estudiante solo se ve la información de ese estudiante; nunca información de terceros.
- **RN-CP-005 — Citaciones registran asistencia:** las citaciones registran tanto la confirmación previa como la asistencia efectiva.

## Notas y pendientes

- **[Decisión tomada]** Modelo confirmado: **una cuenta por estudiante, sin rol acudiente como usuario**. Ver `RN-TU-410`.
- **[Decisión tomada]** El **reagendamiento de citas** desde el portal es **configurable por colegio**. Por defecto activado: el usuario solicita reagendar y el docente o coordinación confirma. Regla: **RN-CP-170 — Reagendamiento de citas configurable por colegio**.
- **[Pendiente — UX]** Selector multi-estudiante cuando un mismo correo de acudiente está vinculado a varias cuentas de estudiante. Definir si se ofrece como vista única de navegación o si se mantiene login independiente por cuenta.
