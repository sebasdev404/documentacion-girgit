---
titulo: Otras integraciones
modulo: integraciones-externas
tipo: referencia
estado: borrador
tags: [integraciones]
---

# Otras integraciones

## Catálogo

| Sistema | Propósito | Tipo | Disponibilidad |
| --- | --- | --- | --- |
| Facturación electrónica DIAN (Colombia) | Emisión de facturas electrónicas válidas. | API a través de proveedor tecnológico autorizado. | Plan estándar y premium (Colombia). |
| SSO Google Workspace | Inicio de sesión con cuenta Google del colegio. | OAuth 2.0 / OIDC. | Plan estándar y premium. |
| SSO Microsoft 365 | Inicio de sesión con cuenta Microsoft del colegio. | OAuth 2.0 / OIDC. | Plan estándar y premium. |
| Almacenamiento de archivos | Bucket por tenant para documentos. | Cliente S3-compatible. | Todos los planes (transparente). |
| Analytics interno | Análisis de uso de la plataforma. | Eventos al backend de la plataforma. | Solo equipo de plataforma. |
| WhatsApp Business API | Notificaciones por WhatsApp. | API. | Plan premium. |
| Software contable del colegio | Exportación de movimientos. | Archivo CSV / Excel con formato específico. | Bajo demanda. |
| LMS externo | Importación / exportación de calificaciones. | API o archivo. | Roadmap fase 2. |
| Sistema de control de acceso (puertas, comedor) | Sincronización de listas. | API o archivo. | Roadmap fase 2. |

## Configuración por tenant

- Cada integración se activa por colegio cuando aplica.
- Las credenciales se cifran en reposo y se acceden auditadamente.
- El acceso a logs y a estado de integración está disponible para el administrador del colegio.

## SSO (Google y Microsoft)

- El colegio configura el dominio aceptado para SSO (ej. `@micolegio.edu.co`).
- Los usuarios del dominio inician sesión sin contraseña propia en la plataforma.
- El primer ingreso crea o vincula la cuenta según correo.
- El SSO no anula el control de roles: la matriz de permisos sigue aplicando.

## Facturación electrónica

Ver detalle en [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]]. Aquí solo el aspecto de integración: la plataforma se conecta vía API al proveedor tecnológico DIAN, envía el XML, recibe el CUFE, almacena la representación gráfica.

## Reglas de negocio

- **RN-OI-001 — Activación por colegio:** las integraciones se activan tenant por tenant.
- **RN-OI-002 — Credenciales cifradas:** todas las credenciales de terceros se almacenan cifradas.
- **RN-OI-003 — SSO no sustituye permisos:** un usuario que entra por SSO sigue sometido a la matriz de permisos.
- **RN-OI-004 — Trazabilidad:** los intentos de integración (éxito y fracaso) quedan en el log.
- **RN-OI-005 — Aislamiento entre tenants:** una integración configurada por un colegio no expone datos de otro.

## Notas y pendientes

- **[Decisión tomada]** **Sin integraciones con LMS externos** en el roadmap actual. Las futuras funcionalidades académicas o virtuales se contemplan como **módulos nativos** desarrollados dentro del ecosistema de la aplicación, evitando dependencias de plataformas externas. Regla: **RN-OI-340 — LMS y aula virtual como módulos nativos, no integraciones externas**.
- **[Decisión externa pendiente — Comercial]** Selección del **proveedor tecnológico DIAN** para Colombia (mismo pendiente referenciado en `facturacion-y-recibos.md`). El diseño queda en abstracto para no acoplar la decisión.
