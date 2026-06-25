---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
aliases:
  - Arquitectura ROL-04
  - Wireframe Coord. Convivencia
---

# Arquitectura — Coordinador de Convivencia

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-04.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia.md`, `Logica del negocio/04-procesos-academicos/observador-del-estudiante.md`, `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md` y `Logica del negocio/12-bienestar-y-servicios/bienestar-y-orientacion.md`.

---

## N0 — Inicio (login del colegio)

El Coordinador de Convivencia entra SIEMPRE por el subdominio de su colegio (RR-06). No tiene acceso cross-tenant.

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
  Dashboard de Convivencia (del tenant)
```

- El `tenant_id` se infiere del subdominio antes de validar credenciales (RR-06).
- Todo intento de login (exito/fallo) queda en el log de auditoria del tenant (RR-03).
- Si el colegio usa el esquema combinado (ROL-05), este rol no existe por separado (RR-12).

---

## HEADER (presente en toda la app)

```
[ Logo Colegio ]   [ Buscador de estudiantes ]      [ Casos abiertos ]  [ Perfil ]  [ Notificaciones ]
```

- **Perfil del usuario:** datos del coordinador, cerrar sesion, preferencias de notificacion.
- **Buscador:** busca estudiantes del tenant por nombre, documento o grupo para abrir su observador.
- **Casos abiertos:** contador de casos de convivencia (Ley 1620) que tiene a su cargo sin cerrar.
- **Notificaciones:** anotaciones que requieren su confirmacion, casos escalados, citaciones proximas, casos tipo III pendientes de reporte, vencimiento de plazos de protocolo.

---

## N1 — SIDEBAR (modulos del rol)

```
+-------------------------------+
|  Dashboard de Convivencia     |
|  Observador del estudiante    |
|  Casos de convivencia (1620)  |
|  Comite Escolar de Convivencia|
|  Tipologias y catalogos       |
|  Citaciones a acudientes      |
|  Reportes de convivencia      |
|  Bienestar / Orientacion (*)  |
|  Comunicados (*)              |
+-------------------------------+
```

- (*) Modulos configurables: el colegio decide si los habilita para este rol.
- El Coordinador de Convivencia NO tiene en su sidebar modulos academicos operativos: notas, consolidados, horarios, plan de estudios, matricula ni documentos oficiales. Esos no aparecen.
- El acceso al modulo academico (notas) esta desactivado por defecto y solo se activa si el colegio unifica coordinaciones.

---

## Detalle por modulo

### Dashboard de Convivencia

Vista de entrada. Tarjetas resumen del estado de convivencia del colegio:
- Anotaciones registradas en el periodo (por tipo: leve / grave / gravisima).
- Casos de convivencia abiertos por tipo I / II / III.
- Estudiantes con observaciones reiteradas (casos cronicos).
- Citaciones de la semana.
- Alertas tempranas de riesgo enrutadas a convivencia (cruce de asistencia + observador, `RN-VA-101`).

> Callout informativo: el dashboard es de solo lectura; las acciones se hacen en cada modulo. Los datos respetan el aislamiento por tenant (RR-01).

### Observador del estudiante

- **Sub-vistas:** observador de un estudiante / vista por grupo / busqueda global.
- **Filtros:** tipo de anotacion (llamado de atencion, compromiso, felicitacion, remision, suspension), estado (pendiente de confirmacion, confirmada, en apelacion, anulada), rango de fechas, autor, nivel de visibilidad.
- **Detalle:** linea cronologica de anotaciones del estudiante en el ano lectivo, con autor, tipo, descripcion, nivel de visibilidad y estado de confirmacion del acudiente.
- **Acciones:** Registrar anotacion en cualquier estudiante (RF-26) · Editar anotacion propia dentro del periodo abierto · Anular anotacion con justificacion · Cerrar / archivar anotacion · Solicitar confirmacion al acudiente.
- Callout importante: la anulacion NO borra; conserva la anotacion como anulada con justificacion (RN-OE-003). El observador de un ano cerrado es inmutable (RN-OE-004).

**Como se usa este modulo:** cuando un docente o director de grupo reporta una situacion, el coordinador abre el observador del estudiante, registra el llamado de atencion o compromiso, elige el nivel de visibilidad (publica / docentes / interna, RN-OB-081) y, si la anotacion lo exige, solicita la confirmacion del acudiente desde el portal. (Ver [[Casos de Uso/RF-26 Registrar anotacion en observador|CU RF-26]].)

### Casos de convivencia (Ley 1620)

- **Sub-vistas:** lista de casos / detalle de un caso / bandeja de reportes recibidos.
- **Filtros:** tipo (I / II / III), estado (Reportado, Clasificado, En atencion, En comite, Reportado a autoridad, En seguimiento, Cerrado, Reabierto), responsable, rango de fechas.
- **Detalle:** consecutivo del caso, estudiantes involucrados (presunto generador / afectado), tipo, actuaciones del protocolo con plazos y responsables, acta del comite (si aplica), acuerdos firmados y constancia de reporte a autoridad (tipo III).
- **Acciones:** Recibir y clasificar situacion en tipo I/II/III (RN-CVE-002) · Reclasificar con justificacion · Ejecutar actuaciones del protocolo · Activar atencion en salud prioritaria · Registrar acuerdos y compromisos · Escalar al Rector (tipo III) · Cerrar caso en seguimiento.
- Callout warning: un caso tipo III escala automaticamente al Rector y NO puede cerrarse sin la constancia de reporte a la autoridad competente (RN-CVE-004). Si hay dano al cuerpo, la remision a EPS/urgencias bloquea el cierre (RN-CVE-005).

