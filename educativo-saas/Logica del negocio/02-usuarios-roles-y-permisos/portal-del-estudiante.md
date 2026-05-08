---
titulo: Portal del estudiante
modulo: usuarios-roles-y-permisos
tipo: referencia
estado: borrador
tags: [portal, estudiante, acudiente]
---

# Portal del estudiante

Espacio web por el cual el estudiante (y opcionalmente el acudiente) consume y gestiona la información que le pertenece dentro del colegio.

## Acceso

- El estudiante accede con usuario y contraseña a través del subdominio o dominio del colegio.
- No hay restricción de acceso por nivel educativo: tanto un estudiante de preescolar como uno de bachillerato tienen el mismo tipo de acceso. El uso que se le dé al portal es responsabilidad del estudiante o de quien lo use en su nombre.
- El acceso al portal **puede desactivarse completamente por configuración del colegio** si la institución decide no habilitarlo para sus estudiantes.

## Funcionalidades disponibles

| Funcionalidad | Descripción |
| --- | --- |
| Consultar notas | Por materia y por periodo. |
| Descargar boletines | Boletines de los periodos cursados y boletín final. |
| Ver registro de asistencia | Conteo y detalle por materia y periodo. |
| Justificar inasistencias | Adjuntando explicación y soporte opcional. |
| Leer comunicados y publicaciones | Solo los que correspondan al alcance del estudiante (institución, nivel, grado, grupo, materias inscritas). |
| Solicitar citas | Con docentes o coordinación. |
| Confirmar boletines digitalmente | Cuando el colegio lo exige. Registro de fecha, hora e IP. |
| Consultar observador disciplinario | Solo lectura. |
| Ver horario de clases | Detalle por día de la semana y bloque. |
| Consultar historial de pagos | Conceptos pagados y pendientes. |
| Pagar pensión y otros conceptos | A través de las pasarelas configuradas por el colegio. |
| Descargar certificados y constancias | Sujeto a paz y salvo y, si aplica, a pago previo del concepto. |

## Restricciones

- El estudiante **no puede modificar ningún dato académico, disciplinario ni administrativo** del sistema.
- Solo consume y gestiona lo que le pertenece directamente.
- Toda acción del estudiante (justificación de inasistencia, confirmación de boletín, pago, solicitud de cita) queda registrada.

## Acceso del acudiente

- El acudiente accede al portal del colegio con sus propias credenciales.
- Ve los datos del estudiante (o estudiantes) que tiene vinculados.
- Las funcionalidades disponibles para el acudiente las define el colegio en la matriz de permisos. Por defecto: ver notas, asistencia, observador, boletines, comunicados y pagos del estudiante a su cargo.
- El acudiente **no puede** modificar datos académicos ni disciplinarios.

## Reglas de negocio

- **RN-PE-001 — Acceso desactivable:** el colegio puede desactivar el portal del estudiante completamente desde su configuración. Si está desactivado, los estudiantes no pueden iniciar sesión.
- **RN-PE-002 — Solo lectura para datos académicos y disciplinarios:** el estudiante y el acudiente nunca pueden modificar notas, asistencia ni observador.
- **RN-PE-003 — Bloqueo de documentos por paz y salvo:** la descarga de boletines, certificados y constancias puede estar bloqueada según la configuración de paz y salvo del colegio (ver [[../06-monetizacion-y-pagos/paz-y-salvo|Paz y salvo]]).
- **RN-PE-004 — Confirmación de boletín auditada:** la confirmación digital de un boletín registra fecha, hora e IP, y queda asociada al usuario que la realizó.
- **RN-PE-005 — Justificaciones requieren revisión:** una inasistencia justificada por el estudiante queda en estado pendiente hasta que el docente o coordinador la apruebe o rechace.
- **RN-PE-006 — Pago obligatorio antes de descarga:** los conceptos cobrables (certificados, constancias) requieren pago confirmado antes de habilitar la descarga.

## Notificaciones que llegan al portal

- Publicación de notas de un periodo.
- Registro de una inasistencia.
- Disponibilidad de un nuevo boletín.
- Publicación de un comunicado o agenda con alcance al estudiante.
- Confirmación de un pago.
- Aprobación o rechazo de un documento durante el proceso de matrícula.
- Aprobación o rechazo de una justificación de inasistencia.

Detalle en [[../05-comunicacion/notificaciones|Notificaciones]].

## Notas y pendientes

- Definir si el portal soporta sesión multi-estudiante para acudientes con varios hijos en el mismo colegio (recomendado: sí, con selector de estudiante).
- Validar accesibilidad para usuarios con conexión limitada (uso de datos, modo offline parcial).
