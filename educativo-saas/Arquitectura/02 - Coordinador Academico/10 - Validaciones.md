---
tags:
  - arquitectura
  - rol/coord-academico
  - validaciones
aliases:
  - Validaciones ROL-03
---

# Validaciones — Coordinador Academico

Casos de validacion y comportamiento del sistema.

## Plan de estudios

| Caso | Comportamiento del Sistema |
|---|---|
| Nombre de materia vacio o < 3 caracteres | Bloquea envio; muestra "El nombre de la materia es obligatorio (min 3 caracteres)" |
| Materia duplicada en el mismo grado | Bloquea envio; muestra "Ya existe esa materia en este grado" |
| Intensidad horaria <= 0 o no entera | Bloquea envio; muestra "La intensidad horaria debe ser un numero mayor que cero" |
| Archivar materia en uso en grupos activos | Advierte: "Esta materia esta asignada en grupos activos. Archivar la quita del plan pero conserva el historico." (exige confirmacion) |

## Grupos

| Caso | Comportamiento del Sistema |
|---|---|
| Nombre de grupo duplicado en grado y ano | Bloquea envio; muestra "Ya existe un grupo con ese nombre en este grado y ano" |
| Jornada no configurada por el Rector | Bloquea envio; muestra "No hay jornadas configuradas; pida al Rector configurarlas" |
| Ano lectivo no activo | Bloquea envio; muestra "Seleccione un ano lectivo activo" |

## Asignacion docente

| Caso | Comportamiento del Sistema |
|---|---|
| Materia ya tiene titular en ese grupo | Bloquea o pide reasignar; muestra "Esa materia ya tiene docente titular en este grupo" |
| Docente inactivo | Bloquea envio; muestra "No se puede asignar a un docente inactivo" |
| Grupo ya tiene director de grupo | Bloquea la segunda designacion; muestra "Este grupo ya tiene director de grupo asignado" |

## Horarios

| Caso | Comportamiento del Sistema |
|---|---|
| Cruce de docente (mismo docente en dos sitios) | Bloquea envio; resalta el bloque; muestra "El docente ya esta asignado en ese bloque" |
| Cruce de aula | Bloquea envio; muestra "El aula ya esta ocupada en ese bloque" |
| Cruce de grupo (dos materias al grupo a la vez) | Bloquea envio; muestra "El grupo ya tiene clase en ese bloque" |
| Materia sin docente asignado | Bloquea publicacion; muestra "Asigne un docente a la materia antes de incluirla en el horario" |

## Cierre de periodo

| Caso | Comportamiento del Sistema |
|---|---|
| Activar cierre con grupos de consolidado incompleto | Bloquea; lista los grupos y docentes pendientes; muestra "Hay consolidados incompletos; complete antes de cerrar" |
| Confirmacion sin marcar | Bloquea envio; resalta el checkbox |
| Reabrir periodo sin motivo | Bloquea; exige motivo (min 10 caracteres) y queda en log (RR-07) |
| Reabrir periodo sin permiso (config. lo restringe al Rector) | Bloquea; muestra "La reapertura de periodo requiere autorizacion del Rector" |

## Notas (permiso configurable)

| Caso | Comportamiento del Sistema |
|---|---|
| Editar nota sin el permiso activado | Oculta/deshabilita la accion en UI y la rechaza en backend (RR-02); muestra "No tiene permiso para editar notas directamente" |
| Editar nota con periodo cerrado y sin permiso de post-cierre | Bloquea; muestra "El periodo esta cerrado; la edicion requiere permiso y justificacion" (RR-07) |
| Editar nota tras cierre sin justificacion | Bloquea; exige justificacion antes de aplicar |

## Nivelaciones

| Caso | Comportamiento del Sistema |
|---|---|
| Abrir nivelacion para estudiante sin materias perdidas | Bloquea; muestra "El estudiante no tiene materias perdidas en el periodo" |
| Fecha limite anterior a hoy | Bloquea envio; muestra "La fecha limite no puede ser anterior a hoy" |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Intento de acceder al observador disciplinario | Oculto en UI; backend rechaza (RR-02); registra intento en log |
| Intento de modificar configuracion base (escala, calendario) | No aparece en su sidebar; backend rechaza si se fuerza la llamada |
| Intento de emitir documento oficial | Accion no disponible; backend rechaza |
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
