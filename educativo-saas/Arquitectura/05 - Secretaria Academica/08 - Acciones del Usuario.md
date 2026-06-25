---
tags:
  - arquitectura
  - rol/secretaria-academica
  - acciones
aliases:
  - Acciones ROL-06
  - Secretaria Acciones
---

# Acciones del Usuario — Secretaria Academica

Tabla accion -> resultado. Cada accion sensible (matricula, emision de documentos, reporte SIMAT) genera entrada en el log de auditoria del tenant (RR-03).

| Accion | Resultado |
|---|---|
| Click en "Crear estudiante" y completa la ficha | Sistema valida datos (documento unico en el tenant) · crea la ficha · vincula datos de acudiente operativo como contacto (RR-11) · registra en log |
| Edita datos del acudiente operativo | Sistema actualiza el contacto dentro de la ficha del estudiante · no crea usuario (`RN-TU-410`) · registra en log |
| Adjunta consentimiento de habeas data y lo marca firmado | Sistema guarda el consentimiento con fecha · habilita el tratamiento de datos del menor (`RN-HD-001`) · registra en log |
| Carga un documento de matricula y lo marca recibido | Sistema actualiza el checklist del estudiante · recalcula pendientes · si quedan 0 pendientes habilita la matricula · registra en log |
| Marca un documento como pendiente | Sistema lo suma a pendientes · alimenta el bloqueo configurable de emision (RR-08) · registra en log |
| Click en "Asignar a grupo" | Sistema valida cupo del grupo · asigna el estudiante · marca matricula en proceso/completada · registra en log |
| Cambia el grupo despues de matriculado | Si el permiso esta activado: reasigna y registra en log · si esta restringido (RR-05): bloquea y sugiere al Coordinador Academico |
| Click en "Generar constancia de estudio" | Sistema valida pendientes (RR-08) · asigna consecutivo unico (`RN-GD-001`) · genera PDF con trazabilidad · registra en log |
| Click en "Generar certificado de notas" | Sistema lee el consolidado de notas en solo lectura · valida pendientes · asigna consecutivo · genera PDF · registra en log |
| Click en "Emitir paz y salvo" | Sistema consulta estado de cartera (si integra) · si hay pendientes y el bloqueo esta activo: impide la emision (`RN-PZ-002`) · si no: emite con consecutivo · registra en log |
| Reimprime / descarga un documento ya emitido | Sistema reusa el consecutivo original · genera copia con marca de reimpresion · registra en log |
| Click en "Generar archivo SIMAT" | Sistema arma el archivo en el formato del MEN con las novedades del periodo (`RN-MO-001`) · corre validacion previa · muestra errores si los hay |
| Click en "Validar antes de exportar" (SIMAT) | Sistema verifica consistencia de los datos (`RN-MO-004`) · lista registros con problemas · no exporta hasta corregirlos |
| Descarga el archivo SIMAT y lo marca como enviado | Sistema genera el archivo · registra fecha de envio · deja el reporte trazable · registra en log |
| Registra una revocatoria de consentimiento | Sistema marca el consentimiento como revocado · respeta la revocatoria en el tratamiento de datos (`RN-HD-006`) · registra en log |
| Envia mensaje al acudiente (si esta activado) | Sistema entrega el mensaje al contacto del estudiante via portal/correo · registra en log |
| Consulta el historial de un registro (si esta activado) | Sistema muestra quien cambio que y cuando (solo lectura) · la consulta no altera el log (RR-03) |
| Cierra sesion | Sistema invalida el token · registra logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
