---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
aliases:
  - Arquitectura ROL-09
  - Wireframe Estudiante y Acudiente
---

# Arquitectura — Estudiante / Acudiente

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-09.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente.md` y `Logica del negocio/02-usuarios-roles-y-permisos/portal-del-estudiante.md`.

> Aclaracion estructural (RN-TU-410 / RR-11): el acudiente NO es un usuario aparte. El menor tiene UNA sola cuenta — la del Estudiante — y el acudiente la opera de hecho con esas mismas credenciales. No hay perfil ni login propio del acudiente. Por eso "Estudiante" y "Acudiente" comparten esta arquitectura: misma pantalla, mismo permiso de solo lectura; lo unico que cambia es quien esta del otro lado del teclado.

---

## N0 — Inicio (login del portal del colegio)

El Estudiante/Acudiente entra por el subdominio del propio colegio (RR-06). No existe URL de plataforma para este rol; el tenant_id se infiere del subdominio antes de validar credenciales.

```
[ micolegio.plataforma.com ]
        |
        v
  Login (usuario + contrasena)
        |
        +--- portal desactivado por el colegio (RN-PE-001) --> "El portal no esta habilitado"
        |
        +--- credenciales invalidas --> mensaje generico + registro en log de seguridad
        |
        +--- primer ingreso (RN-AU-360) --> cambio obligatorio de contrasena temporal
        |
        v
  ?Una sola cuenta de estudiante asociada al correo?
        |
        +--- Si  --> Dashboard del estudiante
        |
        +--- No (varios hijos, mismo correo) --> Selector de estudiante (RR-14 / RN-CP-002)
                                                       |
                                                       v
                                                 Dashboard del estudiante elegido
