---
titulo: Almacenamiento y cuotas
modulo: 11-plataforma-y-operacion
tipo: regla
estado: borrador
tags: [almacenamiento, cuotas, archivos, storage]
---

# Almacenamiento y cuotas

## Descripción

La plataforma asigna a cada colegio (tenant) un **bucket separado** para almacenar archivos: documentos de matrícula, soportes de pago, plantillas de boletines, adjuntos de comunicados / publicaciones, fotos, evidencias de comportamiento, etc.

Cada plan incluye una cuota base; el exceso se factura aparte.

## Tipos de archivos almacenados

| Categoría | Ejemplos |
| --- | --- |
| Documentos de matrícula | PDF de identificación, registro civil, certificados. |
| Soportes de pago | Comprobantes de consignación. |
| Adjuntos de boletines | PDFs generados / firmados. |
| Adjuntos de comunicados / agenda | Imágenes, vídeos, PDF, etc. |
| Plantillas | Plantillas Word / HTML de boletines, certificados. |
| Evidencias del observador | Fotos, audios, PDFs de soporte. |
| Logo y branding | Logo, hoja membretada, firma escaneada. |

## Cuotas por plan (referencia)

| Plan | Cuota incluida |
| --- | --- |
| Esencial | 50 GB. |
| Estándar | 200 GB. |
| Premium | 1 TB. |

Los valores exactos se mantienen en la matriz comercial.

## Validaciones por archivo

| Validación | Descripción |
| --- | --- |
| Tamaño máximo individual | Configurado por tipo (ej. 10 MB para imágenes, 25 MB para vídeos, 5 MB para documentos). |
| Tipo MIME permitido | Whitelist por tipo (no se aceptan ejecutables). |
| Antivirus | Análisis al subir; archivos infectados se rechazan. |
| Nombre seguro | Renombrado interno con identificador único; el nombre original se conserva para mostrar. |

## Política cuando se supera la cuota

| Umbral | Acción |
| --- | --- |
| 80% | Notificación al administrador del colegio. |
| 95% | Notificación urgente + sugerencia de plan superior o ampliación. |
| 100% | Bloqueo de nuevas subidas. La plataforma sigue operando en lectura, pero no acepta nuevos archivos hasta liberar espacio o ampliar la cuota. |

Las funcionalidades críticas (matrícula, boletín final) avisan al usuario que no puede adjuntar y orientan a contactar al administrador.

## Limpieza y optimización

- Archivos temporales (ej. PDF de boletín regenerable) tienen TTL.
- El sistema ofrece al administrador un panel de **archivos huérfanos** (asociados a registros eliminados) para revisarlos.
- Archivos de tenants finalizados se eliminan tras la ventana de retención (ver [[../03-multi-tenancy/modelo-de-tenants|Modelo de tenants]]).

## Acceso a los archivos

- URLs firmadas y de corta vigencia para descarga.
- No hay URLs públicas permanentes a archivos del tenant.
- Cada acceso queda en el [[log-de-auditoria|log]] cuando el archivo es sensible (documento de identidad, soportes financieros).

## Reglas de negocio

- **RN-AC-001 — Bucket por tenant:** un colegio no puede acceder al bucket de otro.
- **RN-AC-002 — Antivirus obligatorio:** todo archivo se analiza antes de quedar disponible.
- **RN-AC-003 — Whitelist de tipos:** solo se aceptan tipos en la whitelist; tipos peligrosos se rechazan.
- **RN-AC-004 — URLs firmadas:** la descarga usa URLs firmadas con expiración corta.
- **RN-AC-005 — Bloqueo al 100%:** al superarse la cuota, no se permiten nuevas subidas; lectura sigue disponible.
- **RN-AC-006 — Notificación temprana:** al alcanzar el 80% se notifica al administrador del colegio.

## Notas y pendientes

- **[Decisión tomada]** **Tamaños máximos por tipo de archivo configurables por plan** (Esencial / Estándar / Premium), con valores base por tipo: documentos, imágenes, video y audio. Las cuotas se ajustan para controlar costos de almacenamiento, rendimiento y experiencia de usuario. Los valores específicos por plan quedan en discusión hasta confirmar costos del proveedor. Regla: **RN-AC-250 — Tamaños máximos por tipo y por plan**.
- **[Decisión tomada]** **Política de retención y borrado físico**:
  - **Soft-delete** con marca y periodo de **cuarentena** antes del borrado físico definitivo.
  - Antes de ejecutar **purgas definitivas**, el sistema **notifica a los superadministradores de plataforma** para permitir validaciones, respaldos adicionales o recuperaciones manuales.
  - **Archivos huérfanos** o sin referencias activas se **purgan periódicamente** (ej. trimestralmente) para optimizar almacenamiento y costos.
  Regla: **RN-AC-251 — Soft-delete + cuarentena + notificación al superadmin antes de purga + purga periódica de huérfanos**.
