---
tags:
  - arquitectura
  - rol/docente
  - validaciones
aliases:
  - Validaciones ROL-07
---

# Validaciones — Docente

Casos de validacion y comportamiento del sistema.

## Registrar / editar notas (RF-16)

| Caso | Comportamiento del Sistema |
|---|---|
| Nota vacia al guardar | Bloquea envio; muestra "Ingrese la nota del estudiante" |
| Nota fuera de la escala valorativa | Bloquea envio; muestra "La nota debe estar dentro de la escala configurada" |
| Grupo o materia no asignado al docente | Bloquea en backend; no muestra el grupo en el selector (RR-10); registra intento en log |
| Periodo cerrado y permiso post-cierre desactivado | Bloquea edicion; muestra "El periodo esta cerrado; no puede editar notas" (RR-07) |
| Periodo cerrado y permiso post-cierre activo, sin justificacion | Bloquea envio; exige justificacion (min 10 caracteres) que queda en log |
| Estudiante no inscrito en el grupo | No aparece en la planilla; si llega por API, backend rechaza |

## Registrar asistencia (RF-22)

| Caso | Comportamiento del Sistema |
|---|---|
| Fecha futura | Bloquea; muestra "No puede registrar asistencia de una fecha futura" |
| Estado sin seleccionar para algun estudiante | Advierte; permite guardar parcial solo si el colegio lo configura, si no exige completar |
| Estado "Excusa" sin nota | Bloquea envio; muestra "Indique el detalle de la excusa" |
| Clase fuera del horario del docente | Bloquea en backend; no corresponde a su asignacion (RR-10) |
| Doble registro de la misma clase del dia | Abre el registro existente para edicion en lugar de duplicar |

## Observacion academica (RF-24)

| Caso | Comportamiento del Sistema |
|---|---|
| Descripcion < 10 caracteres | Bloquea envio; muestra "La observacion es muy corta (min 10 caracteres)" |
| Estudiante fuera de sus grupos | Bloquea; no aparece en el selector (RR-10) |
| Intento de usar tipologia disciplinaria | Bloquea; el catalogo del docente es academico, no disciplinario |

## Convivencia (reporte)

| Caso | Comportamiento del Sistema |
|---|---|
| Descripcion de hechos < 20 caracteres | Bloquea envio; muestra "Describa los hechos (min 20 caracteres)" |
| Intento de clasificar el tipo del caso | No disponible para el docente; la clasificacion es del Coordinador de Convivencia (RN-CVE-002) |
| Marca "presunto delito" | No bloquea; escala de inmediato al Rector y restringe la visibilidad (RN-CVE-004) |

## Salud (alertas de aula)

| Caso | Comportamiento del Sistema |
|---|---|
| Intento de abrir la ficha medica completa | Bloquea; el docente solo ve alertas autorizadas (RN-SA-002, RN-SA-007) |
| No hay alerta autorizada para el estudiante | Muestra "Sin alertas de salud autorizadas para docencia" |
| Remision sin motivo | Bloquea envio; exige el motivo |

## Mensajes a acudientes (RF-43)

| Caso | Comportamiento del Sistema |
|---|---|
| Permiso de mensajeria desactivado por el colegio | Oculta la accion en UI; backend rechaza si llega por API |
| Mensaje a un estudiante fuera de sus grupos | Bloquea; el selector solo muestra sus estudiantes (RR-10) |
| Cuerpo del mensaje vacio | Bloquea envio; muestra "Escriba el mensaje" |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Intento de acceder por el subdominio de otro colegio | Bloquea; el tenant se infiere del subdominio antes de validar credenciales (RR-06) |
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Token expirado a mitad de carga de notas | Cierra sesion; la operacion no se aplica; pide reautenticacion |
| Acceso a un modulo sin permiso (consolidados, configuracion, boletines) | El modulo no aparece en el sidebar; backend rechaza la ruta directa (RR-02) |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
