---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-09
  - Estudiante y Acudiente Respuestas
---

# Respuestas del Sistema — Estudiante / Acudiente

Que responde el sistema ante cada evento. Las notificaciones que llegan al portal/correo de este rol se rigen por `Logica del negocio/05-comunicacion/notificaciones.md`.

| Evento | Respuesta del Sistema |
|---|---|
| Estudiante/acudiente inicia sesion | Infiere el tenant del subdominio (RR-06) · valida credenciales · si hay varios estudiantes pide seleccionar · registra el acceso en log |
| Selecciona un estudiante (varios hijos) | Carga el contexto del estudiante elegido · no fusiona datos de hermanos (RR-14, RN-CP-002) |
| El colegio publica notas de un periodo | Habilita la consulta en Notas · envia notificacion al portal y correo del estudiante + acudiente · agrupa si hay varias notas (RN-NT-190) |
| Registra una justificacion de inasistencia | Crea la justificacion en estado Pendiente (RN-PE-005) · notifica al docente/coordinador para revision · deja la inasistencia sin cambiar hasta el fallo |
| El docente aprueba/rechaza la justificacion | Actualiza el estado de la inasistencia (justificada o se mantiene) · notifica al estudiante + acudiente el resultado |
| Confirma un boletin | Registra la confirmacion con fecha, hora e IP asociadas al usuario (RN-PE-004) · marca el boletin como confirmado |
| Solicita descargar un boletin/certificado | Verifica paz y salvo y pago previo (RN-PE-003, RN-PE-006, RN-PYS-150) · si esta al dia genera el PDF (con QR cuando aplica, RN-PZ-004) · si hay pendientes muestra el detalle y no descarga |
| El colegio publica un boletin | Habilita el boletin en el modulo · notifica al portal y correo (estudiante + acudiente) |
| Inicia un pago en la pasarela | Redirige a la pasarela habilitada · deja la cuota En proceso · espera el webhook |
| Llega el webhook de pago confirmado | Marca la cuota como Pagada (RN-PP-003) · emite el comprobante (RN-PP-006) · notifica la confirmacion · registra con transactionId (RN-PP-001) |
| Llega el webhook de pago rechazado | Devuelve la cuota a Pendiente · notifica el rechazo · no genera comprobante |
| Cuota proxima a vencer / vencida | Genera notificacion al portal y correo (estudiante + acudiente) · marca el estado de la cuota |
| Carga un documento requerido | Guarda en estado En revision (RN-GD-270) · notifica a Secretaria |
| Secretaria aprueba/rechaza un documento | Actualiza el estado del documento · notifica al estudiante/acudiente el resultado (y el motivo si fue rechazo) |
| Solicita un documento oficial cobrable con deuda principal | No genera el cargo del certificado mientras exista deuda (RN-PYS-150) · informa que debe ponerse al dia primero |
| Solicita una cita | Crea la solicitud (estado Solicitada) · notifica al destinatario · al confirmarse/reprogramarse notifica al estudiante/acudiente |
| Se registra una anotacion en el observador que requiere confirmacion | Notifica al portal y correo (estudiante + acudiente) · deja la anotacion Pendiente de confirmacion hasta que el acudiente la confirme |
| El colegio publica un comunicado con alcance al estudiante | Lo muestra en Comunicaciones · notifica segun el alcance (institucion/nivel/grado/grupo/materia) |
| Cambia su contrasena | Actualiza la credencial · invalida sesiones previas · notifica al correo (evento critico, RN-NO-001) |
| Intenta editar nota/asistencia/observador (UI o llamada directa) | Rechaza la operacion en backend (RN-PE-002, RR-02) · no aplica cambio · registra el intento en log de seguridad |
| Intenta acceder a datos de otro estudiante | Rechaza por scope (RR-14, RR-01) · no devuelve datos · registra el intento |
| Rebote permanente del correo del usuario | Suspende el canal correo · mantiene portal y push activos · notifica al administrador del colegio (RN-NT-191) |
| Cierra sesion | Invalida el token · registra el logout en log |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/05-comunicacion/notificaciones.md`
- Fuente: `Logica del negocio/02-usuarios-roles-y-permisos/portal-del-estudiante.md`
