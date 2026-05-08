---
titulo: Gestión documental
modulo: 11-plataforma-y-operacion
tipo: proceso
estado: borrador
tags: [documentos, gestion-documental, plantillas, certificados]
---

# Gestión documental

## Descripción

Capacidad de la plataforma para **crear, almacenar, versionar, firmar y emitir** los documentos que el colegio gestiona en su operación. La gestión documental NO es un módulo aislado: se transversaliza al resto del sistema (matrícula, boletín, paz y salvo, certificados, observador, comunicados).

## Tipos de documentos

| Categoría | Ejemplos |
| --- | --- |
| Documentos de admisión / matrícula | Identificación, registro civil, certificados, tipo de sangre, fotos. |
| Documentos académicos | Boletines, certificados de notas, certificados de estudio, planes de mejoramiento. |
| Documentos financieros | Recibos, facturas, notas crédito, paz y salvo. |
| Documentos administrativos | Pagaré, contrato de matrícula, autorizaciones. |
| Documentos disciplinarios / observador | Anotaciones firmadas, compromisos. |
| Comunicaciones | Comunicados, citaciones, circulares. |
| Plantillas | Hoja membretada, firma escaneada, logos. |

## Plantillas y personalización

- Cada colegio configura sus **plantillas** para los documentos que la plataforma emite (boletines, certificados, paz y salvo, recibos).
- Las plantillas usan **variables dinámicas**: nombre del estudiante, periodo, notas, etc.
- Personalización limitada en el plan estándar (encabezado, pie, logo).
- Personalización total como **servicio profesional** o plan premium (ver [[../04-procesos-academicos/boletines-y-reportes-academicos|Boletines]]).

## Versionado

- Cada plantilla y cada documento emitido se versiona.
- Una nueva versión no afecta documentos ya emitidos.
- Para reimprimir un documento histórico, el sistema usa la versión vigente en el momento de su emisión.

## Firmado

| Modalidad | Descripción |
| --- | --- |
| Firma escaneada en plantilla | Imagen de la firma del rector / secretaria embebida en la plantilla. |
| Firma electrónica simple | Casilla de aceptación con timestamp e IP. |
| Firma electrónica avanzada | Integración con proveedor externo (fase 2). |

## Subida y almacenamiento

- Los documentos cargados por usuarios (matrícula, soportes) se guardan en el bucket del tenant (ver [[almacenamiento-y-cuotas|Almacenamiento y cuotas]]).
- Cada documento queda asociado al recurso de origen (estudiante, pago, observador).
- Antivirus obligatorio.
- Limpieza automática de versiones obsoletas tras retención configurada.

## Búsqueda y consulta

- Búsqueda por estudiante, tipo de documento, año, estado.
- Vista consolidada por estudiante: \"carpeta del estudiante\".
- Filtros por documentos pendientes, vencidos, firmados.

## Documentos requeridos

- El colegio define la lista de documentos requeridos por nivel / grado / proceso.
- El sistema valida la lista al matricular y bloquea procesos cuando faltan documentos críticos.
- Notifica al acudiente los documentos pendientes.

## Reglas de negocio

- **RN-GD-001 — Plantilla versionada:** una nueva plantilla no afecta documentos emitidos previamente.
- **RN-GD-002 — Documento asociado a recurso:** todo documento queda asociado al recurso del que es soporte.
- **RN-GD-003 — Antivirus obligatorio:** los archivos cargados pasan por análisis antes de quedar disponibles.
- **RN-GD-004 — Documento emitido inmutable:** un documento ya emitido no se edita; cualquier ajuste va por reemisión con motivo.
- **RN-GD-005 — Documentos requeridos validados:** la falta de documentos críticos bloquea procesos sensibles (matrícula, boletín final, paz y salvo).
- **RN-GD-006 — Auditoría de descarga:** las descargas de documentos sensibles se registran en el log.

## Notas y pendientes

- Definir si la firma electrónica avanzada se contrata en fase 1 o queda para fase 2.
- Definir el flujo de \"documento vencido\" (ej. certificado de afiliación EPS) y su renovación periódica.
