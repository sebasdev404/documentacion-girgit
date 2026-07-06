---
tags:
  - arquitectura
  - rol/docente
aliases:
  - Arquitectura ROL-07
  - Wireframe Docente
---

# Arquitectura — Docente

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-07.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/06-docente.md`. Tocan a este rol tambien `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md` (reporte de situaciones tipo I) y `Logica del negocio/12-bienestar-y-servicios/salud-y-enfermeria.md` (alertas de salud visibles a docencia).

---

## N0 — Inicio (login del colegio)

El Docente entra por el subdominio de SU colegio (RR-06). El `tenant_id` se infiere del subdominio antes de validar credenciales: aunque tuviera las mismas credenciales, no puede autenticarse en el portal de otro colegio.

```
[ micolegio.plataforma.com ]
        |
        v
  Login (correo + contrasena)
        |
        +--- credenciales invalidas --> mensaje generico + registro en log
        |
        +--- colegio suspendido --> pantalla "colegio suspendido"
        |
        v
  Home del Docente (mis clases de hoy)
```

- El sistema detecta el modelo pedagogico configurado por el colegio y arma el Home en consecuencia (ver "Variantes" mas abajo).
- Todo intento de login (exito/fallo) queda en el log de auditoria del tenant (RR-03).

---

## HEADER (presente en toda la app)

```
[ Logo Colegio ]   [ Buscador (mis estudiantes / mis grupos) ]      [ Periodo activo ]  [ Perfil ]  [ Notificaciones ]
```

- **Perfil del usuario:** datos del docente, cambiar contrasena, cerrar sesion. Sin acceso a configuracion del colegio.
- **Buscador:** acotado a SUS grupos y materias asignados (RR-10). No encuentra estudiantes ni grupos que no dicta.
- **Periodo activo:** indicador del periodo lectivo abierto. Si esta cerrado, la edicion de notas se bloquea (RR-07) salvo permiso configurable.
- **Notificaciones:** recordatorios de cierre de periodo, mensajes de acudientes (si esta habilitado), citaciones del Coordinador, alertas del Director de Grupo del salon.

---

## N1 — SIDEBAR (modulos del rol)

```
+-----------------------------+
|  Inicio (mis clases hoy)    |
|  Mis grupos y estudiantes   |
|  Notas                      |
|  Asistencia                 |
|  Observador academico       |
|  Mi horario                 |
|  Salud (alertas de aula)    |
|  Convivencia (reportar)     |
|  Mensajes                   |
+-----------------------------+
```

El Docente NO ve en su sidebar: Configuracion del colegio, Usuarios y roles, Plan de estudios, Matricula, Documentos oficiales, Boletines, Consolidados generales, Auditoria, Plataforma. Esos modulos no aparecen porque no tiene permiso (ver [[04 - Permisos Detallados]]).

> Los modulos "Salud (alertas de aula)" y "Convivencia (reportar)" solo aparecen si el colegio activa esos servicios. Son de **consulta/reporte**, no de gestion: el detalle clinico y la clasificacion de casos son de Personal de Apoyo y del Coordinador de Convivencia respectivamente.

---

## Detalle por modulo

### Inicio (mis clases de hoy)

Vista de entrada operativa. Tarjetas de las clases del dia segun el horario, en orden cronologico.

- Cada tarjeta: materia, grupo, aula, bloque horario y accion rapida "Tomar asistencia" / "Ir a notas".
- Pendientes del docente: notas por cargar antes del cierre, asistencias del dia sin registrar.
- Callout informativo: el Home es de solo lectura salvo las acciones rapidas; todo lo operativo vive en cada modulo.

**Como se usa este modulo:** el docente abre la app al iniciar la jornada y ve sus clases del dia en orden. Desde cada tarjeta salta directo a tomar asistencia o registrar notas, sin navegar el sidebar. Es la pantalla mas usada en mobile.

### Mis grupos y estudiantes

- **Sub-vistas:** lista de mis grupos / detalle de un grupo / ficha minima de un estudiante.
- **Filtros:** por grupo, por materia, por jornada.
- **Detalle del grupo:** listado de estudiantes inscritos en ESE grupo para la materia que dicta. Foto, nombre, codigo.
- **Detalle del estudiante (acotado):** nombre, su nota acumulada en MI materia, su asistencia en MIS clases, mis observaciones academicas. Si el colegio lo autoriza, alerta de salud (alergia/condicion critica).
- **Acciones:** Ver listado · Abrir notas del grupo · Abrir asistencia del grupo · Agregar observacion academica.
- Callout importante: el docente NO ve consolidados generales del grupo ni notas de materias que no dicta (RR-10). Solo el Director de Grupo del salon ve el consolidado completo.

**Como se usa este modulo:** el docente entra a un grupo para pasar lista, cargar notas de una evaluacion o dejar una observacion sobre un estudiante en su materia. Es su unica puerta a la informacion de estudiantes, siempre limitada a lo que dicta.

### Notas

- **Sub-vistas:** planilla de notas por grupo+materia / detalle por evaluacion.
- **Filtros:** periodo, tipo de evaluacion, grupo, materia.
- **Detalle:** planilla tipo grilla (estudiantes x evaluaciones) con la escala valorativa que configuro el Rector (numerica o por imagenes en preescolar).
- **Acciones:** Registrar nota · Editar nota (periodo abierto) · Cargar evidencia (si el colegio activa el modulo de evidencias) · Solicitar reapertura de edicion (si esta configurado).
- Callout warning: con el periodo CERRADO, la edicion se bloquea (RR-07). Solo si el colegio activo "editar notas despues del cierre" se permite, con justificacion obligatoria.

**Como se usa este modulo:** tras una evaluacion, el docente abre la planilla del grupo, carga las notas dentro del periodo abierto y el sistema recalcula automaticamente el acumulado del estudiante en la materia. (Ver [[Casos de Uso/RF-16 Registrar y editar notas en materia asignada|CU RF-16]].)

### Asistencia

- **Sub-vistas:** toma de asistencia de la clase del dia / historico de mis clases.
- **Filtros:** fecha, grupo, materia.
- **Detalle:** lista de estudiantes del grupo con estados: Presente / Ausente / Tarde / Excusa.
- **Acciones:** Registrar asistencia · Editar registro del dia · Marcar excusa.
- Callout informativo: la asistencia se toma sobre SUS clases.

**Como se usa este modulo:** al iniciar cada clase el docente pasa lista en mobile en segundos. El registro queda con fecha, hora y autor (RR-03). (Ver [[Casos de Uso/RF-22 Registrar asistencia en clase propia|CU RF-22]].)

### Observador academico

- **Sub-vistas:** observaciones que YO registre / nueva observacion.
- **Filtros:** estudiante, fecha, tipo.
- **Detalle:** anotacion academica por estudiante en MI materia (avances, dificultades, compromisos pedagogicos).
- **Acciones:** Agregar observacion academica · Editar la mia (mientras este abierta).
- Callout importante: esto es el observador ACADEMICO, no el disciplinario. El docente NO accede al observador disciplinario ni define sanciones; eso es del Coordinador de Convivencia y, parcialmente, del Director de Grupo.

**Como se usa este modulo:** el docente deja constancia del desempeno de un estudiante en su materia (refuerzo, compromiso, felicitacion academica). Queda asociado al estudiante con la visibilidad que el colegio configuro. (Ver [[Casos de Uso/RF-24 Observacion academica|CU RF-24]].)

### Mi horario

- **Sub-vistas:** vista semanal / vista del dia.
- **Detalle:** bloques de clase con materia, grupo y aula. Solo lectura: el horario lo construye el Coordinador.
- **Acciones:** Consultar · Exportar/descargar.
- Callout informativo: la forma del horario depende del modelo pedagogico (un solo grupo con muchas materias vs. rotacion entre grupos).

**Como se usa este modulo:** el docente consulta su carga de la semana y planifica. No puede editarlo; cualquier cambio lo gestiona el Coordinador Academico.

### Salud (alertas de aula)

- **Sub-vistas:** alertas de salud de mis estudiantes (solo las autorizadas) / remitir a enfermeria.
- **Detalle:** lista de alergias y condiciones criticas marcadas como visibles para docencia por el acudiente. Sin detalle clinico completo (RN-SA-002, RN-SA-007).
- **Acciones:** Ver alerta de salud autorizada · Reportar/remitir un estudiante a enfermeria.
- Callout warning: el docente NUNCA ve la ficha medica completa. Solo ve la alerta que el acudiente autorizo exponer a docentes. El detalle es de Personal de Apoyo / enfermeria.

**Como se usa este modulo:** antes de una salida o actividad fisica el docente revisa si algun estudiante tiene una alergia o condicion critica autorizada. Si un estudiante se siente mal en clase, lo remite a enfermeria con un toque; el Personal de Apoyo recibe el reporte.

### Convivencia (reportar)

- **Sub-vistas:** reportar situacion observada en aula / mis reportes.
- **Detalle:** formulario de reporte de una situacion de convivencia (Ley 1620). El docente reporta; NO clasifica el tipo (eso es del Coordinador de Convivencia).
- **Acciones:** Reportar situacion (tipo I la resuelve en aula con medida pedagogica) · Marcar "presunto delito" para escalar de inmediato al Rector (tipo III).
- Callout importante: clasificar tipo I/II/III, abrir el caso, citar acudientes y firmar actas NO es del docente (RN-CVE-002, RN-CVE-003). El docente es el reportante y aplica medidas pedagogicas inmediatas en tipo I.

**Como se usa este modulo:** cuando ocurre una situacion en el aula, el docente la reporta desde aqui o desde el observador. El sistema enruta el reporte al Coordinador de Convivencia para su clasificacion. Si percibe un presunto delito, lo marca y el sistema escala al Rector y restringe la visibilidad del caso.

### Mensajes

- **Sub-vistas:** bandeja / nuevo mensaje a acudiente (si esta habilitado).
- **Detalle:** comunicacion con acudientes de SUS estudiantes via portal, cuando el colegio lo permite. Algunos colegios lo restringen y obligan a canales formales.
- **Acciones:** Leer mensaje · Responder · Iniciar mensaje (configurable, RF-43).
- Callout informativo: este permiso es configurable. Si el colegio lo desactiva, el docente solo recibe notificaciones y no inicia conversaciones con acudientes.

**Como se usa este modulo:** si el colegio lo habilita, el docente responde dudas del acudiente sobre el desempeno del estudiante en su materia. Toda comunicacion queda registrada.

---

## Diferencias clave vs otros roles

| Aspecto | Docente (ROL-07) | Director de Grupo (ROL-08, complemento) | Coordinador Academico (ROL-03) |
| --- | --- | --- | --- |
| Alcance de visibilidad | Solo SUS materias y grupos asignados | Su materia + consolidado del grupo dirigido | Todos los grupos del colegio |
| Notas | Edita las de su materia | + ve consolidado del grupo | Coordina cierre, edita post-cierre |
| Observador | Solo el academico | + anotaciones del grupo dirigido | Define tipologias (segun esquema) |
| Boletines | No participa | Genera/observa el del grupo dirigido | Aprueba/firma |
| Consolidados generales | No los ve (RR-10) | Solo el de su grupo | De todos los grupos |
| Convivencia | Reporta (no clasifica) | Reporta + acompana al estudiante | Clasifica (si es combinado ROL-05) |
| Configuracion | Sin acceso | Sin acceso | Plan de estudios y horarios |

> El complemento [[../07 - Director de Grupo/01 - Ficha de Rol|Director de Grupo]] NO cambia el rol base: suma permisos solo sobre el grupo dirigido (RR-09). En sus demas grupos sigue siendo Docente sobre sus materias.

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo | Buscador (mis grupos)     | Periodo | Perfil | Notif        |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                              |
|        |                                                         |
| Inicio |  [ Mis clases de hoy: tarjetas por bloque ]             |
| Grupos |  [ Lista de estudiantes de MIS grupos + filtros ]       |
| Notas  |  [ Planilla notas (estudiantes x evaluaciones) ]        |
| Asist. |  [ Lista P/A/T/E del grupo de la clase ]                |
| Observ |  [ Observaciones academicas por estudiante ]            |
| Horario|  [ Semana: materia/grupo/aula/bloque (solo lectura) ]   |
| Salud  |  [ Alertas autorizadas + remitir a enfermeria ]         |
| Conviv |  [ Reportar situacion (no clasifica) ]                   |
| Mensaj |  [ Bandeja acudientes (configurable) ]                   |
+--------+---------------------------------------------------------+
```

---

## Relacionado

- [[01 - Ficha de Rol]]
- [[02 - Ficha Detallada]]
- [[03 - PRD]]
- [[04 - Permisos Detallados]]
- [[05 - Requerimientos]]
- [[06 - Resumen Rapido]]
- [[07 - Feature Map]]
- [[08 - Acciones del Usuario]]
- [[../07 - Director de Grupo/01 - Ficha de Rol|Director de Grupo (complemento)]]
- [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/06-docente.md`
