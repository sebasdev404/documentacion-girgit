---
tags:
  - arquitectura
  - rol/rector
  - validaciones
aliases:
  - Validaciones ROL-02
  - Rector Validaciones
---

# Validaciones — Rector / Administrador del Colegio

Casos de validacion y comportamiento del sistema.

## Identidad institucional (RF-04)

| Caso | Comportamiento del Sistema |
|---|---|
| Nombre vacio o < 3 caracteres | Bloquea envio; muestra "El nombre del colegio es obligatorio (min 3 caracteres)" |
| NIT con formato invalido | Bloquea envio; muestra "NIT invalido" |
| Resolucion MEN vacia | Bloquea envio; muestra "La resolucion del MEN es obligatoria para emitir documentos" |
| Correo institucional invalido | Bloquea envio; muestra "Correo invalido" |
| Logo sobre el peso permitido por la cuota | Bloquea la subida; muestra "El archivo supera el limite de almacenamiento" |

## Calendario y periodos (RF-05)

| Caso | Comportamiento del Sistema |
|---|---|
| Elige un calendario no habilitado por el plan | Bloquea; muestra "Ese calendario no esta habilitado para su colegio; solicitelo al Superadmin" (RR-13) |
| Fechas de periodos que se solapan | Bloquea; resalta los periodos en conflicto |
| Fecha de cierre de notas posterior al fin del periodo | Bloquea; muestra "El cierre de notas debe ser anterior o igual al fin del periodo" |
| Numero de periodos fuera del rango configurado | Bloquea; muestra "El numero de periodos no es valido" |

## Escala valorativa (RF-07)

| Caso | Comportamiento del Sistema |
|---|---|
| Valor minimo mayor o igual al maximo | Bloquea; muestra "El valor minimo debe ser menor al maximo" |
| Niveles de desempeno con rangos que se solapan | Bloquea; resalta el solape |
| Escala por imagenes sin imagenes cargadas | Bloquea; muestra "Suba las imagenes de la escala" |
| Cambia la escala cuando ya hay notas cargadas | Advierte: "Hay notas registradas; el cambio puede recalcular consolidados. Confirme." (no bloquea, exige confirmacion) |

## Metodo de aprobacion (RF-08)

| Caso | Comportamiento del Sistema |
|---|---|
| Nota minima fuera del rango de la escala | Bloquea; muestra "La nota minima debe estar dentro de la escala definida" |
| Ponderaciones que no suman 100% | Bloquea; muestra "Las ponderaciones deben sumar 100%" |
| Cambia el metodo con consolidados ya calculados | Advierte impacto y exige confirmacion antes de aplicar |

## Usuarios (RF-10)

| Caso | Comportamiento del Sistema |
|---|---|
| Correo ya existente en el tenant | Bloquea; muestra "Ya existe un usuario con ese correo en el colegio" |
| Documento duplicado en el tenant | Bloquea; muestra "Ya existe un usuario con ese documento" |
| Complemento Director de Grupo sobre un rol que no es Docente | Bloquea; muestra "El complemento Director de Grupo solo aplica a Docentes" |
| Carga masiva con filas invalidas | Crea las filas validas; lista las rechazadas con su motivo; no aborta todo el lote |
| Desactivar el unico Rector activo | Bloquea; muestra "Debe existir al menos un Rector activo" |

## Roles y permisos (RF-09, RR-05)

| Caso | Comportamiento del Sistema |
|---|---|
| Intenta desactivar un permiso estructural | Bloquea; muestra "Este permiso es estructural y no se puede desactivar" |
| Intenta crear un permiso nuevo | No disponible; el sistema solo permite activar/desactivar los existentes |
| Selecciona esquema combinado teniendo asignados coordinadores separados (RR-12) | Advierte conflicto; pide resolver antes de aplicar |

## Edicion de notas post-cierre (RF-17, RR-07)

| Caso | Comportamiento del Sistema |
|---|---|
| Edita nota tras el cierre sin justificacion | Bloquea; muestra "Indique la justificacion del cambio (min 10 caracteres)" |
| Nuevo valor fuera de la escala | Bloquea; muestra "La nota debe estar dentro de la escala" |
| Permiso configurable de edicion post-cierre desactivado | Bloquea; muestra "La edicion despues del cierre no esta habilitada" |

## Documentos y SIMAT (RF-34 a RF-37, RR-08, RR-15)

| Caso | Comportamiento del Sistema |
|---|---|
| Emite documento con bloqueo por pendientes activo y el estudiante tiene pendientes | Bloquea; muestra el detalle de los pendientes (RR-08) |
| Genera documento sin identidad institucional completa | Bloquea; muestra "Complete la identidad institucional antes de emitir documentos" |
| Reporte SIMAT con datos de matricula incompletos | Bloquea; lista los registros incompletos que impiden el reporte (RR-15) |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Intenta acceder a datos de otro colegio | Bloquea en backend; aislamiento total (RR-01); registra el intento en log de seguridad |
| Intenta cambiar el calendario A/B habilitado del tenant | No disponible; la accion es del Superadmin (RR-13) |
| Accion sensible sin conectividad con el log de auditoria | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |
| Tenant suspendido por el Superadmin | Bloquea el acceso; muestra pantalla "colegio suspendido" |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
