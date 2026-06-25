---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
aliases:
  - Arquitectura ROL-05
  - Wireframe Coord. Combinado
---

# Arquitectura — Coordinador Academico y Convivencia

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-05 (combinado). Une en un solo perfil la operacion academica del [[../02 - Coordinador Academico/00 - Arquitectura Coordinador Academico|Coord. Academico (ROL-03)]] y el seguimiento de convivencia del [[../03 - Coordinador de Convivencia/00 - Arquitectura Coordinador de Convivencia|Coord. de Convivencia (ROL-04)]].

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/04-coordinador-academico-y-convivencia.md`, mas las secciones `Logica del negocio/04-procesos-academicos/`, `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md` y `Logica del negocio/12-bienestar-y-servicios/bienestar-y-orientacion.md`.

---

## N0 — Inicio (login del colegio)

El coordinador combinado entra por el **subdominio de su colegio** (RR-06). No tiene URL de plataforma; opera dentro de un unico tenant.

```
[ micolegio.plataforma.com ]
        |
        v
  Login (correo + contrasena)
        |
        +--- credenciales invalidas --> mensaje generico + registro en log
        |
        +--- tenant suspendido --------> pantalla "colegio suspendido"
        |
        v
  Dashboard del tenant (vista academica + convivencia)
```

- El `tenant_id` se infiere del subdominio antes de validar credenciales (RR-06).
- Toda accion sensible (notas, observador, cierre, citaciones) queda en el log del tenant (RR-03).

---

## HEADER (presente en toda la app)

```
[ Logo Colegio ]   [ Buscador (estudiante / grupo / docente) ]   [ Ano lectivo + Periodo ]   [ Perfil ]   [ Notificaciones ]
```

- **Perfil del usuario:** datos del coordinador, cerrar sesion, preferencias.
- **Buscador:** busca estudiantes, grupos, materias y docentes del tenant (ve todo el tenant; nunca otro tenant — RR-01).
- **Selector de ano lectivo / periodo:** define el contexto de notas, consolidados y cierre.
- **Notificaciones:** cierres pendientes, nivelaciones generadas, casos de convivencia abiertos, citaciones por confirmar, alertas tempranas de riesgo.

---

## N1 — SIDEBAR (modulos del rol)

```
+-------------------------------+
|  Dashboard                    |
|  Plan de estudios             |
|  Grupos y asignaciones        |
|  Horarios                     |
|  Consolidados y cierre        |
|  Nivelaciones / Habilitaciones|
|  Boletines                    |
|  Observador del estudiante    |
|  Convivencia (Ley 1620)       |
|  Reportes de convivencia      |
|  Comunicaciones               |
+-------------------------------+
```

El coordinador combinado NO ve los modulos de configuracion base del tenant (escala valorativa, jornadas, calendario, modelo pedagogico) — eso es del Rector (ROL-02). Tampoco ve **Documentos Oficiales** (constancias, certificados, SIMAT) — eso es de Secretaria (ROL-06). El expediente completo de **Bienestar y orientacion** pertenece al Personal de Apoyo (ROL-09): el coordinador solo recibe y origina remisiones, no abre el expediente clinico (RN-BW-002).

---

## Detalle por modulo

### Dashboard

Vista de entrada que combina las dos coordinaciones. Tarjetas resumen:
- Estado del periodo (abierto / en cierre / cerrado) y porcentaje de notas cargadas por grupo.
- Grupos sin director de grupo asignado o sin horario completo.
- Nivelaciones / habilitaciones pendientes de nota.
- Casos de convivencia abiertos por tipo (I / II / III) y citaciones por confirmar.
- Alertas tempranas de riesgo (cruce asistencia + notas + observador) pendientes de revisar.

> Callout informativo: el dashboard es de solo lectura; cada accion se ejecuta en su modulo.

### Plan de estudios (RF-11)

- **Sub-vistas:** materias por grado / areas del conocimiento.
- **Filtros:** grado, area, ano lectivo, estado (activa / archivada).
- **Detalle:** intensidad horaria semanal, area a la que pertenece la materia.
- **Acciones:** Crear materia · Editar materia · Archivar materia · Asignar intensidad horaria · Asignar area.

**Como se usa este modulo:** al inicio del ano, el coordinador define que materias existen por grado, su intensidad horaria semanal y su area del conocimiento. Es la base sobre la que luego se construyen grupos, asignaciones y horarios. No puede tocar la escala valorativa ni el modelo pedagogico (eso es del Rector). (Ver [[Casos de Uso/RF-11 Gestionar plan de estudios|CU RF-11]].)

### Grupos y asignaciones (RF-12, RF-13, RF-14)

- **Sub-vistas:** lista de grupos / detalle de un grupo.
- **Filtros:** grado, ano lectivo, jornada.
- **Detalle:** estudiantes del grupo, materias, docente por materia, director de grupo designado.
- **Acciones:** Crear grupo · Editar grupo · Asignar docente a materia x grupo · Designar director de grupo · Quitar asignacion.
- Callout importante: el docente solo vera los grupos y materias que se le asignen aqui (RR-10); el director de grupo solo opera sobre el grupo que se le designa (RR-09).

**Como se usa este modulo:** crea los grupos por grado y ano, asigna el docente titular de cada materia x grupo y designa que docente sera director de cada grupo. Estas asignaciones alimentan los horarios, las notas, la asistencia y el observador. (Ver [[Casos de Uso/RF-13 Asignar docentes|CU RF-13]] y [[Casos de Uso/RF-14 Designar director de grupo|CU RF-14]].)

### Horarios (RF-15)

- **Sub-vistas:** horario por grupo / por docente / por aula.
- **Filtros:** grupo, docente, dia, bloque.
- **Detalle:** que docente dicta que materia, en que aula, en que bloque y dia.
- **Acciones:** Crear bloque · Editar bloque · Resolver choque · Publicar horario.
- Callout warning: el sistema detecta choques (docente o aula en dos lugares a la vez) y bloquea la publicacion hasta resolverlos.

**Como se usa este modulo:** sobre los grupos y asignaciones ya creados, el coordinador arma la malla horaria respetando la intensidad del plan de estudios y las jornadas/bloques que configuro el Rector. Publica el horario para que docentes y estudiantes lo vean. (Ver [[Casos de Uso/RF-15 Construir horarios de clase|CU RF-15]].)

### Consolidados y cierre (RF-18, RF-19, RF-20, RF-17)

- **Sub-vistas:** consolidado por grupo / consolidado de todos los grupos / panel de cierre.
- **Filtros:** grado, grupo, materia, periodo.
- **Detalle:** notas por estudiante x materia, faltantes, estudiantes en riesgo de perder.
- **Acciones:** Ver consolidado · Validar consolidado · Activar / ejecutar cierre de periodo · Editar nota tras el cierre (si el colegio lo habilito) con justificacion.
- Callout importante: editar una nota despues del cierre exige el permiso configurable activado + justificacion (RR-07); queda en el log.

**Como se usa este modulo:** al final del periodo revisa que todos los docentes hayan cargado notas, valida los consolidados y ejecuta el cierre. El cierre dispara automaticamente las nivelaciones de quienes perdieron materia. Puede ver el consolidado de todos los grupos del tenant. (Ver [[Casos de Uso/RF-20 Cierre de periodo|CU RF-20]].)

### Nivelaciones / Habilitaciones (RF-21)

- **Sub-vistas:** nivelaciones del periodo / habilitaciones del ano.
- **Filtros:** grupo, materia, estado (pendiente / en proceso / aprobada / no aprobada).
- **Detalle:** estudiante, materia, nota original, nota de recuperacion, plan de mejoramiento.
- **Acciones:** Ver procesos generados · Hacer seguimiento · Revisar plan de mejoramiento · Anular proceso con motivo.
- Callout informativo: los procesos los **genera el sistema** automaticamente al cierre (RN-NH-001); la **nota** la registra el docente titular (RN-NH-002), no el coordinador. El coordinador coordina y supervisa.

**Como se usa este modulo:** tras el cierre del periodo (nivelacion) o del ano (habilitacion), el coordinador supervisa que los docentes registren las notas de recuperacion dentro de la fecha limite y que los planes de mejoramiento queden cargados. (Ver [[Casos de Uso/RF-21 Nivelaciones y habilitaciones|CU RF-21]].)

### Boletines (RF-39)

- **Sub-vistas:** boletines por grupo / por estudiante.
- **Filtros:** grupo, periodo, estado (borrador / aprobado / publicado).
- **Detalle:** boletin del estudiante con notas, observaciones y consolidado del periodo.
- **Acciones:** Revisar boletin · Aprobar / firmar boletin (si el colegio lo habilito) · Devolver con observacion.
- Callout importante: aprobar/firmar boletines es un permiso **configurable** (puede quedar en el Rector). El boletin del grupo lo **genera** el Director de Grupo (RF-38); el coordinador lo **aprueba**.

**Como se usa este modulo:** cuando el colegio delega la firma al coordinador, este revisa los boletines generados por los directores de grupo y los aprueba para su publicacion a acudientes. (Ver [[Casos de Uso/RF-39 Aprobar boletines|CU RF-39]].)

### Observador del estudiante (RF-26, RF-27)

- **Sub-vistas:** observador de un estudiante / vista cronologica de anotaciones.
- **Filtros:** tipo de anotacion, estado (pendiente / confirmada / en apelacion / anulada), rango de fechas, autor.
- **Detalle:** anotaciones acumuladas del ano lectivo del estudiante, con su nivel de visibilidad (publica / docentes / interna — RN-OB-081).
- **Acciones:** Registrar anotacion en cualquier estudiante (RF-26) · Definir tipologias de anotacion (RF-27) · Cerrar / archivar anotacion · Anular con justificacion · Configurar visibilidad de la anotacion.
- Callout importante: la anotacion anulada se conserva como anulada con justificacion (RN-OE-003); el observador del ano cerrado es inmutable (RN-OE-004).

**Como se usa este modulo:** a diferencia del Director de Grupo (que solo escribe en su grupo) o el Docente (solo en sus materias), el coordinador combinado puede registrar anotaciones en el observador de **cualquier** estudiante del tenant y mantiene el catalogo de tipologias del colegio. (Ver [[Casos de Uso/RF-26 Registrar anotacion en observador de cualquier estudiante|CU RF-26]].)

### Convivencia (Ley 1620) (RF-28)

- **Sub-vistas:** casos de convivencia / clasificacion tipo I-II-III / Comite Escolar de Convivencia / Ruta de Atencion Integral.
- **Filtros:** tipo (I / II / III), estado (reportado / clasificado / en atencion / en comite / en seguimiento / cerrado), grupo, fecha.
- **Detalle:** caso con consecutivo, estudiantes involucrados, actuaciones del protocolo, plazos, acta del comite, acuerdos firmados.
- **Acciones:** Recibir y clasificar caso (tipo I/II/III, auditado — RN-CVE-002) · Activar protocolo segun el tipo · Citar formalmente a acudientes (RF-28, configurable) · Actuar como secretaria tecnica del Comite · Reclasificar con justificacion · Originar remision a orientacion.
- Callout warning: el coordinador clasifica y atiende, pero el **tipo III escala automaticamente al Rector** y no se cierra sin constancia de reporte a la autoridad (RN-CVE-004). La atencion en salud es prioritaria y bloquea el cierre (RN-CVE-005).

**Como se usa este modulo:** cuando un docente o director de grupo reporta una situacion, el coordinador la clasifica en tipo I/II/III, activa el protocolo de la Ruta de Atencion Integral, cita acudientes si el caso lo amerita y actua como secretaria tecnica del Comite Escolar de Convivencia. Todo acuerdo se refleja en el observador (RN-CVE-007). (Ver [[Casos de Uso/RF-28 Citar a acudientes|CU RF-28]].)

### Reportes de convivencia (RF-29)

- **Sub-vistas:** por estudiante / por grupo / por tipologia / por rango de fechas.
- **Filtros:** estudiante, grupo, tipo de anotacion, periodo.
- **Detalle:** consolidado de anotaciones y casos para seguimiento de reincidencia e informes institucionales.
- **Acciones:** Generar reporte · Descargar PDF · Preparar informe institucional para auditoria / SIUCE.
- Callout informativo: los reportes respetan la visibilidad por anotacion (RN-OE-005); los datos alimentan el reporte al SIUCE dentro de los reportes oficiales MEN.

**Como se usa este modulo:** el coordinador genera reportes de convivencia por estudiante o grupo para hacer seguimiento de casos recurrentes y preparar los informes de convivencia institucional. (Ver [[Casos de Uso/RF-29 Reportes de convivencia|CU RF-29]].)

### Comunicaciones

- **Sub-vistas:** mensajes con acudientes / notificaciones del sistema.
- **Filtros:** estudiante, grupo, tipo (citacion / informativo).
- **Acciones:** Comunicarse con acudientes via portal (RF-43) · Recibir notificaciones por correo (RF-44).
- Callout informativo: el coordinador combinado **no** envia comunicados a todo el colegio (RF-42 es del Rector); se comunica de forma dirigida con acudientes en el marco de un caso o un seguimiento academico.

**Como se usa este modulo:** soporta las citaciones y comunicados dirigidos a acudientes derivados de convivencia o de seguimiento academico, sin exponer informacion sensible en el cuerpo de la notificacion.

---

## Diferencias clave vs otros roles

| Aspecto | Coord. Academico (ROL-03) | Coord. Convivencia (ROL-04) | Coord. Combinado (ROL-05) | Rector (ROL-02) |
| --- | --- | --- | --- | --- |
| Plan de estudios / grupos / horarios | Si | No | Si | Si (puede absorber) |
| Consolidados y cierre de periodo | Si | No | Si | Si |
| Observador de cualquier estudiante | No (salvo combinado) | Si | Si | Si |
| Convivencia Ley 1620 (clasificar, RAI) | No | Si | Si | Preside el Comite |
| Configuracion base del tenant | No | No | No | Si |
| Documentos oficiales / SIMAT | No | No | No | No (es de Secretaria) |
| Coexistencia | Con ROL-04 separado | Con ROL-03 separado | Excluye ROL-03 + ROL-04 (RR-12) | Unico |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo |  Buscador est/grupo/doc  | Ano+Periodo | Perfil | Notif    |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Dashbrd|  [ Dashboard: estado de cierre + casos convivencia ]     |
| Plan   |  [ Materias por grado + intensidad + areas ]             |
| Grupos |  [ Grupos + asignacion docente + director de grupo ]     |
| Horario|  [ Malla horaria + deteccion de choques ]                |
| Consol.|  [ Consolidados por grupo + panel de cierre ]            |
| Nivel. |  [ Nivelaciones / habilitaciones generadas ]             |
| Boletin|  [ Aprobar / firmar boletines (configurable) ]           |
| Observ.|  [ Observador de cualquier estudiante + tipologias ]     |
| Conviv.|  [ Casos Ley 1620: clasificar I/II/III + RAI + Comite ]  |
| Reportes| [ Reportes de convivencia + informe institucional ]     |
| Comunic.| [ Citaciones y mensajes a acudientes ]                  |
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
- [[09 - Campos del Formulario]]
- [[10 - Validaciones]]
- [[11 - Respuestas del Sistema]]
- [[../02 - Coordinador Academico/00 - Arquitectura Coordinador Academico|Coord. Academico (ROL-03)]]
- [[../03 - Coordinador de Convivencia/00 - Arquitectura Coordinador de Convivencia|Coord. de Convivencia (ROL-04)]]
- [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/04-coordinador-academico-y-convivencia.md`
