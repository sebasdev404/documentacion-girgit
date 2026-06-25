---
tags:
  - arquitectura
  - rol/secretaria-academica
  - validaciones
aliases:
  - Validaciones ROL-06
  - Secretaria Validaciones
---

# Validaciones — Secretaria Academica

Casos de validacion y comportamiento del sistema.

## Registrar estudiante

| Caso | Comportamiento del Sistema |
|---|---|
| Numero de documento vacio | Bloquea envio; muestra "El documento del estudiante es obligatorio" |
| Documento ya existente en el tenant | Bloquea envio; muestra "Ya existe un estudiante con este documento" |
| Nombres o apellidos vacios | Bloquea envio; resalta los campos faltantes |
| Fecha de nacimiento futura | Bloquea envio; muestra "La fecha de nacimiento no puede ser futura" |
| Grado no seleccionado | Bloquea envio; muestra "Seleccione el grado de ingreso" |
| Sin consentimiento de habeas data | Advierte: "Falta el consentimiento de tratamiento de datos del menor"; permite crear pero bloquea matricula si el colegio lo exige (`RN-HD-001`) |

## Datos de acudiente operativo

| Caso | Comportamiento del Sistema |
|---|---|
| Sin nombre o telefono del acudiente | Bloquea envio; muestra "El contacto operativo requiere nombre y telefono" |
| Correo con formato invalido | Bloquea envio; muestra "Correo invalido" |
| Marcar dos acudientes como principal | Bloquea; muestra "Solo un acudiente puede ser el contacto principal" |
| Intentar crear el acudiente como usuario | Bloquea en backend; el acudiente es contacto, no usuario (RR-11, `RN-TU-410`) |

## Documentos y matricula

| Caso | Comportamiento del Sistema |
|---|---|
| Marcar documento "Recibido" sin fecha de recepcion | Bloquea envio; exige la fecha |
| Adjunto con formato o tamano no permitido | Bloquea; muestra "Formato/tamano de archivo no permitido" |
| Asignar a grupo sin cupo disponible | Bloquea; muestra "El grupo no tiene cupo disponible" |
| Asignar a grupo con documentos pendientes (bloqueo activo) | Bloquea; muestra "Hay documentos pendientes; complete el checklist" (RR-08) |
| Cambiar grupo post-matricula con permiso restringido | Bloquea; muestra "El cambio de grupo lo realiza el Coordinador Academico" (RR-05) |

## Emision de documentos oficiales

| Caso | Comportamiento del Sistema |
|---|---|
| Emitir con documentos pendientes y bloqueo activado | Bloquea; muestra "No se puede emitir: el estudiante tiene documentos pendientes" (RR-08, `RN-GD-270`) |
| Emitir con pagos pendientes y bloqueo activado | Bloquea; muestra "No se puede emitir el paz y salvo: cartera pendiente" (`RN-PZ-002`) |
| Emitir en modo advertencia (bloqueo desactivado) | Permite emitir; estampa sello de advertencia y registra el pendiente en log |
| Certificado de notas con periodo sin consolidar | Bloquea; muestra "El periodo no tiene notas consolidadas para certificar" |
| Intento de editar el consecutivo | Bloquea; el consecutivo es automatico y no editable (`RN-GD-001`) |
| Intento de editar notas al generar certificado | Bloquea en backend; la secretaria solo lee el consolidado (no edita notas) |

## Reporte SIMAT

| Caso | Comportamiento del Sistema |
|---|---|
| Exportar sin correr la validacion previa | Bloquea; muestra "Valide los datos antes de exportar" (`RN-MO-004`) |
| Datos inconsistentes (campos requeridos del MEN vacios) | Bloquea exportacion; lista los registros con error para corregir |
| Reporte fuera de la ventana del MEN | Advierte: "El periodo esta fuera de la ventana de reporte"; permite generar borrador |
| Marcar como enviado sin haber descargado | Advierte; pide confirmar que el archivo se cargo en el portal del MEN |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Acceso a un estudiante de otro tenant | Bloquea en backend; aislamiento total por tenant (RR-01) |
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Permiso configurable desactivado (comunicaciones / historial) | Oculta o deshabilita la accion en UI y la rechaza en backend (RR-02, RR-05) |
| Token expirado a mitad de una emision | Cierra sesion; el documento no se emite ni consume consecutivo; pide reautenticacion |
| Sesion en tenant suspendido | Muestra "colegio suspendido"; no permite operar |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
