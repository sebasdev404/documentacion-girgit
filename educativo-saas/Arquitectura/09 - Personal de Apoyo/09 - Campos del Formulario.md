---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - formularios
aliases:
  - Campos Formulario ROL-12
---

# Campos del Formulario — Personal de Apoyo

Campos de cada formulario que opera el rol. Los formularios de modulo de servicio solo aparecen para el **perfil** correspondiente (`RN-TU-004`).

## A) Formulario "Aporte al observador" (RF-48, nucleo comun)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Buscador/Select | Si | Estudiante del tenant | Se ubica por nombre/documento/grupo |
| Tipo de anotacion | Select | Si | Catalogo del colegio | Clasifica la anotacion |
| Descripcion | Texto largo | Si | Min 10 caracteres | Hecho a registrar |
| Visibilidad | Select | Si | publica / docentes / interna | Por defecto **interna** (`RN-TU-005`, `RN-OB-081`) |
| Fecha del hecho | Fecha | Si | <= hoy | Cuando ocurrio |

## B) Formulario "Remision interna" (nucleo comun)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Buscador/Select | Si | Estudiante del tenant | Sujeto de la remision |
| Destino | Select | Si | Coordinacion / otro perfil de servicio | A quien se deriva |
| Motivo (resumen) | Texto largo | Si | Min 10 caracteres | No se expone en la notificacion al estudiante/acudiente |
| Urgencia | Select | Si | normal / prioritaria | Define el orden de atencion |

## C) Formulario "Agendar cita de bienestar" (perfil Orientador, `RN-BW`)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante / Acudiente | Select | Si | Destinatario valido | A quien se cita |
| Tipo de atencion | Select | Si | Catalogo de bienestar | Individual / con acudiente / seguimiento / crisis |
| Fecha y hora | Fecha-hora | Si | >= ahora; sin choque de agenda | Programacion de la cita |
| Modalidad | Select | Si | presencial / virtual | Define si reserva consultorio |
| Consultorio | Select | No | Espacio disponible | Solo si es presencial |
| Motivo (interno) | Texto largo | No | — | **No** viaja en la notificacion (`RN-BW-006`) |

## D) Formulario "Atencion en enfermeria" (perfil Enfermeria, `RN-SA`)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Buscador/Select | Si | Estudiante del tenant | Carga su ficha medica y alertas |
| Motivo de consulta | Texto largo | Si | Min 5 caracteres | Por que llega a enfermeria |
| Signos observados | Texto | No | — | Temperatura, sintomas, etc. |
| Medicamento suministrado | Select | No | Solo de la lista **autorizada y vigente** (`RN-SA-003`) | Bloqueado si no hay autorizacion |
| Dosis y hora | Texto / Hora | Condicional | Obligatorio si hay medicamento | Trazabilidad del suministro |
| Disposicion | Select | Si | regreso a clase / reposo / llamar acudiente / remision | Cierre de la atencion |

## E) Formulario "Remision a centro medico" (perfil Enfermeria, `RN-SA`)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante con atencion abierta | Sujeto de la remision |
| Centro de destino | Texto/Select | Si | — | Donde se remite |
| Medio de traslado | Select | Si | — | Ambulancia / acudiente / otro |
| Acompanante | Texto | Si | — | Quien acompana al estudiante |
| Desenlace | Texto largo | No (al cierre Si) | Obligatorio para cerrar (`RN-SA-006`) | Resultado reportado |

## F) Formulario "Prestamo de biblioteca" (perfil Bibliotecario, `RN-BI`)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Usuario | Buscador/Select | Si | Estudiante o docente sin bloqueo por mora | Quien toma el prestamo |
| Ejemplar (codigo de barras) | Texto/Escaner | Si | Ejemplar en estado Disponible (`RN-BI-001`) | Copia fisica concreta |
| Fecha de salida | Fecha | Auto | = hoy | Inicio del prestamo |
| Fecha de vencimiento | Fecha | Auto (no editable) | Calculada por configuracion (`RN-BI-002`) | Plazo segun tipo de usuario/material |

## G) Formulario "Multa de biblioteca" (perfil Bibliotecario, `RN-BI`)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Prestamo asociado | Select | Si | Prestamo vencido/dano/extravio | Origen de la multa |
| Motivo | Select | Si | mora / dano / extravio | Tipo de cargo |
| Valor | Numero | Auto | Segun politica y tope (`RN-BI-005`) | Liquidacion automatica |
| Integrar a cartera | Checkbox | Auto | Segun config del colegio (`RN-BI-006`) | Solo si el tenant lo activo |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
