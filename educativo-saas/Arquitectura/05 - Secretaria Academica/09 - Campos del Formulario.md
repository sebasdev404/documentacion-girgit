---
tags:
  - arquitectura
  - rol/secretaria-academica
  - formularios
aliases:
  - Campos Formulario ROL-06
  - Secretaria Formularios
---

# Campos del Formulario — Secretaria Academica

Campos de cada formulario que opera el rol.

## A) Formulario "Registrar estudiante" (RF-30)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tipo de documento | Select | Si | TI / CC / RC / CE / Pasaporte | Documento de identidad del estudiante |
| Numero de documento | Texto | Si | Unico en el tenant | Identificacion del estudiante |
| Nombres | Texto | Si | Min 2 caracteres | Nombres del estudiante |
| Apellidos | Texto | Si | Min 2 caracteres | Apellidos del estudiante |
| Fecha de nacimiento | Fecha | Si | <= hoy; coherente con el grado | Para validar edad por grado |
| Sexo | Select | Si | Lista | Dato requerido por SIMAT |
| Grado al que ingresa | Select | Si | Grado existente del tenant | Determina documentos requeridos |
| Direccion | Texto | No | — | Direccion de residencia |
| EPS / aseguradora | Texto | No | — | Dato de salud para emergencias |

## B) Formulario "Datos de acudiente operativo" (RF-30, RR-11)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Parentesco | Select | Si | Madre / Padre / Tutor / Otro | Relacion con el estudiante |
| Nombre del acudiente | Texto | Si | Min 3 caracteres | Contacto (no es usuario, `RN-TU-410`) |
| Documento del acudiente | Texto | Si | Formato valido | Identificacion del contacto |
| Telefono / celular | Texto | Si | Formato telefonico | Para avisos y citaciones |
| Correo de contacto | Email | No | Formato email valido | Para mensajes via portal (configurable) |
| Es contacto principal | Checkbox | No | Solo uno por estudiante | Marca el acudiente operativo principal |

## C) Formulario "Documento de matricula" (RF-32)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tipo de documento requerido | Select | Si | Catalogo por grado | Registro civil, notas previas, paz y salvo anterior, etc. |
| Archivo | Adjunto | No | PDF/JPG/PNG, tamano max segun cuota | Soporte digital del documento |
| Estado | Select | Si | Recibido / Pendiente | Estado del documento |
| Fecha de recepcion | Fecha | Condicional | Requerida si estado = Recibido | Cuando se recibio |
| Observacion | Texto largo | No | — | Nota interna |

## D) Formulario "Asignar a grupo" (RF-31)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante inscrito | A quien se matricula |
| Grupo | Select | Si | Grupo con cupo disponible | Grupo destino |
| Fecha de matricula | Fecha | Si | >= hoy o segun calendario | Fecha efectiva |
| Confirmar checklist completo | Checkbox | Si | Debe estar en 0 pendientes (si bloqueo activo) | Verifica documentos antes de matricular |

## E) Formulario "Generar documento oficial" (RF-34 / RF-35 / RF-36)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del tenant | A nombre de quien se emite |
| Tipo de documento | Select | Si | Constancia / Certificado de notas / Paz y salvo | Define la plantilla |
| Periodo / ano lectivo | Select | Condicional | Requerido en certificado de notas | Periodo a certificar |
| Dirigido a | Texto | No | — | Destinatario (entidad o "a quien interese") |
| Consecutivo | Auto | Si | No editable, unico por tipo (`RN-GD-001`) | Lo asigna el sistema |
| Motivo de emision | Texto | No | — | Queda en la trazabilidad |

## F) Formulario "Generar reporte SIMAT" (RF-37, RR-15)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Periodo de reporte | Select | Si | Ventana del MEN | Periodo a reportar |
| Tipo de novedad | Select | Si | Matricula / Retiro / Traslado / Promocion | Novedad a incluir |
| Grado(s) | Multi-select | No | Grados del tenant | Filtra el alcance |
| Validar antes de exportar | Checkbox | Si | Debe correr la validacion (`RN-MO-004`) | Evita exportar datos inconsistentes |
| Marcar como enviado | Checkbox | No | — | Deja el reporte trazable |

## G) Formulario "Consentimiento de habeas data" (RN-HD-001)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del tenant | Titular de los datos (menor) |
| Tipo de consentimiento | Select | Si | Tratamiento de datos / Uso de imagen | Que autoriza |
| Acudiente que autoriza | Select | Si | Acudiente operativo del estudiante | Quien firma (`RN-HD-002`) |
| Archivo firmado | Adjunto | Condicional | Requerido si estado = Firmado | Soporte de la firma |
| Estado | Select | Si | Pendiente / Firmado / Revocado | Estado del consentimiento |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
