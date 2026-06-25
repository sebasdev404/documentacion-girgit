---
tags:
  - arquitectura
  - rol/secretaria-academica
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-06
  - Secretaria Respuestas
---

# Respuestas del Sistema — Secretaria Academica

Que responde el sistema ante cada evento.

| Evento | Respuesta del Sistema |
|---|---|
| Secretaria crea un estudiante | Crea la ficha · vincula los datos del acudiente operativo como contacto (RR-11) · inicializa el checklist de documentos del grado · registra en log del tenant |
| Adjunta y firma el consentimiento de habeas data | Marca el consentimiento como firmado · habilita el tratamiento de datos del menor (`RN-HD-001`) · registra en log |
| Registra una revocatoria de consentimiento | Marca el consentimiento como revocado · aplica la restriccion al tratamiento de datos (`RN-HD-006`) · notifica al Rector si la normativa del colegio lo exige · registra en log |
| Carga un documento de matricula y lo marca recibido | Actualiza el checklist · recalcula pendientes · si llega a 0 pendientes habilita la matricula · registra en log |
| Asigna un estudiante a un grupo | Valida cupo · ocupa una plaza del grupo · cambia estado a Matriculado · notifica al acudiente (si las comunicaciones estan activas) · registra en log |
| Cambia el grupo despues de matriculado | Si esta permitido: reasigna y libera el cupo anterior · registra en log · si esta restringido: rechaza y sugiere al Coordinador Academico (RR-05) |
| Genera una constancia de estudio | Valida pendientes (RR-08) · asigna consecutivo unico (`RN-GD-001`) · genera el PDF con trazabilidad (quien, cuando, consecutivo) · registra en log |
| Genera un certificado de notas | Lee el consolidado de notas en solo lectura · valida pendientes · asigna consecutivo · genera el PDF · registra en log |
| Emite un paz y salvo | Consulta cartera (si integra) · si hay pendientes y el bloqueo esta activo: impide la emision y muestra el motivo (`RN-PZ-002`) · si no: emite con consecutivo · registra en log |
| Emision bloqueada por pendientes | No genera documento · muestra el detalle de los pendientes · registra el intento en log (RR-08) |
| Reimprime un documento ya emitido | Reusa el consecutivo original · genera copia con marca de reimpresion y fecha · registra en log |
| Genera el archivo SIMAT | Arma el archivo en el formato del MEN con las novedades del periodo (`RN-MO-001`) · corre la validacion previa · si hay errores los lista y no exporta (`RN-MO-004`) |
| Marca el reporte SIMAT como enviado | Registra fecha de envio · deja el reporte trazable en el historial · registra en log |
| Documento de matricula vence | Genera notificacion en el inicio · si las comunicaciones estan activas, dispara aviso al acudiente · marca el documento como vencido |
| Envia mensaje al acudiente (si esta activado) | Entrega el mensaje al contacto del estudiante via portal/correo · registra en log |
| Consulta el historial de un registro (si esta activado) | Devuelve quien cambio que y cuando (solo lectura) · no altera el log de auditoria (RR-03) |
| Intento de accion sin permiso (notas, observador, configuracion) | Rechaza en frontend y backend · muestra "No tiene permisos para esta accion" · registra el intento en log de seguridad (RR-02) |
| Login fallido de la secretaria | Mensaje generico (no revela si el usuario existe) · incrementa contador de intentos · registra en log de seguridad |
| El Rector cambia un permiso configurable de la secretaria | Aplica el cambio en la siguiente sesion · muestra/oculta los modulos afectados (comunicaciones, historial, bloqueos) (RR-05) |
| Tenant suspendido por el Superadmin | Bloquea el acceso · muestra "colegio suspendido" · no permite operar |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/13-cumplimiento-colombia/reportes-oficiales-men.md` (SIMAT) y `Logica del negocio/11-plataforma-y-operacion/gestion-documental.md` (consecutivos)
