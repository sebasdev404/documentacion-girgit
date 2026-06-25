---
tags:
  - arquitectura
  - rol/docente
  - ficha-detallada
aliases:
  - Ficha Detallada ROL-07
  - Docente Ficha Detallada
---

# Ficha Detallada — Docente

Ficha extendida para Sheet/Excel. Complementa [[01 - Ficha de Rol]].

| Campo | Valor |
|---|---|
| ID Rol | ROL-07 |
| Nombre | Docente |
| Alias | Profesor, Maestro |
| Tipo | Principal — Tenant (con complemento opcional [[../07 - Director de Grupo/01 - Ficha de Rol\|Director de Grupo]]) |
| Tipo de usuario | Profesor del colegio |
| Reporta a | Coordinador Academico (ROL-03) o Coordinador combinado (ROL-05); en ultima instancia al Rector (ROL-02) |
| Supervisa a | Estudiantes inscritos en los grupos y materias que tiene asignados |
| Ambito de datos | Tenant — limitado a SUS grupos y materias asignados (RR-10) |
| Cantidad sugerida | La que el colegio necesite; es el rol mas numeroso |
| Como se asigna | El Rector crea la cuenta; el Coordinador Academico asigna grupos y materias (RR-04) |
| Modulos que usa | Inicio (mis clases), Mis grupos y estudiantes, Notas, Asistencia, Observador academico, Mi horario, Salud (alertas de aula, configurable), Convivencia (reportar, configurable), Mensajes (configurable) |
| Permisos CRUD | Notas: Editar (solo materia asignada, periodo abierto) · Asistencia: Editar (sus clases) · Observador academico: Editar (su materia) · Horario: Ver · Estudiantes: Ver (sus grupos) · Alertas de salud autorizadas: Ver · Convivencia: Reportar |
| Permisos configurables | Editar notas despues del cierre (default OFF), Cargar evidencias, Comunicarse con acudientes via portal, Ver plan de estudios completo |
| Permisos negados | Consolidados generales, notas de materias que no dicta, observador disciplinario, configuracion del colegio, documentos oficiales, boletines, matricula, datos de otros tenants |
| MFA | No obligatorio (configurable por el colegio) |
| Acceso | Subdominio del colegio (no panel de plataforma) — RR-06 |
| Dispositivo | Mobile + desktop. Mobile predominante para asistencia y notas en clase |
| Frecuencia de uso | Diaria; es el rol con mayor uso operativo del sistema |
| Dolor / Necesidad actual | Cargar notas y asistencia rapido desde el aula sin fricciones; ver al instante a quien le falta nota; saber alergias/condiciones criticas autorizadas antes de una actividad; reportar una situacion de convivencia sin tener que clasificarla |
| Notas UX / Recomendaciones | Acciones rapidas desde el Home (tomar asistencia, ir a notas); planilla de notas optimizada para mobile; bloqueo claro y mensaje explicito cuando el periodo esta cerrado (RR-07); ocultar por completo en UI los modulos sin permiso (no mostrarlos deshabilitados); separar visualmente observador academico vs disciplinario para evitar confusiones |
| Reglas asociadas | RR-01, RR-02, RR-03, RR-06, RR-07, RR-09, RR-10; RN-CVE-002/003 (convivencia, reporta no clasifica); RN-SA-002/007 (salud, alertas autorizadas) |

## Variantes segun modelo pedagogico

| Modelo | Tipico en | Como lo presenta el sistema |
|---|---|---|
| Docente unico por salon | Primaria | Un solo grupo principal con muchas materias; suele ser tambien Director de Grupo |
| Docente con rotacion | Bachillerato | Horario con multiples grupos a lo largo del dia; dicta una o pocas materias |

> La variante NO cambia los permisos del docente, solo como el sistema le presenta su horario y sus grupos.

## Riesgos y controles

| Riesgo | Control |
|---|---|
| Acceso a datos de grupos/materias que no dicta | Filtro de visibilidad en backend por asignacion (RR-10); el buscador y los listados solo devuelven lo asignado |
| Edicion de notas fuera del periodo | Bloqueo por RR-07; reapertura solo si el colegio activa el permiso configurable, con justificacion obligatoria y auditada |
| Confusion entre observador academico y disciplinario | Separacion clara en UI; el docente no tiene acceso de escritura al disciplinario |
| Exposicion indebida de datos clinicos | Solo se muestran alertas autorizadas por el acudiente (RN-SA-007); nunca la ficha medica completa |
| Auto-clasificacion de un caso de convivencia | El docente solo reporta; la clasificacion tipo I/II/III es del Coordinador de Convivencia (RN-CVE-002) |

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/06-docente.md`
