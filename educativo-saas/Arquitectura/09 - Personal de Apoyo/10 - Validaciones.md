---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - validaciones
aliases:
  - Validaciones ROL-12
---

# Validaciones — Personal de Apoyo

Casos de validacion y comportamiento del sistema.

## Acceso y perfil

| Caso | Comportamiento del Sistema |
|---|---|
| Cuenta sin perfil asignado | Bloquea el ingreso al servicio; muestra "Esta cuenta no tiene un perfil asignado; contacte al Rector" (`RN-TU-003`) |
| Intento de abrir el modulo de un perfil ajeno | Bloquea en backend; muestra "No tiene acceso a este servicio" (`RN-TU-004`); registra el intento en log |
| Intento de abrir notas/cartera/configuracion | No se renderiza el modulo; el backend rechaza la llamada (RR-02, `RN-TU-002`) |

## Aporte al observador (`RN-OB-081`)

| Caso | Comportamiento del Sistema |
|---|---|
| Descripcion vacia o < 10 caracteres | Bloquea envio; muestra "Describa el hecho (min 10 caracteres)" |
| Sin nivel de visibilidad | Bloquea envio; el sistema preselecciona **interna** por defecto (`RN-TU-005`) |
| Fecha del hecho en el futuro | Bloquea envio; muestra "La fecha no puede ser futura" |
| Intento de borrar un aporte existente | No permite borrado fisico; solo anotacion correctiva |

## Ficha del estudiante

| Caso | Comportamiento del Sistema |
|---|---|
| Solicita ver notas/boletines desde la ficha | No expone esos datos; la ficha es acotada (`RN-TU-006`) |
| Consulta de ficha | Permite ver datos acotados y **registra la consulta** en log (`RN-TU-009`) |

## Bienestar (perfil Orientador, `RN-BW`)

| Caso | Comportamiento del Sistema |
|---|---|
| Cita en fecha/hora pasada o con choque de agenda | Bloquea envio; muestra "Horario no disponible" |
| Notificacion de cita con motivo clinico | El sistema nunca incluye el motivo en la notificacion (`RN-BW-006`) |
| Remision externa sin consentimiento del acudiente | Bloquea; exige registrar el consentimiento antes de compartir datos (`RN-BW-005`) |
| Cerrar caso sin resumen | Bloquea; exige resumen de cierre (`RN-BW-009`) |

## Salud (perfil Enfermeria, `RN-SA`)

| Caso | Comportamiento del Sistema |
|---|---|
| Suministrar medicamento sin autorizacion vigente | Bloquea el registro; muestra "Sin autorizacion vigente; contacte al acudiente" (`RN-SA-003`) |
| Atencion sin motivo de consulta | Bloquea envio; exige el motivo |
| Editar una atencion ya guardada | No permite editar el registro original; obliga a una anotacion adicional (`RN-SA-004`) |
| Cerrar remision a centro medico sin desenlace | Bloquea; exige registrar el desenlace (`RN-SA-006`) |

## Biblioteca (perfil Bibliotecario, `RN-BI`)

| Caso | Comportamiento del Sistema |
|---|---|
| Usuario con bloqueo por morosidad activo | Bloquea el prestamo; muestra "Usuario con mora pendiente; regularice primero" (`RN-BI-004`) |
| Prestamo sobre un material sin ejemplar disponible | Bloquea; ofrece crear una **reserva** en cola |
| Editar manualmente la fecha de vencimiento | No permitido; se calcula por configuracion (`RN-BI-002`) |
| Cupo maximo de ejemplares superado | Bloquea; muestra "Cupo maximo alcanzado" (`RN-BI-003`) |
| Devolucion de un ejemplar no prestado | Bloquea; muestra "Ese ejemplar no figura prestado" |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |
| Intento de acceder a datos de otro tenant | Bloquea en backend; aislamiento total (RR-01) |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
