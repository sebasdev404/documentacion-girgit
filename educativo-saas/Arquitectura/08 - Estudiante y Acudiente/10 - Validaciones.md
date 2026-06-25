---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
  - validaciones
aliases:
  - Validaciones ROL-09
  - Estudiante y Acudiente Validaciones
---

# Validaciones — Estudiante / Acudiente

Casos de validacion y comportamiento del sistema.

## Acceso al portal

| Caso | Comportamiento del Sistema |
|---|---|
| Portal desactivado por el colegio | Bloquea login; muestra "El portal no esta habilitado por tu colegio" (RN-PE-001) |
| Credenciales invalidas | Bloquea acceso; mensaje generico que no revela si el usuario existe; registra en log de seguridad |
| Primer ingreso con contrasena temporal | Fuerza el cambio de contrasena antes de continuar (RN-AU-360) |
| Intento de entrar por el subdominio de otro colegio | Bloquea; el tenant se infiere del subdominio (RR-06); no autentica con credenciales de otro tenant |
| Correo vinculado a varios estudiantes | Muestra selector de estudiante; no entra a un dashboard sin elegir contexto (RR-14) |

## Justificar inasistencia

| Caso | Comportamiento del Sistema |
|---|---|
| Sin seleccionar inasistencia | Bloquea envio; muestra "Selecciona la inasistencia a justificar" |
| Motivo < 10 caracteres | Bloquea envio; muestra "Describe el motivo (min 10 caracteres)" |
| Soporte con formato/peso no permitido | Bloquea adjunto; muestra "Archivo no permitido o demasiado grande" |
| Checkbox de veracidad sin marcar | Bloquea envio; resalta el checkbox |
| Envio correcto | Crea la justificacion en estado Pendiente; NO cambia el estado de la inasistencia hasta revision (RN-PE-005) |

## Confirmar / descargar boletin

| Caso | Comportamiento del Sistema |
|---|---|
| Confirmar sin marcar el checkbox | Bloquea; exige marcar "Confirmo que recibi y revise el boletin" |
| Descargar PDF con deuda y bloqueo por paz y salvo activo | Bloquea descarga; muestra el detalle de lo pendiente (RN-PE-003, RN-PE-006) |
| Descargar boletin no emitido aun | Bloquea; muestra "El boletin aun no esta disponible" |
| Confirmacion correcta | Registra fecha, hora e IP asociadas al usuario (RN-PE-004) |

## Pagar concepto

| Caso | Comportamiento del Sistema |
|---|---|
| Cuota ya pagada | Bloquea; muestra "Esta cuota ya esta pagada" |
| Pasarela rechaza la transaccion | Mantiene la cuota Pendiente; muestra "Pago rechazado, intenta de nuevo"; registra el intento |
| Navegador confirma pero no llega webhook | NO marca como pagada por la pantalla; espera el webhook de la pasarela (RN-PP-003) |
| Mismo transactionId llega dos veces | Ignora el duplicado; no registra doble pago (RN-PP-004) |
| Sin pasarela habilitada por el colegio | No muestra el boton Pagar; indica que el pago no esta disponible en linea |

## Cargar / solicitar documentos

| Caso | Comportamiento del Sistema |
|---|---|
| Archivo de tipo/peso no permitido | Bloquea carga; muestra "Archivo no permitido o demasiado grande" |
| Documento ya aprobado | Bloquea recarga; muestra "Este documento ya fue aprobado" |
| Solicitar certificado cobrable con deuda principal | Bloquea; no genera el cargo del certificado mientras exista deuda (RN-PYS-150) |
| Solicitar documento con bloqueo por paz y salvo | Bloquea; muestra lo que debe resolver (RN-PE-003, RN-PZ-005) |
| Cargue correcto | Guarda en estado En revision; notifica a Secretaria (RN-GD-270) |

## Solicitar cita / mensaje a docente

| Caso | Comportamiento del Sistema |
|---|---|
| Motivo de cita < 10 caracteres | Bloquea envio; muestra "Describe el motivo (min 10 caracteres)" |
| Disponibilidad propuesta en el pasado | Bloquea; muestra "Elige una fecha futura" |
| Mensaje a docente con canal deshabilitado | La opcion no aparece; el modulo queda como solo lectura de comunicados (RN-MI-180) |

## Solo lectura y scope

| Caso | Comportamiento del Sistema |
|---|---|
| Intento de editar una nota/asistencia/observador desde la UI | La UI no ofrece controles de edicion; cualquier llamada directa se rechaza en backend (RN-PE-002, RR-02) |
| Intento de acceder a datos de otro estudiante | Bloquea; el scope se limita al estudiante en contexto (RR-14); registra el intento |
| Acudiente con varios hijos intenta ver datos mezclados | El sistema no fusiona; solo muestra el estudiante seleccionado (RN-CP-002, RN-PP-120) |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |
| Accion sensible sin conectividad con el log | Bloquea la accion; no se opera sin poder auditar (RR-03) |
| Preferencia de notificacion sobre evento critico | Bloquea desactivacion; los eventos criticos no se pueden apagar (RN-NO-001) |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
