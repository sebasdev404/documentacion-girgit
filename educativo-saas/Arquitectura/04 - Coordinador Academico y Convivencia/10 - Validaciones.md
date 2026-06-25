---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
  - validaciones
aliases:
  - Validaciones ROL-05
---

# Validaciones — Coordinador Academico y Convivencia

Casos de validacion y comportamiento del sistema.

## Plan de estudios y grupos

| Caso | Comportamiento del Sistema |
|---|---|
| Nombre de materia vacio o < 3 caracteres | Bloquea envio; muestra "El nombre de la materia es obligatorio (min 3 caracteres)" |
| Materia duplicada en el mismo grado | Bloquea envio; muestra "Ya existe una materia con ese nombre en el grado" |
| Intensidad horaria <= 0 | Bloquea envio; muestra "La intensidad horaria debe ser mayor a cero" |
| Archivar una materia con grupos activos en el ano | Bloquea; muestra "No se puede archivar: tiene grupos activos este ano" |
| Nombre de grupo duplicado en grado y ano | Bloquea envio; muestra "Ya existe un grupo con ese nombre en el grado y ano" |

## Asignaciones y horarios

| Caso | Comportamiento del Sistema |
|---|---|
| Asignar un docente inactivo | Bloquea; muestra "El docente no esta activo" |
| Asignar una materia que no pertenece al grado del grupo | Bloquea; muestra "La materia no pertenece al grado del grupo" |
| Designar director de grupo a un docente sin asignacion en el tenant | Advierte; permite continuar si el colegio lo autoriza |
| Choque de docente (mismo bloque, dos grupos) | Bloquea la publicacion; resalta el bloque en conflicto |
| Choque de aula (misma aula, mismo bloque) | Bloquea la publicacion; resalta el aula en conflicto |
| Horas asignadas distintas a la intensidad del plan | Advierte: "El total de horas no coincide con la intensidad de la materia"; no bloquea |

## Consolidados y cierre

| Caso | Comportamiento del Sistema |
|---|---|
| Ejecutar cierre con notas faltantes | Bloquea; lista los docentes y grupos con notas pendientes |
| Ejecutar cierre de un periodo ya cerrado | Bloquea; muestra "El periodo ya esta cerrado" |
| Editar nota tras cierre sin el permiso configurable | Bloquea; muestra "No tiene permiso para editar notas despues del cierre" |
| Editar nota tras cierre sin justificacion | Bloquea; exige justificacion (min 10 caracteres) que queda en log (RR-07) |
| Nota fuera de la escala valorativa del tenant | Bloquea; muestra "La nota esta fuera de la escala valorativa del colegio" |

## Nivelaciones / habilitaciones

| Caso | Comportamiento del Sistema |
|---|---|
| El coordinador intenta registrar la nota de la nivelacion | Bloquea; muestra "Solo el docente titular registra la nota de nivelacion" (RN-NH-002) |
| Anular un proceso sin motivo | Bloquea; exige motivo que queda en log |
| Operar nivelaciones de un ano cerrado | Bloquea; muestra "Los procesos de un ano cerrado son inmutables" (RN-NH-005) |

## Boletines

| Caso | Comportamiento del Sistema |
|---|---|
| Aprobar boletin sin el permiso configurable | Bloquea; muestra "La aprobacion de boletines no esta habilitada para este rol" |
| Aprobar un boletin de un periodo no cerrado | Bloquea; muestra "El periodo debe estar cerrado para aprobar boletines" |

## Observador

| Caso | Comportamiento del Sistema |
|---|---|
| Anotacion sin tipologia | Bloquea; muestra "Seleccione una tipologia" |
| Descripcion vacia o < 10 caracteres | Bloquea; muestra "Describa el hecho (min 10 caracteres)" |
| Fecha del hecho fuera del ano lectivo | Bloquea; muestra "La fecha debe estar dentro del ano lectivo" |
| Anular anotacion sin justificacion | Bloquea; exige justificacion; conserva el historial (RN-OE-003) |
| Editar anotacion de un observador de ano cerrado | Bloquea; muestra "El observador de un ano cerrado es inmutable" (RN-OE-004) |

## Convivencia (Ley 1620)

| Caso | Comportamiento del Sistema |
|---|---|
| Avanzar un caso sin clasificar | Bloquea; muestra "Debe clasificar el caso (tipo I/II/III) antes de continuar" (RN-CVE-002) |
| Reclasificar sin justificacion | Bloquea; exige justificacion con autor y fecha |
| Cerrar un caso tipo III sin constancia de reporte a la autoridad | Bloquea; muestra "El caso tipo III no se puede cerrar sin registrar el reporte a la autoridad" (RN-CVE-004) |
| Cerrar un caso con dano al cuerpo sin remision a salud | Bloquea; muestra "Registre la atencion en salud antes de cerrar" (RN-CVE-005) |
| Citacion con motivo sensible en el cuerpo de la notificacion | Bloquea / advierte; el motivo clinico no se incluye en la notificacion al acudiente |
| Plazo de protocolo por debajo del minimo legal | Bloquea; muestra "El plazo no puede ser inferior al minimo legal" (RN-CVE-010) |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Intento de ver datos de otro tenant | Bloquea en backend; no devuelve resultados (RR-01) |
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Tenant del colegio suspendido | Bloquea acceso; muestra pantalla "colegio suspendido" |
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |
| El colegio activa ROL-03 / ROL-04 separados teniendo ROL-05 activo | Advierte / bloquea segun politica; recuerda que el esquema combinado excluye los separados (RR-12) |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
