---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
  - formularios
aliases:
  - Campos Formulario ROL-05
---

# Campos del Formulario — Coordinador Academico y Convivencia

Campos de cada formulario que opera el rol. Cubre los formularios academicos (heredados de ROL-03) y los de convivencia (heredados de ROL-04).

## A) Formulario "Crear / editar materia del plan de estudios" (RF-11)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre de la materia | Texto | Si | Min 3 caracteres, unica por grado | Nombre que veran docentes y estudiantes |
| Grado | Select | Si | Grado existente del tenant | A que grado pertenece |
| Area del conocimiento | Select | Si | Area del catalogo del colegio | Agrupacion de la materia |
| Intensidad horaria semanal | Numero | Si | > 0, coherente con la jornada | Horas/semana |
| Ano lectivo | Select | Si | Ano lectivo abierto | Contexto de la materia |
| Estado | Select | No | Activa / Archivada | Por defecto Activa |

## B) Formulario "Crear / editar grupo" (RF-12)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre del grupo | Texto | Si | Unico por grado y ano | Ej. "6A", "Once-2" |
| Grado | Select | Si | Grado existente | Grado del grupo |
| Ano lectivo | Select | Si | Ano lectivo abierto | Contexto del grupo |
| Jornada | Select | Si | Jornada configurada por el Rector | Manana / tarde / unica |
| Cupo maximo | Numero | No | > 0 | Capacidad del grupo |

## C) Formulario "Asignar docente a materia x grupo" (RF-13)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo | Select | Si | Grupo existente | Grupo objetivo |
| Materia | Select | Si | Materia del plan de ese grado | Materia a asignar |
| Docente | Select | Si | Usuario con rol Docente activo | Docente titular |
| Vigencia | Fecha | No | >= inicio del ano lectivo | Desde cuando aplica |

## D) Formulario "Designar director de grupo" (RF-14)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo | Select | Si | Grupo sin director o con cambio | Grupo a dirigir |
| Docente | Select | Si | Docente con asignacion en el tenant | Sera director de grupo |
| Motivo del cambio | Texto | No | Si reemplaza a otro, min 10 caracteres | Queda en log |

## E) Formulario "Bloque de horario" (RF-15)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Grupo | Select | Si | Grupo existente | Grupo del bloque |
| Materia | Select | Si | Materia asignada al grupo | Que se dicta |
| Docente | Select | Si | Docente asignado a esa materia x grupo | Quien dicta |
| Aula | Select | Si | Aula del catalogo, sin choque | Donde se dicta |
| Dia | Select | Si | Dia habil del calendario | Dia de la semana |
| Bloque horario | Select | Si | Bloque de la jornada, sin choque | Franja horaria |

## F) Formulario "Editar nota tras cierre" (RF-17)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del grupo | A quien se corrige |
| Materia | Select | Si | Materia del estudiante | Materia a corregir |
| Periodo | Select | Si | Periodo cerrado | Periodo afectado |
| Nueva nota | Numero | Si | Dentro de la escala valorativa del tenant | Valor corregido |
| Justificacion | Texto largo | Si | Min 10 caracteres | Obligatoria; queda en log (RR-07) |

## G) Formulario "Anotacion en el observador" (RF-26)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Cualquier estudiante del tenant | Sobre quien es la anotacion |
| Tipologia | Select | Si | Tipologia del catalogo (RF-27) | Llamado / compromiso / felicitacion / remision / suspension / etc. |
| Descripcion | Texto largo | Si | Min 10 caracteres | Detalle del hecho |
| Fecha del hecho | Fecha | Si | Dentro del ano lectivo | Cuando ocurrio |
| Visibilidad | Select | Si | Publica / docentes / interna (RN-OB-081) | Quien puede ver la anotacion |
| Requiere confirmacion | Checkbox | No | — | Solicita confirmacion al estudiante / acudiente |

## H) Formulario "Definir tipologia de anotacion" (RF-27)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre de la tipologia | Texto | Si | Unica en el catalogo | Ej. "Llamado de atencion", "Bullying" |
| Categoria base | Select | Si | Categoria base de plataforma | Academica / convivencia / salud / citacion |
| Gravedad | Select | No | Leve / grave / gravisima | Clasificacion interna del colegio |
| Visibilidad por defecto | Select | Si | Publica / docentes / interna | Nivel sugerido al crear anotaciones |

## I) Formulario "Clasificar caso de convivencia (Ley 1620)" (RF-28)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Caso | Select | Si | Caso reportado abierto | Caso a clasificar |
| Tipo | Select | Si | Tipo I / II / III (fijo por ley) | Determina el protocolo (RN-CVE-002) |
| Estudiantes involucrados | Multi-select | Si | Estudiantes del tenant | Generadores y afectados |
| Justificacion de la clasificacion | Texto largo | Si | Min 10 caracteres | Auditada; obligatoria al clasificar / reclasificar |

## J) Formulario "Citar formalmente a acudiente" (RF-28)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante | Select | Si | Estudiante del tenant | Estudiante del caso |
| Acudiente | Select | Si | Acudiente vinculado al estudiante | A quien se cita |
| Fecha y hora | Fecha/Hora | Si | Futura, dia habil | Cuando es la cita |
| Lugar | Texto | Si | Min 3 caracteres | Donde se atiende |
| Asunto (no sensible) | Texto | Si | Sin datos clinicos / sensibles | Motivo general visible al acudiente |
| Canal de notificacion | Select | Si | Canal habilitado por el colegio | Correo / portal / WhatsApp |

## K) Formulario "Generar reporte de convivencia" (RF-29)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Alcance | Select | Si | Estudiante / grupo / tipologia / fechas | Que agrega el reporte |
| Objetivo del alcance | Select | Condicional | Coherente con el alcance | Estudiante o grupo concreto |
| Rango de fechas | Fecha (rango) | No | Dentro del ano lectivo | Periodo del reporte |
| Formato | Select | Si | PDF / vista | Salida del reporte |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
