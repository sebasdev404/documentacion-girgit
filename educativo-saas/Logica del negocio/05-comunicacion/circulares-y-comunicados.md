---
titulo: Circulares y comunicados
modulo: comunicacion
tipo: proceso
estado: borrador
tags: [circulares, comunicados]
---

# Circulares y comunicados

## Descripción

Mecanismo de comunicación institucional dirigido a segmentos específicos de usuarios. Se diferencia de la [[agenda-y-publicaciones|agenda]] en que los comunicados son típicamente más formales, suelen exigir confirmación de lectura y se envían también por correo electrónico.

## Quién puede emitir

Por defecto, solo los roles administrativos del colegio:

- [[roles/01-rector-administrador-colegio\|Administrador / Rector]]
- [[roles/02-coordinador-academico\|Coordinador Académico]]
- [[roles/03-coordinador-convivencia\|Coordinador de Convivencia]]
- [[roles/05-secretaria-academica\|Secretaría Académica]]

El colegio puede ampliar o restringir esta lista en su configuración.

## Audiencias

Un comunicado se dirige a un alcance específico:

| Alcance | Descripción |
| --- | --- |
| Toda la institución | Todos los estudiantes y/o docentes del colegio. |
| Sede | Solo los usuarios de una sede específica. |
| Nivel educativo | Preescolar, Primaria, Secundaria, Media. |
| Grado | Un grado completo (todos los grupos del grado). |
| Grupo | Un grupo específico. |
| Individual | Un estudiante / acudiente específico. |
| Docentes | Solo los docentes (puede combinarse con sede o nivel). |

## Confirmación de lectura

- El emisor puede marcar el comunicado como **"requiere confirmación de lectura"**.
- Los destinatarios deben confirmar al leer el comunicado desde el portal.
- El sistema lleva el reporte de confirmaciones: quién confirmó y quién no.
- Las confirmaciones se registran con fecha, hora e IP.

## Adjuntos

- Un comunicado puede llevar archivos adjuntos (PDF, imágenes, documentos).
- Los adjuntos consumen cuota de almacenamiento del tenant.
- El sistema valida tamaño máximo por archivo y por comunicado.

## Canales de envío

- **Portal del colegio:** siempre.
- **Correo electrónico:** opcional. El emisor decide si se envía copia por correo.
- **WhatsApp:** disponible en plan premium.

## Estados y transiciones

```
Borrador → Programado (con fecha de envío) → Enviado
                                            → Cancelado (antes del envío)
```

## Reglas de negocio

- **RN-CC-COM-001 — Permisos de emisión configurables:** los roles que pueden emitir comunicados se configuran por colegio.
- **RN-CC-COM-002 — Alcance respeta segmentación:** un comunicado solo es visible para los usuarios dentro del alcance configurado.
- **RN-CC-COM-003 — Confirmación auditada:** las confirmaciones de lectura registran fecha, hora e IP.
- **RN-CC-COM-004 — Adjuntos consumen cuota:** los adjuntos suman al uso de almacenamiento del tenant.
- **RN-CC-COM-005 — Eliminación preserva historial:** los comunicados eliminados quedan archivados, no se borran físicamente. La trazabilidad institucional se preserva.
- **RN-CC-COM-006 — Programación cancelable:** un comunicado programado puede cancelarse antes de su envío.

## Notas y pendientes

- **[Decisión tomada]** Límites de adjuntos en comunicados: **20 MB por adjunto** y **50 MB totales** por comunicado. Mismos límites en publicaciones de agenda. Regla: **RN-CC-160 — Límite 20MB/adjunto y 50MB/total por comunicado**.
- **[Decisión tomada]** El sistema soporta **plantillas reutilizables de comunicados** por colegio desde el lanzamiento (encabezado, cuerpo con variables `{{nombre_estudiante}}`, `{{grupo}}`, etc., y configuración de destinatarios por defecto). Regla: **RN-CC-161 — Plantillas reutilizables por colegio**.
