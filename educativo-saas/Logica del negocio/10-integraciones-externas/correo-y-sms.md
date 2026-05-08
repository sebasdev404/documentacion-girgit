---
titulo: Correo y SMS
modulo: integraciones-externas
tipo: referencia
estado: borrador
tags: [integraciones, correo, sms, mensajeria]
---

# Correo y SMS

## Proveedores integrados

| Proveedor | Canal | Uso | Notas |
| --- | --- | --- | --- |
| Proveedor SMTP transaccional (ej. SendGrid, Amazon SES) | Correo | Notificaciones, comunicados, envíos masivos. | Configuración a nivel plataforma; el colegio no maneja credenciales. |
| Proveedor SMS / WhatsApp Business API | SMS / WhatsApp | Notificaciones críticas, recordatorios de pago. | Disponible en plan premium. |

Las decisiones de proveedores específicos son operativas y pueden cambiar; lo relevante son los principios.

## Configuración por tenant

- Por defecto, los envíos salen del dominio de la plataforma con el branding del colegio ("Colegio X via plataforma").
- Plan premium: el colegio puede usar su propio dominio de correo (verificación SPF / DKIM).
- WhatsApp se activa por colegio con la verificación de su número comercial.

## Plantillas y variables

- Cada tipo de notificación tiene plantilla por canal con variables (`{nombre_estudiante}`, `{periodo}`, etc.).
- El colegio personaliza saludo, cierre y firma; las variables obligatorias no se modifican.
- Las plantillas se versionan para garantizar reproducibilidad de mensajes históricos.

## Eventos disparadores

Ver catálogo en [[../05-comunicacion/notificaciones|Notificaciones]].

## Manejo de bounces y reintentos

- **Bounce blando:** reintento automático hasta 3 veces.
- **Bounce duro:** se marca el correo como inválido y se notifica al administrador del colegio.
- Si un usuario recibe demasiados bounces seguidos, su canal de correo se suspende y debe actualizar la dirección.
- Los SMS / WhatsApp fallidos se reportan al administrador para validación manual del número.

## Cumplimiento

- Cabeceras de "unsubscribe" cuando aplique (correo institucional vs comercial).
- Respeto a horarios para canales no urgentes (no enviar SMS a las 3 a.m. salvo críticos).
- Auditoría de envíos en el [[../11-plataforma-y-operacion/log-de-auditoria|log]].

## Reglas de negocio

- **RN-CS-001 — Plantillas versionadas:** cada plantilla mantiene historial de versiones.
- **RN-CS-002 — Suspensión por bounce:** un correo con bounces repetidos se suspende.
- **RN-CS-003 — SMS / WhatsApp solo en premium:** estos canales requieren plan premium.
- **RN-CS-004 — Trazabilidad de envíos:** todo envío queda con destinatario, canal, fecha y resultado.

## Notas y pendientes

- **[Pendiente — comercial]** Costos asociados a **WhatsApp Business** quedan como **definición comercial futura**. La plataforma podrá contemplar límites, consumo incluido por plan o cobro adicional por uso según el proveedor seleccionado. La **arquitectura ya queda preparada** para soportar el canal.
- **[Decisión tomada]** **Tiempos de entrega por canal**: durante las etapas iniciales la plataforma opera bajo esquema **"best effort"**. La definición de **SLAs formales** queda sujeta a futuras decisiones de infraestructura, volumen y acuerdos con proveedores externos. Regla: **RN-CS-330 — Best effort por canal en fase 1; SLA formal en fase posterior**.
