---
tags:
  - arquitectura
  - rol/coord-academico
aliases:
  - Arquitectura ROL-03
  - Wireframe Coord. Academico
---

# Arquitectura — Coordinador Academico

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-03.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/02-coordinador-academico.md`.

---

## N0 — Inicio (login del colegio)

El Coordinador Academico entra por el **subdominio de su colegio** (RR-06), no por una URL de plataforma. El `tenant_id` se infiere del subdominio antes de validar credenciales.

```
[ colegio.plataforma.com ]
        |
        v
  Login (correo + contrasena)
        |
        +--- credenciales invalidas --> mensaje generico + registro en log
        |
        v
  Dashboard academico del colegio
```

- Solo ve datos de su propio tenant (RR-01).
- Todo intento de login (exito/fallo) queda en el log de auditoria del tenant.

---

## HEADER (presente en toda la app)

```
[ Logo del colegio ]   [ Buscador (grupos / docentes / estudiantes) ]   [ Periodo activo ]  [ Perfil ]  [ Notificaciones ]
```

- **Perfil del usuario:** datos del coordinador, cambiar contrasena, cerrar sesion.
- **Buscador:** busca por grupo, docente, materia o estudiante dentro del tenant.
- **Periodo activo:** semaforo del periodo lectivo en curso (Abierto / En cierre / Cerrado).
- **Notificaciones:** consolidados incompletos, periodos por cerrar, docentes sin notas cargadas, solicitudes de nivelacion.

---

## N1 — SIDEBAR (modulos del rol)

```
+---------------------------+
|  Dashboard academico      |
|  Plan de estudios         |
|  Grupos                   |
|  Asignacion docente       |
|  Horarios                 |
|  Consolidados de notas    |
|  Cierre de periodo        |
|  Nivelaciones             |
|  Boletines                |
|  Comunicaciones           |
+---------------------------+
```

El Coordinador Academico NO tiene en su sidebar la configuracion base del colegio (escala valorativa, jornadas, modelo pedagogico, calendario — eso es del Rector), ni el observador disciplinario (es del Coord. de Convivencia, salvo configuracion combinada), ni la emision de documentos oficiales (es de la Secretaria). Esos modulos no aparecen.

> Modulos como salud, bienestar, biblioteca, transporte, convivencia (Ley 1620) y admisiones no forman parte del sidebar de este rol: pertenecen a otros roles o a la configuracion del colegio. El Coordinador Academico solo participa en la operacion academica.

---

## Detalle por modulo

### Dashboard academico

Vista de entrada. Tarjetas resumen del estado academico del tenant:
- Periodo activo y dias restantes para el cierre.
- Grupos con consolidado completo / incompleto.
- Docentes con notas pendientes de cargar.
- Estudiantes en proceso de nivelacion / habilitacion.

> Callout informativo: el dashboard es de solo lectura; las acciones se ejecutan en cada modulo.

### Plan de estudios

- **Sub-vistas:** lista de materias por grado / detalle de una materia.
- **Filtros:** grado, area del conocimiento, ano lectivo.
- **Detalle:** materia, area, intensidad horaria semanal, grados a los que aplica.
- **Acciones:** Crear materia · Editar materia · Archivar materia (CRUD, RF-11).
- Callout importante: la escala valorativa y el metodo de aprobacion NO se editan aqui; son configuracion del Rector. El plan de estudios solo define que materias existen y con que intensidad.

**Como se usa este modulo:** al inicio del ano lectivo el coordinador arma el plan de estudios de cada grado, definiendo materias, area e intensidad horaria semanal. Este plan es la base sobre la que luego se crean grupos, se asignan docentes y se construyen horarios. (Ver [[05 - Requerimientos]] RF-11.)

### Grupos

- **Sub-vistas:** lista de grupos / detalle de un grupo.
- **Filtros:** grado, jornada, ano lectivo, estado del grupo.
- **Detalle:** grado, nombre del grupo, jornada, director de grupo, cantidad de estudiantes, materias del plan.
- **Acciones:** Crear grupo · Editar grupo · Archivar grupo (CRUD, RF-12).
- Callout: el coordinador crea la estructura del grupo; la asignacion del estudiante al grupo en la matricula es tipicamente de la Secretaria (permiso configurable para el coordinador).

**Como se usa este modulo:** para cada grado y ano lectivo el coordinador crea los grupos necesarios segun la cantidad de estudiantes, define su jornada y, mas adelante, designa al director de grupo. (Ver RF-12.)

### Asignacion docente

- **Sub-vistas:** matriz grupo x materia / vista por docente.
- **Filtros:** grupo, docente, materia, periodo.
- **Detalle:** que docente dicta que materia en que grupo; carga horaria por docente.
- **Acciones:** Asignar docente a materia/grupo · Reasignar · Designar director de grupo (Editar, RF-13 y RF-14).
- Callout importante: la asignacion determina lo que cada docente puede ver (RR-10: el docente solo ve sus grupos y materias asignados). Designar director de grupo activa sobre ese docente los permisos del complemento Director de Grupo (RR-09).

**Como se usa este modulo:** una vez creados los grupos, el coordinador asigna a cada materia el docente titular y designa para cada grupo su director de grupo. Esta asignacion habilita el acceso de cada docente y alimenta la construccion de horarios. (Ver RF-13, RF-14.)

### Horarios

- **Sub-vistas:** horario por grupo / horario por docente / horario por aula.
- **Filtros:** grupo, docente, aula, dia, jornada.
- **Detalle:** bloque horario, dia, materia, docente, aula.
- **Acciones:** Crear bloque · Editar bloque · Eliminar bloque · Publicar horario (CRUD, RF-15).
- Callout warning: el sistema advierte cruces de docente, aula o grupo en el mismo bloque antes de publicar.

**Como se usa este modulo:** el coordinador construye el horario de clase combinando la asignacion docente con las jornadas y bloques definidos por el Rector. El sistema valida que un docente, un aula o un grupo no queden en dos sitios a la vez. Al publicar, cada docente y estudiante ve su horario propio. (Ver RF-15.)

### Consolidados de notas

- **Sub-vistas:** consolidado por grupo / consolidado de todos los grupos.
- **Filtros:** grado, grupo, materia, periodo, estado (aprobado / perdido).
- **Detalle:** notas por estudiante y materia, promedios, materias perdidas, estudiantes en riesgo.
- **Acciones:** Ver consolidado del tenant completo (Ver, RF-18, RF-19) · Editar notas (Configurable, RF-17 — solo si el colegio lo habilita).
- Callout importante: por defecto el coordinador NO edita notas (eso es del docente titular); la edicion directa y la edicion despues del cierre son permisos configurables (RR-07).

**Como se usa este modulo:** el coordinador revisa los consolidados de todos los grupos para detectar grupos con notas incompletas, estudiantes en riesgo y materias perdidas, antes de coordinar el cierre del periodo. (Ver RF-18, RF-19.)

### Cierre de periodo

- **Sub-vistas:** estado de cierre por grupo / panel de cierre del periodo.
- **Filtros:** grupo, docente, estado del consolidado.
- **Detalle:** que grupos tienen consolidado completo, que docentes faltan por cargar notas, fecha limite.
- **Acciones:** Validar consolidados · Activar cierre · Desactivar cierre (Editar, RF-20).
- Callout warning: cerrar un periodo bloquea la edicion de notas para los docentes (RR-07); reabrirlo puede requerir intervencion del Rector segun configuracion del colegio.

**Como se usa este modulo:** cuando todos los grupos tienen el consolidado completo, el coordinador valida y activa el cierre del periodo. Esto congela las notas y habilita la generacion de boletines. (Ver RF-20.)

### Nivelaciones

- **Sub-vistas:** lista de estudiantes con materias perdidas / detalle de una nivelacion.
- **Filtros:** grado, grupo, materia, estado (pendiente / en curso / superada).
- **Detalle:** estudiante, materia perdida, docente, plan de nivelacion, resultado.
- **Acciones:** Abrir proceso de nivelacion/habilitacion · Registrar resultado · Cerrar proceso (Editar, RF-21).

**Como se usa este modulo:** al cerrar un periodo, el coordinador identifica a los estudiantes que perdieron materias y abre los procesos de nivelacion o habilitacion correspondientes, registrando el resultado una vez superados. (Ver RF-21.)

### Boletines

- **Sub-vistas:** boletines por grupo / detalle de un boletin.
- **Filtros:** grado, grupo, periodo, estado (generado / aprobado / publicado).
- **Detalle:** boletin del estudiante con notas consolidadas del periodo.
- **Acciones:** Generar boletin del grupo (Reportar, RF-39 relacionado) · Aprobar / firmar boletines (Configurable, RF-39) · Descargar PDF (Ver).
- Callout: la aprobacion/firma de boletines es un permiso configurable; puede quedar en el coordinador o delegarse al Rector. El coordinador NO emite documentos oficiales (constancias, certificados) — eso es de la Secretaria.

**Como se usa este modulo:** tras el cierre del periodo, el coordinador genera los boletines de los grupos a partir del consolidado y, si el colegio lo habilita, los aprueba/firma para publicarlos a los acudientes. (Ver RF-39.)

### Comunicaciones

- **Sub-vistas:** comunicados / mensajes con docentes y acudientes.
- **Detalle:** comunicados academicos (recordatorios de cierre, fechas de nivelacion).
- **Acciones:** Enviar comunicado (Configurable) · Mensajear acudientes via portal (Configurable, RF-43).
- Callout: ambas acciones son configurables; el envio de comunicados al colegio entero es tipicamente del Rector.

**Como se usa este modulo:** el coordinador comunica a docentes y acudientes los hitos academicos del periodo (fechas de cierre, jornadas de nivelacion, publicacion de boletines), si el colegio le habilita el permiso. (Ver RF-43.)

---

## Diferencias clave vs otros roles

| Aspecto | Coord. Academico (ROL-03) | Rector (ROL-02) | Coord. de Convivencia (ROL-04) |
| --- | --- | --- | --- |
| Configuracion base (escala, jornadas, calendario) | No la toca | La define | No la toca |
| Plan de estudios / grupos / horarios | CRUD | CRUD | No participa |
| Observador disciplinario | Sin acceso | Acceso total | Acceso total |
| Edicion de notas | Configurable | Editar | No participa |
| Aprobar / firmar boletines | Configurable | Aprobar | No participa |
| Documentos oficiales (constancias, certificados) | No emite | Supervisa | No emite |
| Cierre de periodo | Lo coordina | Lo supervisa | No participa |
| Ambito | Un solo tenant | Un solo tenant | Un solo tenant |

> Si el colegio fusiona ambas coordinaciones, usa el rol [[../04 - Coordinador Academico y Convivencia/00 - Arquitectura Coordinador Academico y Convivencia|Coord. combinado (ROL-05)]] en lugar de ROL-03 + ROL-04 (RR-12).

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo |  Buscador grupos/docentes | Periodo | Perfil | Notif       |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Dashbrd|  [ Dashboard academico: tarjetas resumen ]               |
| Plan   |  [ Plan de estudios: materias por grado + CRUD ]         |
| Grupos |  [ Grupos: lista + crear/editar ]                        |
| Asignac|  [ Matriz grupo x materia x docente ]                    |
| Horario|  [ Horario por grupo/docente/aula + validacion cruces ]  |
| Consol.|  [ Consolidados de notas del tenant ]                    |
| Cierre |  [ Panel de cierre de periodo ]                          |
| Nivelac|  [ Estudiantes con materias perdidas ]                   |
| Boletin|  [ Generar / aprobar boletines ]                         |
| Comunic|                                                          |
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
- [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/02-coordinador-academico.md`
