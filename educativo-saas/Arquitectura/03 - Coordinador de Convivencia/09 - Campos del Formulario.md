---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - formularios
aliases:
  - Campos Formulario ROL-04
  - Coord. Convivencia Campos
---

# Campos del Formulario — Coordinador de Convivencia

Campos de cada formulario que opera el rol.

## A) Formulario "Registrar anotacion en observador" (RF-26)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Buscador / Select | Si | Estudiante existente del tenant | A quien se le registra la anotacion |
| Tipo de anotacion | Select | Si | Del catalogo de tipologias del colegio | Llamado de atencion, compromiso, felicitacion, remision, suspension, etc. |
| Tipologia (gravedad) | Select | Si | leve / grave / gravisima (o custom) | Segun el catalogo definido (RN-OB-080) |
| Descripcion del hecho | Texto largo | Si | Min 15 caracteres | Narracion objetiva de la situacion |
| Fecha del hecho | Fecha | Si | Dentro del ano lectivo abierto | Cuando ocurrio |
| Nivel de visibilidad | Select | Si | publica / docentes / interna | Quien podra ver la anotacion (RN-OB-081) |
| Requiere confirmacion del acudiente | Checkbox | No | — | Si se marca, se solicita confirmacion via portal |
| Adjuntos | Archivo | No | Tipos permitidos; sujeto a cuota | Evidencias o soportes |

## B) Formulario "Definir tipologia de anotacion" (RF-27)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre de la tipologia | Texto | Si | Unico en el colegio; min 3 caracteres | Ej. "Bullying", "Liderazgo" |
| Gravedad base | Select | Si | leve / grave / gravisima | Clasificacion del catalogo |
| Categoria | Select | Si | Del catalogo base + custom (RN-OB-080) | Convivencia, salud, citacion, etc. |
| Requiere confirmacion por defecto | Checkbox | No | — | Si las anotaciones de este tipo piden confirmacion |
| Medidas sugeridas | Multi-select | No | Del catalogo de medidas | Restaurativas / pedagogicas asociadas |
| Estado | Toggle | Si | Activa / Inactiva | Inactivar no borra historico |

## C) Formulario "Clasificar caso de convivencia" (Ley 1620)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiantes involucrados | Multi-select | Si | Estudiantes del tenant | Presunto generador / afectado |
| Rol en el hecho | Select por estudiante | Si | generador / afectado / testigo | Papel de cada involucrado |
| Tipo de situacion | Select | Si | I / II / III | Tipificacion fija por ley (RN-CVE-002) |
| Descripcion de los hechos | Texto largo | Si | Min 20 caracteres | Relato del caso |
| Hay dano al cuerpo o a la salud | Checkbox | Si | — | Si se marca, activa atencion en salud obligatoria (RN-CVE-005) |
| Justificacion de la clasificacion | Texto largo | Si | Min 15 caracteres | Queda en log; obligatoria tambien al reclasificar |
| Visibilidad del caso | Select | Si | interna (default) / partes | Restringida por defecto (RN-CVE-008) |

## D) Formulario "Generar acta del Comite" (RN-CVE-006)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Caso asociado | Select | Si | Caso tipo II o III existente | Caso que motiva la sesion |
| Fecha de la sesion | Fecha | Si | <= hoy | Cuando sesiono el comite |
| Asistentes | Multi-select | Si | Integrantes registrados del comite | Quorum de la composicion legal |
| Hechos | Texto largo | Si | Min 20 caracteres | Resumen de lo tratado |
| Decisiones y compromisos | Texto largo | Si | Min 15 caracteres | Acuerdos del comite |
| Acta firmada (PDF) | Archivo | Si | PDF; sujeto a cuota | Acta firmada por el Rector (inmutable al cargarse) |

## E) Formulario "Citar acudiente" (RF-28, configurable)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del tenant | Estudiante cuyo acudiente se cita |
| Motivo (interno) | Texto largo | Si | Min 10 caracteres | Visible solo internamente; no viaja en la notificacion (RN-BW-006) |
| Fecha y hora | Fecha-Hora | Si | Futura | Cuando es la citacion |
| Lugar / modalidad | Texto / Select | Si | presencial / virtual | Donde o como |
| Caso o anotacion vinculada | Select | No | Caso/anotacion existente | Trazabilidad del motivo |
| Canal de notificacion | Multi-select | Si | Canales habilitados por el colegio | Correo / portal / WhatsApp |

## F) Formulario "Generar reporte de convivencia" (RF-29)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Alcance | Select | Si | estudiante / grupo / tipo / fechas | Que agrupa el reporte |
| Estudiante o grupo | Select | Condicional | Segun el alcance elegido | Sujeto del reporte |
| Rango de fechas | Rango | Si | Dentro del ano lectivo | Periodo a reportar |
| Tipos de anotacion | Multi-select | No | Del catalogo | Filtro opcional |
| Formato de salida | Select | Si | PDF / pantalla | Como se entrega |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
