---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
  - acciones
aliases:
  - Acciones ROL-09
  - Estudiante y Acudiente Acciones
---

# Acciones del Usuario — Estudiante / Acudiente

Tabla accion -> resultado. Toda interaccion del estudiante/acudiente (justificacion, confirmacion, pago, solicitud) queda registrada en el log del tenant (RR-03, RN-PE-004).

| Accion | Resultado |
|---|---|
| Inicia sesion por el subdominio del colegio | Sistema infiere el tenant del subdominio (RR-06) · valida credenciales · si el portal esta desactivado muestra "Portal no habilitado" (RN-PE-001) · si es primer ingreso fuerza cambio de contrasena (RN-AU-360) · registra el acceso en log |
| Selecciona un estudiante en el selector (varios hijos) | Sistema cambia el contexto completo de la sesion al estudiante elegido · no fusiona datos de hermanos (RR-14, RN-CP-002) |
| Abre "Notas" y filtra por periodo/materia | Sistema muestra solo las notas del estudiante en contexto (RF-45) · no permite editar (RN-PE-002) |
| Abre "Horario" | Sistema muestra el horario semanal del grupo del estudiante (RF-46) |
| Justifica una inasistencia (adjunta motivo/soporte) | Sistema crea la justificacion en estado Pendiente (RN-PE-005) · notifica al docente/coordinador · NO cambia el estado de la inasistencia hasta que sea revisada · registra en log |
| Confirma un boletin digitalmente | Sistema registra la confirmacion con fecha, hora e IP asociada al usuario (RN-PE-004) · marca el boletin como confirmado · registra en log |
| Pulsa "Descargar boletin PDF" | Sistema verifica paz y salvo/pago (RN-PE-003, RN-PE-006) · si esta al dia genera el PDF · si hay bloqueo muestra el detalle de lo pendiente y no descarga |
| Abre el "Observador" (si esta habilitado) | Sistema muestra las anotaciones del estudiante en solo lectura (RF-48, RN-OB-080) · si el colegio no lo expone, el modulo no aparece (RN-OB-081) |
| Confirma una anotacion del observador que lo requiere | Sistema registra la confirmacion con fecha · actualiza el estado de la anotacion a Confirmada · registra en log |
| Lee un comunicado / lo marca como leido | Sistema registra la lectura · actualiza el contador de no leidos |
| Escribe un mensaje a un docente (si el canal esta habilitado) | Sistema envia por el canal formal (RN-MI-180) · notifica al docente · si el canal esta restringido, la accion no esta disponible |
| Pulsa "Pagar" una cuota y completa el pago en la pasarela | Sistema redirige a la pasarela habilitada · al recibir el webhook confirma el pago (RN-PP-003) · marca la cuota como Pagada · emite comprobante (RN-PP-006) · notifica · registra con transactionId (RN-PP-001) |
| Descarga el comprobante de un pago | Sistema genera el comprobante del pago confirmado · registra la descarga |
| Carga un documento requerido de matricula | Sistema guarda el documento en estado En revision (RN-GD-270) · notifica a Secretaria · al resolverse notifica aprobado/rechazado al usuario |
| Solicita una constancia/certificado/paz y salvo | Sistema valida paz y salvo y pago del costo si aplica (RN-PE-006, RN-PYS-150) · si procede genera el documento con QR (RN-PZ-004) · si hay deuda principal no genera ni siquiera el cargo del certificado (RN-PYS-150) |
| Solicita una cita con docente/coordinacion | Sistema crea la solicitud en estado Solicitada · notifica al destinatario · al confirmarse/reprogramarse notifica al estudiante/acudiente |
| Ajusta preferencias de notificacion | Sistema guarda las preferencias dentro de los limites del colegio (RN-NO-004) · no permite desactivar eventos criticos (RN-NO-001) |
| Cambia su contrasena | Sistema valida la contrasena nueva · invalida sesiones previas · notifica al correo (RN-NO-001) · registra en log |
| Intenta editar una nota/asistencia/observador (via UI o llamada directa) | Sistema bloquea en backend (RN-PE-002, RR-02) · no aplica cambio · registra el intento en log de seguridad |
| Cierra sesion | Sistema invalida el token · registra logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[09 - Campos del Formulario]] — campos de cada accion con formulario
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
