---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - validaciones
aliases:
  - Validaciones ROL-04
  - Coord. Convivencia Validaciones
---

# Validaciones — Coordinador de Convivencia

Casos de validacion y comportamiento del sistema.

## Registrar anotacion en observador (RF-26)

| Caso | Comportamiento del Sistema |
|---|---|
| Estudiante no seleccionado | Bloquea envio; muestra "Seleccione un estudiante" |
| Tipo de anotacion vacio | Bloquea envio; muestra "Seleccione el tipo de anotacion" |
| Descripcion < 15 caracteres | Bloquea envio; muestra "Describa el hecho (min 15 caracteres)" |
| Fecha del hecho fuera del ano lectivo abierto | Bloquea envio; muestra "La fecha debe estar dentro del periodo lectivo vigente" |
| Nivel de visibilidad no elegido | Bloquea envio; resalta el campo (RN-OB-081) |
| Intento de registrar en estudiante de otro tenant | Bloquea en backend; registra intento en log de seguridad (RR-01, RR-02) |
| Intento de editar anotacion de un ano cerrado | Bloquea; muestra "El observador de este ano esta cerrado" (RN-OE-004) |
| Anular sin justificacion | Bloquea; exige justificacion (la anotacion se conserva como anulada, RN-OE-003) |

## Definir tipologia (RF-27)

| Caso | Comportamiento del Sistema |
|---|---|
| Nombre de tipologia vacio o < 3 caracteres | Bloquea envio; muestra "Indique un nombre (min 3 caracteres)" |
| Nombre duplicado en el colegio | Bloquea envio; muestra "Ya existe una tipologia con ese nombre" |
| Inactivar una tipologia en uso | Permite, pero advierte: "Las anotaciones historicas conservan esta tipologia" |
| Intento de editar la tipificacion legal I/II/III | Bloquea; la tipificacion de casos es fija por ley, no editable (RN-CVE-003) |

## Clasificar / operar caso de convivencia (Ley 1620)

| Caso | Comportamiento del Sistema |
|---|---|
| Avanzar el caso sin clasificar el tipo | Bloquea; exige clasificacion en tipo I/II/III antes de continuar (RN-CVE-002) |
| Reclasificar sin justificacion | Bloquea; exige motivo; registra autor y fecha en log |
| Cerrar caso tipo III sin constancia de reporte a autoridad | Bloquea; muestra "Registre el reporte a la autoridad (entidad, fecha, radicado)" (RN-CVE-004) |
| Cerrar caso con dano al cuerpo sin remision a salud | Bloquea; muestra "Registre la atencion en salud antes de cerrar" (RN-CVE-005) |
| Cerrar caso con actuaciones obligatorias pendientes | Bloquea; lista las actuaciones faltantes del protocolo (RN-CVE-003) |
| Plazo de protocolo configurado por debajo del minimo legal | Bloquea al guardar; muestra "El plazo no puede ser inferior al exigido por la norma" (RN-CVE-010) |
| Editar un caso de un ano lectivo cerrado | Bloquea; solo consulta; exige reapertura autorizada (RN-CVE-009) |

## Comite Escolar de Convivencia

| Caso | Comportamiento del Sistema |
|---|---|
| Cerrar la configuracion del ano sin comite registrado | Bloquea; exige la composicion minima legal del comite (RN-CVE-001) |
| Generar acta de tipo II/III sin asistentes | Bloquea; el acta requiere asistentes y decisiones (RN-CVE-006) |
| Editar un acta ya firmada | Bloquea; el acta es inmutable una vez firmada por el Rector (RN-CVE-006) |

## Citacion a acudiente (RF-28, configurable)

| Caso | Comportamiento del Sistema |
|---|---|
| Permiso de citacion desactivado para el rol | Oculta la accion; si se intenta por API, backend la rechaza (RR-05, RR-02) |
| Fecha de la citacion en el pasado | Bloquea envio; muestra "La citacion debe programarse a futuro" |
| Sin canal de notificacion seleccionado | Bloquea envio; exige al menos un canal habilitado |
| Motivo sensible escrito en el cuerpo de la notificacion | El sistema no transmite el motivo al acudiente; solo fecha, hora y lugar (RN-BW-006) |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Acceso a notas / consolidados sin el permiso configurable activo | Oculta y bloquea; muestra "No tiene acceso al modulo academico" |
| Intento de acceder al expediente clinico de bienestar | Bloquea; solo orientacion ve el expediente completo (RN-BW-002) |
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Sesion en el subdominio de otro tenant | Rechaza autenticacion; el tenant se infiere del subdominio (RR-06) |
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