**Como se usa este modulo:** el coordinador actua como puerta de entrada del Sistema Nacional de Convivencia Escolar. Recibe el reporte, clasifica obligatoriamente el tipo (la clasificacion queda auditada), el sistema instancia el protocolo correspondiente con sus plazos, y el coordinador ejecuta las actuaciones, articula con orientacion y deja todo registrado en el observador. Para tipo II/III convoca el comite. (Ver [[Casos de Uso/RF-26 Registrar anotacion en observador|CU RF-26]] y la fuente `Logica del negocio/13-cumplimiento-colombia/convivencia-ley-1620.md`.)

### Comite Escolar de Convivencia

- Actua como **secretaria tecnica** del comite (configurable por colegio).
- **Sub-vistas:** integrantes del comite por ano lectivo / sesiones / actas.
- **Acciones:** Registrar integrantes (respetando la composicion minima legal) · Convocar sesion · Generar acta con asistentes, hechos, decisiones y compromisos · Cargar acta firmada.
- Callout importante: el acta es inmutable una vez firmada por el Rector (RN-CVE-006). El comite es obligatorio por colegio; el sistema impide cerrar la configuracion del ano sin el (RN-CVE-001). El Rector preside; este rol no firma actas, las prepara.

### Tipologias y catalogos

- Catalogo de tipos de anotacion del colegio (leve / grave / gravisima y categorias custom, RN-OB-080).
- Catalogo de medidas restaurativas y pedagogicas (base de plataforma + propias del colegio).
- **Acciones:** Definir tipologias de anotacion (RF-27) · Activar / desactivar categorias custom · Asociar medidas sugeridas a cada tipologia.
- Callout informativo: la tipificacion legal I/II/III de los casos de convivencia es FIJA por ley y no editable; lo configurable son las tipologias del observador, los plazos (dentro de topes legales) y el catalogo de medidas (RN-CVE-003, RN-CVE-010).

### Citaciones a acudientes

- **Permiso configurable:** puede ser exclusivo del Rector segun la politica del colegio.
- **Acciones:** Citar formalmente a un acudiente (RF-28) · Programar fecha/hora/lugar · Registrar resultado de la citacion · Vincular la citacion a un caso o anotacion.
- Callout warning: la notificacion de la citacion informa fecha, hora y lugar, pero nunca el contenido sensible del caso (RN-BW-006). El envio usa los canales habilitados por el colegio.

### Reportes de convivencia

- **Sub-vistas:** por estudiante (resumen anual) / por grupo / por tipo de anotacion / por rango de fechas.
- **Acciones:** Generar reporte de convivencia (RF-29) · Exportar a PDF · Generar informe disciplinario consolidado del estudiante (multi-ano).
- Callout informativo: los reportes respetan el alcance del rol y la visibilidad de cada anotacion (RN-OE-005). Los datos de convivencia alimentan el reporte consolidado para auditoria y SIUCE.

### Bienestar / Orientacion (configurable)

- El coordinador NO accede al expediente clinico completo de bienestar (RN-BW-002); ese es del Personal de Apoyo (ROL-09).
- **Acciones (configurable):** Recibir remisiones internas desde orientacion · Aportar contexto de convivencia a un caso · Autorizar acciones de acompanamiento de su competencia.
- Callout importante: la informacion sensible de orientacion (diagnosticos, hipotesis clinicas) no es visible para este rol salvo la parte del plan que el orientador marque como compartida (RN-BW-008).

### Comunicados (configurable)

- **Permiso configurable:** el colegio decide si este rol puede enviar comunicados al colegio entero o solo mensajes via portal a acudientes.
- **Acciones (configurable):** Enviar comunicado de convivencia al colegio · Comunicarse con un acudiente via portal.

---

## Diferencias clave vs otros roles

| Aspecto | Coord. Convivencia (ROL-04) | Coord. Academico (ROL-03) | Coord. Combinado (ROL-05) |
| --- | --- | --- | --- |
| Ambito | Convivencia y disciplina | Plan academico, notas, horarios | Ambos ambitos |
| Observador disciplinario | Anota en cualquier estudiante | No participa | Anota en cualquier estudiante |
| Notas academicas | Sin acceso (salvo config) | Acceso (editar/cierre) | Acceso |
| Casos Ley 1620 | Clasifica y opera | No | Clasifica y opera |
| Tipologias de anotacion | Las define | No | Las define |
| Coexistencia | Excluyente con ROL-05 (RR-12) | Excluyente con ROL-05 (RR-12) | Excluye a ROL-03 + ROL-04 |

| Aspecto | Coord. Convivencia (ROL-04) | Director de Grupo (ROL-08) |
| --- | --- | --- |
| Alcance del observador | Cualquier estudiante del tenant | Solo su grupo dirigido |
| Clasificacion de casos | Si (es su rol) | Solo reporta situaciones |
| Define tipologias | Si | No |
| Genera reportes de convivencia | Si | No (consulta su grupo) |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo | Buscador estudiantes      | Casos | Perfil | Notif         |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Dashbrd|  [ Dashboard convivencia: tarjetas + alertas ]           |
| Observ.|  [ Observador estudiante: linea cronologica + filtros ]  |
| Casos  |  [ Caso 1620: tipo, protocolo, actuaciones, plazos ]     |
| Comite |                                                          |
| Tipolog|                                                          |
| Citac. |                                                          |
| Reporte|                                                          |
| Bienest|  (*) configurable                                        |
| Comunic|  (*) configurable                                        |
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
- Rol combinado relacionado: [[../04 - Coordinador Academico y Convivencia/01 - Ficha de Rol|Coord. Academico y Convivencia (ROL-05)]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia.md`
