---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
  - formularios
aliases:
  - Campos Formulario ROL-09
  - Estudiante y Acudiente Campos
---

# Campos del Formulario — Estudiante / Acudiente

Campos de cada formulario que opera el rol. Es un rol de consulta; los formularios son los pocos puntos de autogestion (justificar, pagar, confirmar, cargar, solicitar).

## A) Formulario "Justificar inasistencia" (RF-23, RN-PE-005)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Inasistencia a justificar | Select (lista) | Si | Inasistencia existente del estudiante en contexto | La ausencia que se quiere justificar |
| Motivo | Texto largo | Si | Min 10 caracteres | Explicacion de la ausencia |
| Soporte | Archivo | No | PDF/JPG/PNG, max segun politica del colegio | Incapacidad u otro documento de respaldo |
| Confirmacion de veracidad | Checkbox | Si | Debe marcarse | "Declaro que la informacion es veraz" |

## B) Formulario "Confirmar boletin" (RN-PE-004)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Boletin | Lectura (no editable) | — | Boletin emitido del estudiante | Boletin del periodo a confirmar |
| Confirmacion de recepcion | Checkbox | Si | Debe marcarse | "Confirmo que recibi y revise el boletin" |
| Fecha, hora e IP | Auto (sistema) | Auto | Registrado por el sistema | Queda asociado al usuario (RN-PE-004) |

## C) Formulario "Pagar concepto" (RN-PP-003)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Concepto / cuota | Select o lista | Si | Cuota pendiente del estudiante | Que se va a pagar |
| Monto | Lectura (no editable) | — | Igual al valor de la cuota (con descuentos aplicados) | Deuda unica por estudiante (RN-PP-120) |
| Medio de pago | Select | Si | Pasarela/medio habilitado por el colegio | PSE, tarjeta, boton local, etc. |
| Datos del pagador | Texto/Email | Segun pasarela | Validacion de la pasarela | Lo gestiona la pasarela; el sistema no valida tarjetas |

> El estado final del pago lo determina el webhook de la pasarela, no la confirmacion del navegador (RN-PP-003). No se permite registrar dos veces el mismo transactionId (RN-PP-004).

## D) Formulario "Cargar documento requerido" (RF-32, RN-GD-270)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tipo de documento | Select | Si | Tipo solicitado por el colegio | Documento requerido de matricula |
| Archivo | Archivo | Si | PDF/JPG/PNG, max segun politica | El documento a cargar |
| Observacion | Texto | No | — | Comentario opcional del solicitante |

> Al cargar, el documento queda En revision; la aprobacion/rechazo la hace Secretaria y se notifica (RN-GD-270).

## E) Formulario "Solicitar documento oficial" (RF-34 / RF-35 / RF-36)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tipo de documento | Select | Si | Constancia / certificado de notas / paz y salvo | Documento solicitado |
| Motivo / destino | Texto | No | — | Para que se necesita |
| Aceptacion de costo | Checkbox | Condicional | Obligatorio si el documento es cobrable | Habilita el pago previo (RN-PE-006, RN-PYS-150) |

> Si existe deuda principal, el sistema no genera ni siquiera el cargo del certificado (RN-PYS-150). El paz y salvo no se exige para asistir/consultar durante el ano en curso (RN-PZ-006).

## F) Formulario "Solicitar cita"

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Con quien | Select | Si | Docente del estudiante o coordinacion | Destinatario de la cita |
| Motivo | Texto largo | Si | Min 10 caracteres | Razon de la cita |
| Disponibilidad propuesta | Fecha/Hora (multiple) | Si | Fecha >= hoy | Horarios sugeridos por el solicitante |

## G) Formulario "Mensaje a docente" (RF-43, configurable RN-MI-180)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Destinatario | Select | Si | Docente del estudiante / coordinacion | Solo disponible si el canal esta habilitado |
| Asunto | Texto | Si | Min 3 caracteres | Tema del mensaje |
| Mensaje | Texto largo | Si | Min 10 caracteres | Contenido del mensaje formal |
| Adjunto | Archivo | No | Segun politica | Soporte opcional |

## H) Formulario "Cambiar contrasena" (RN-AU-360)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Contrasena actual | Password | Si | Debe coincidir | Verificacion del titular |
| Contrasena nueva | Password | Si | Politica de complejidad del sistema | Reemplaza la temporal/anterior |
| Confirmar contrasena | Password | Si | Igual a la nueva | Evita errores de tipeo |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
