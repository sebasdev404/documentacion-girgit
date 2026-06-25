---
tags:
  - arquitectura
  - rol/rector
  - formularios
aliases:
  - Campos Formulario ROL-02
  - Rector Campos
---

# Campos del Formulario — Rector / Administrador del Colegio

Campos de cada formulario que opera el rol.

## A) Formulario "Identidad institucional" (RF-04)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre del colegio | Texto | Si | Min 3 caracteres | Razon social / nombre oficial |
| Nombre comercial | Texto | No | — | Como se muestra en la app |
| Logo | Archivo (imagen) | No | PNG/JPG, peso max segun cuota | Aparece en documentos y portal |
| NIT | Texto | Si | Formato NIT colombiano | Identificacion tributaria del colegio |
| Resolucion MEN | Texto | Si | — | Resolucion del Ministerio de Educacion Nacional |
| Codigo DANE | Texto | No | Formato DANE | Requerido para reportes oficiales |
| Direccion | Texto | Si | — | Sede principal |
| Telefono | Texto | Si | Formato telefono | Contacto institucional |
| Correo institucional | Email | Si | Formato email valido | Remitente de comunicaciones |

## B) Formulario "Calendario y periodos" (RF-05)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Calendario | Select | Si | Solo opciones habilitadas por el plan (A / B) | Calendario lectivo (RR-13) |
| Ano lectivo | Numero | Si | Ano valido, no duplicado | Periodo anual |
| Numero de periodos | Numero | Si | Entre 1 y el maximo configurado | Cuantos periodos tiene el ano |
| Fecha inicio de periodo | Fecha | Si | Dentro del ano lectivo, sin solape | Inicio de cada periodo |
| Fecha fin de periodo | Fecha | Si | Posterior al inicio, sin solape | Fin de cada periodo |
| Fecha de cierre de notas | Fecha | Si | <= fin del periodo | Limite para registrar notas |
| Fecha de entrega de boletines | Fecha | No | >= cierre de notas | Entrega oficial |

## C) Formulario "Jornadas y bloques horarios" (RF-06)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre de jornada | Texto | Si | Unico en el tenant | Manana / Tarde / Unica / Nocturna |
| Hora de inicio | Hora | Si | Anterior a la hora de fin | Inicio de la jornada |
| Hora de fin | Hora | Si | Posterior al inicio | Fin de la jornada |
| Duracion de bloque | Numero (min) | Si | > 0 | Minutos por bloque de clase |
| Recreos | Lista de rangos | No | Dentro de la jornada, sin solape | Descansos |
| Niveles asociados | Multi-select | Si | Niveles existentes | A que niveles aplica la jornada |

## D) Formulario "Escala valorativa" (RF-07)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tipo de escala | Select | Si | Numerica / Por imagenes | Define el modo de valoracion |
| Valor minimo | Numero | Condicional (numerica) | < valor maximo | Extremo inferior (p. ej. 1.0) |
| Valor maximo | Numero | Condicional (numerica) | > valor minimo | Extremo superior (p. ej. 5.0) |
| Decimales | Numero | Condicional (numerica) | 0 a 2 | Precision de la nota |
| Niveles de desempeno | Lista | No | Rangos sin solape, cubren el espectro | Bajo / Basico / Alto / Superior |
| Imagenes de escala | Archivo (imagen) x N | Condicional (por imagenes) | PNG/JPG | Caritas/iconos para preescolar |
| Numero de niveles (imagenes) | Numero | Condicional (por imagenes) | >= 2 | Cuantos niveles tiene la escala |

## E) Formulario "Metodo de aprobacion" (RF-08)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Metodo de calculo | Select | Si | Promedio / Ponderado / Sumatoria dividida | Como se calcula la nota final |
| Nota minima de aprobacion | Numero | Si | Dentro del rango de la escala | Umbral de aprobacion |
| Redondeo | Select | No | Sin redondeo / 1 decimal / 2 decimales | Como se redondea la nota |
| Ponderaciones | Lista (campo + %) | Condicional (ponderado) | Suman 100% | Pesos por componente |

## F) Formulario "Crear usuario" (RF-10)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombres y apellidos | Texto | Si | Min 3 caracteres | Nombre completo |
| Tipo de documento | Select | Si | Lista (CC, TI, CE, etc.) | Documento de identidad |
| Numero de documento | Texto | Si | Unico en el tenant | Identificacion |
| Correo | Email | Si | Formato valido, unico en el tenant | Recibe el acceso |
| Rol | Select | Si | Rol existente del tenant | Rol principal (RR-04) |
| Complemento Director de Grupo | Checkbox | No | Solo si el rol es Docente | Permisos adicionales sobre el grupo dirigido |
| Grupo / materias | Multi-select | Condicional | Existentes en el tenant | Asignaciones (segun rol) |
| Estado | Select | Si | Activo / Inactivo | Estado inicial |

## G) Formulario "Asignar / ajustar permisos de rol" (RF-09, RR-05)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Rol | Select | Si | Rol existente | Rol a configurar |
| Nombre visible | Texto | No | Min 3 caracteres | Renombrar el rol |
| Permisos configurables | Toggles | No | Solo los marcados como configurables | Activar / desactivar |
| Esquema de coordinacion | Select | Condicional | Separados / Combinado (RR-12) | Mutuamente excluyentes |

## H) Formulario "Editar nota post-cierre" (RF-17, RR-07)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Estudiante / materia / periodo | Selectores | Si | Existentes y con periodo cerrado | Que nota se edita |
| Nuevo valor | Numero | Si | Dentro de la escala | Nota corregida |
| Justificacion | Texto largo | Si | Min 10 caracteres | Motivo del cambio (queda en log) |

## I) Formulario "Comunicado al colegio" (RF-42)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Titulo | Texto | Si | Min 3 caracteres | Asunto del comunicado |
| Mensaje | Texto largo | Si | No vacio | Cuerpo |
| Audiencia | Multi-select | Si | Grupos / roles / colegio entero | Destinatarios |
| Canal | Multi-select | Si | Portal / Correo / SMS (RI-03, RI-04) | Por donde se envia |
| Adjuntos | Archivo x N | No | Tipos permitidos, peso segun cuota | Documentos anexos |
| Programar envio | Fecha/hora | No | >= ahora | Envio diferido |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
