---
titulo: "CU-012: Publicar comunicado institucional"
modulo: 05-comunicacion
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, comunicado, rector]
---

# CU-012: Publicar comunicado institucional

## Identificación

- **ID:** CU-012
- **Nombre:** Publicar comunicado institucional
- **Módulo:** Comunicación
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rector / Administrador del Colegio]] o secretaría.
- **Secundarios:** Audiencia (estudiantes / acudientes / docentes).

## Descripción

Emisión de un comunicado dirigido a un alcance específico, con o sin requerimiento de confirmación de lectura.

## Precondiciones

- Autor con permiso de emisión configurado.

## Postcondiciones (éxito)

- Comunicado en estado **Enviado** y visible para la audiencia.
- Notificaciones enviadas por los canales configurados.

## Flujo principal

1. Autor entra y crea un nuevo comunicado.
2. Llena título, cuerpo, alcance, audiencia.
3. Adjunta archivos si aplica.
4. Marca si requiere confirmación de lectura.
5. Programa fecha de envío o envía inmediato.
6. Sistema valida cuota de almacenamiento y antivirus en adjuntos.
7. Sistema envía y notifica.

## Flujos alternativos

### A1. Programado

- El comunicado se envía en la fecha programada; antes puede cancelarse.

### A2. Comunicado urgente

- Salta el throttling de notificaciones y se envía inmediato a todos los canales activos.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Cuota agotada. | Sistema bloquea y orienta. |
| EX-2 | Adjunto infectado. | Sistema rechaza el archivo. |
| EX-3 | Alcance no permitido para el rol. | Sistema bloquea con mensaje claro. |

## Reglas de negocio aplicables

- RN-CC-COM-001..006, RN-AC-002, RG-002.

## Criterios de aceptación

- [ ] El alcance se respeta: solo los usuarios dentro del alcance lo reciben.
- [ ] La confirmación de lectura queda registrada cuando se exige.
- [ ] El log de auditoría registra el envío y los destinatarios.

## Notas y pendientes

- Validar plantillas reutilizables para comunicados frecuentes.