```

- MFA opcional para este rol y para el Superadministrador. El colegio puede desactivar el portal por completo (RN-PE-001): las cuentas existen pero no pueden iniciar sesion.
- El selector de estudiante NO fusiona expedientes, permisos ni pagos entre hermanos (RR-14, RN-CP-002, RN-PP-120). Cada cuenta se opera por separado.
- Todo intento de login (exito/fallo) queda en el log de auditoria del tenant.

---

## HEADER (presente en toda la app)

```
[ Logo Colegio ]  [ Selector de estudiante v ]      [ Buscador ]  [ Notificaciones ]  [ Perfil ]
```

- **Selector de estudiante:** visible solo cuando el correo esta vinculado a varios estudiantes (acudiente con varios hijos). Cambia el contexto completo de la sesion; no mezcla datos (RR-14).
- **Buscador:** acotado a lo propio (una materia, un comunicado, un boletin del estudiante en contexto). Nunca devuelve datos de otros estudiantes (RR-14).
- **Notificaciones:** buzon del portal — notas publicadas, inasistencias, boletin disponible, comunicados, confirmacion de pago, aprobacion/rechazo de documento o de justificacion (ver `Logica del negocio/05-comunicacion/notificaciones.md`).
- **Perfil:** datos de contacto del estudiante y del/los acudiente(s), cambio de contrasena, preferencias de notificacion (dentro de los limites del colegio, RN-NO-004). El perfil es mayormente de solo lectura; los datos academicos no se editan aqui.

---

## N1 — SIDEBAR (modulos del rol)

```
+---------------------------+
|  Inicio                   |
|  Notas                    |
|  Horario                  |
|  Asistencia               |
|  Boletines                |
|  Observador               |
|  Comunicaciones           |
|  Pagos y estado de cuenta |
|  Documentos               |
|  Citas                    |
+---------------------------+
```

El Estudiante/Acudiente NO ve modulos de configuracion, usuarios, plan de estudios, ni datos de terceros. Todo su sidebar es de **consulta** y de **gestion de lo propio** (justificar inasistencia, pagar, solicitar documento/cita). Varios modulos son **configurables por el colegio**: si el colegio los apaga, no aparecen (Observador — RN-OB-081; descarga de boletin — RN-PE-003; canal con docentes — RN-MI-180).

---

## Detalle por modulo

### Inicio

Vista de entrada del estudiante en contexto. Tarjetas resumen:
- Ultimas notas publicadas y promedio del periodo en curso.
- Proximas clases del dia (mini-horario).
- Estado de cuenta resumido (al dia / cuota proxima / en mora).
- Comunicados recientes con alcance al estudiante.
- Avisos accionables: "tienes 1 inasistencia sin justificar", "boletin del periodo disponible", "documento pendiente de cargue".

> Callout informativo: el Inicio es de solo lectura; cada accion se realiza dentro de su modulo. Lo que ve aqui depende del estudiante seleccionado en el header.

### Notas

- **Sub-vistas:** notas por materia / linea de tiempo por periodo.
- **Filtros:** periodo academico, materia, area.
- **Detalle:** notas por logro/indicador, observaciones academicas del docente, promedio por materia y consolidado del periodo (RF-45).
- **Acciones:** ninguna de escritura. Solo consultar y, si el colegio lo permite, descargar el detalle.
- Callout importante: el estudiante/acudiente nunca edita una nota (RN-PE-002). Si detecta un error, el canal es Citas o Comunicaciones, no el modulo de notas.

**Como se usa este modulo:** cuando el colegio publica las notas de un periodo, llega una notificacion al portal y al correo. El acudiente abre Notas, filtra por el periodo recien publicado y revisa materia por materia. Si una nota le sorprende, abre la observacion academica asociada o solicita una cita con el docente. (Ver RF-45 y `Logica del negocio/04-procesos-academicos/calificaciones.md`.)

### Horario

- **Sub-vistas:** semana / dia.
- **Filtros:** dia de la semana, jornada.
- **Detalle:** materia, docente, aula/bloque por dia del grupo del estudiante (RF-46).
- **Acciones:** consultar, exportar/imprimir el horario (si el colegio lo habilita).

**Como se usa este modulo:** el acudiente consulta el horario para saber que clases tiene su hijo cada dia. Es informativo y estable durante el periodo; si el colegio reorganiza horarios, el modulo refleja el cambio y llega notificacion.

### Asistencia

- **Sub-vistas:** resumen por materia / detalle cronologico.
- **Filtros:** periodo, materia, estado (presente / ausente / tardanza / justificada / pendiente).
- **Detalle:** conteo y detalle de inasistencias por materia y periodo.
- **Acciones:** **Justificar inasistencia** — adjuntar explicacion y soporte opcional. La justificacion queda en estado *pendiente* hasta que el docente o coordinador la apruebe o rechace (RN-PE-005).
- Callout warning: justificar no cambia por si mismo el estado de la inasistencia; requiere revision. El sistema notifica el resultado (aprobada/rechazada).

**Como se usa este modulo:** tras una ausencia, el acudiente entra a Asistencia, ubica la inasistencia, abre "Justificar", escribe el motivo y adjunta el soporte (incapacidad, etc.). Envia y la solicitud queda pendiente. Cuando el docente la resuelve, llega notificacion. (Ver RF-22 — registro de asistencia del docente — y el flujo de justificacion.)

### Boletines

- **Sub-vistas:** lista de boletines por periodo / boletin final.
- **Detalle:** boletin del periodo con notas, logros, observacion general del director de grupo, inasistencias (RF-47).
- **Acciones:** **Descargar PDF** (configurable, RN-PE-003) y **Confirmar boletin digitalmente** cuando el colegio lo exige.
- Callout importante: la descarga puede estar **bloqueada por paz y salvo / pago** (RN-PE-003, RN-PE-006, RN-PYS-150). La confirmacion del boletin registra fecha, hora e IP y queda asociada al usuario que la realizo (RN-PE-004).

**Como se usa este modulo:** al publicarse un boletin, llega notificacion. El acudiente lo abre, lo revisa y, si el colegio lo exige, marca "Confirmo que recibi y revise el boletin". Esa confirmacion queda auditada. Para descargar el PDF, si hay deuda y el colegio bloquea por paz y salvo, primero debe ponerse al dia en Pagos.

### Observador

- **Sub-vistas:** observador disciplinario / observaciones academicas (cronologico).
- **Filtros:** tipo de anotacion, estado, rango de fechas, autor.
- **Detalle:** anotaciones del observador del estudiante en solo lectura (RF-48, RN-OB-080).
- **Acciones:** consultar y, cuando una anotacion lo requiera, **confirmar la anotacion** (deja registro). No edita ni elimina anotaciones.
- Callout warning: **modulo configurable** — algunos colegios mantienen el observador como documento interno y no lo exponen en el portal (RN-OB-081). Si esta apagado, el modulo no aparece en el sidebar.

**Como se usa este modulo:** cuando se registra una anotacion que requiere confirmacion del acudiente, llega notificacion. El acudiente abre el Observador, lee la anotacion y la confirma. La confirmacion queda registrada con fecha. (Ver `Logica del negocio/04-procesos-academicos/observador-del-estudiante.md`.)

### Comunicaciones

- **Sub-vistas:** comunicados y agenda / mensajes con docentes (configurable).
- **Filtros:** alcance (institucion, nivel, grado, grupo, materia), leidos/no leidos, fecha.
- **Detalle:** comunicados y publicaciones con alcance al estudiante (institucion, nivel, grado, grupo, materias inscritas); adjuntos si los hay.
- **Acciones:** leer/marcar como leido; responder/escribir a docentes o coordinacion **solo si el colegio habilita el canal** (RN-MI-180); ajustar preferencias de notificacion (RN-NO-004).
- Callout importante: por defecto el canal con docentes esta restringido a comunicacion formal; para temas de cita, el camino es el modulo Citas.

**Como se usa este modulo:** el acudiente revisa los comunicados del colegio y los marca leidos. Si el colegio habilito mensajeria, puede escribir al docente por el canal formal; si no, el modulo es solo de lectura de comunicados.

### Pagos y estado de cuenta

- **Sub-vistas:** estado de cuenta / historial de pagos / cuotas pendientes.
- **Filtros:** concepto (matricula, pension, transporte, etc.), estado (pendiente / en proceso / pagado / vencido / en mora), periodo.
- **Detalle:** conceptos cobrables, valor, fecha de vencimiento, descuentos/becas aplicados, saldo a favor si lo hay (RN-PP-120, RN-PP-121).
- **Acciones:** **Pagar** por las pasarelas habilitadas por el colegio (RN-PP-003); **descargar comprobante** de pagos confirmados (RN-PP-006).
- Callout warning: la **deuda es unica por estudiante** (RN-PP-120) — no hay split entre acudientes; quien pague no es asunto del sistema. El estado del pago se confirma por **webhook de la pasarela**, no por el navegador (RN-PP-003).

**Como se usa este modulo:** el acudiente entra a Pagos, ve la cuota pendiente, pulsa "Pagar", elige el medio (PSE, tarjeta, boton local) y completa el pago en la pasarela. Al confirmarse por webhook, la cuota pasa a Pagado, llega notificacion y el comprobante queda disponible. (Ver `Logica del negocio/06-monetizacion-y-pagos/pagos-de-pensiones.md`.)

### Documentos

- **Sub-vistas:** documentos requeridos (matricula) / certificados y constancias.
- **Detalle:**
  - **Cargue de documentos requeridos** durante matricula: subir archivo, ver estado (cargado / en revision / aprobado / rechazado) y recibir notificacion del resultado (RN-GD-270).
  - **Solicitar certificados/constancias/paz y salvo**: sujeto a paz y salvo y, si el concepto es cobrable, a **pago previo** (RN-PE-006, RN-PYS-150).
- **Acciones:** cargar documento; solicitar/descargar documento oficial.
- Callout importante: mientras exista deuda principal, ni siquiera se genera el cargo del certificado (RN-PYS-150). El paz y salvo no se exige para asistir a clases o consultar notas durante el ano en curso (RN-PZ-006).

**Como se usa este modulo:** en matricula, el acudiente sube los documentos pedidos y queda atento al resultado; si uno se rechaza, llega notificacion con el motivo y vuelve a cargarlo. Para un certificado de estudios, lo solicita, paga el costo si aplica, y lo descarga con su QR de verificacion.

### Citas

- **Sub-vistas:** solicitar cita / mis citas.
- **Detalle:** solicitudes de cita con docente o coordinacion, estado (solicitada / confirmada / reprogramada / cancelada).
- **Acciones:** **Solicitar cita** indicando con quien, motivo y disponibilidad; ver el estado de la solicitud.
- Callout informativo: la cita es el canal formal para temas que no se resuelven por comunicado (ej. duda sobre una nota o una anotacion del observador).

**Como se usa este modulo:** si el acudiente necesita hablar con el docente de matematicas, entra a Citas, elige al docente, escribe el motivo y propone horarios. El docente/coordinacion confirma y llega notificacion.

---

## Diferencias clave vs otros roles

| Aspecto | Estudiante/Acudiente (ROL-09) | Docente (ROL-07) | Director de Grupo (ROL-08) |
| --- | --- | --- | --- |
| Naturaleza | Solo consulta + gestion de lo propio | Operacion academica de sus materias | Complemento del Docente sobre su grupo |
| Notas | Solo ve las propias/del hijo | Registra y edita en su materia | Genera boletin del grupo |
| Asistencia | Justifica (queda pendiente de revision) | Registra en sus clases | Consulta la del grupo dirigido |
| Observador | Solo lee (si el colegio lo expone) y confirma | Registra observacion academica | Anota en el observador del grupo |
| Scope de datos | Solo el estudiante en contexto | Sus grupos y materias asignados | Su grupo + sus materias |
| Acudiente | Opera la misma cuenta, sin login propio | No aplica | No aplica |
| Entra por | Subdominio del colegio | Subdominio del colegio | Subdominio del colegio |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo | Selector estudiante v | Buscador | Notif | Perfil          |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Inicio |  [ Inicio: notas recientes · horario hoy · saldo · avisos]|
| Notas  |  [ Notas por materia y periodo (solo lectura) ]          |
| Horario|  [ Horario semanal del grupo ]                           |
| Asist. |  [ Asistencia + Justificar inasistencia ]                |
| Boletin|  [ Boletines + Confirmar + Descargar (paz y salvo) ]     |
| Observ.|  [ Observador (solo lectura · configurable) ]            |
| Comunic|  [ Comunicados + canal docentes (configurable) ]         |
| Pagos  |  [ Estado de cuenta + Pagar + Comprobantes ]             |
| Docum. |  [ Cargar documentos + Solicitar certificados ]          |
| Citas  |  [ Solicitar cita con docente/coordinacion ]             |
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
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente.md`
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/portal-del-estudiante.md`
