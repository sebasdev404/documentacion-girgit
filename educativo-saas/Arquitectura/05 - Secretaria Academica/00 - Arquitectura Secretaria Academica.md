---
tags:
  - arquitectura
  - rol/secretaria-academica
aliases:
  - Arquitectura ROL-06
  - Wireframe Secretaria
---

# Arquitectura — Secretaria Academica

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-06.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/05-secretaria-academica.md`, `Logica del negocio/13-cumplimiento-colombia/reportes-oficiales-men.md` (SIMAT) y `Logica del negocio/11-plataforma-y-operacion/gestion-documental.md` (consecutivos).

---

## N0 — Inicio (login del colegio)

La Secretaria entra por el subdominio del colegio (RR-06). El tenant se infiere del subdominio antes de validar credenciales.

```
[ colegio.subdominio.com ]
        |
        v
  Login (correo + contrasena)
        |
        +--- credenciales invalidas --> mensaje generico + registro en log
        |
        v
  Inicio (resumen de matricula + documentos pendientes + alertas SIMAT)
```

- MFA no obligatorio para este rol (depende de la politica del colegio).
- El acceso queda en el log de auditoria del tenant (RR-03).
- Si el tenant esta suspendido por el Superadmin, ve pantalla "colegio suspendido" y no puede operar.

---

## HEADER (presente en toda la app)

```
[ Logo Colegio ]   [ Buscador de estudiantes ]      [ Periodo / Calendario ]  [ Perfil ]  [ Notificaciones ]
```

- **Perfil del usuario:** datos de la secretaria, cerrar sesion, cambiar contrasena.
- **Buscador:** busca estudiantes por nombre, documento, grupo o estado de matricula.
- **Periodo / Calendario:** indica el ano lectivo y el periodo activo (solo lectura; lo define el Rector).
- **Notificaciones:** documentos de matricula vencidos, plazos del SIMAT, solicitudes de constancia de acudientes, paz y salvos pendientes de cartera.

---

## N1 — SIDEBAR (modulos del rol)

```
+----------------------------+
|  Inicio                    |
|  Estudiantes               |
|  Matricula                 |
|  Documentos de matricula   |
|  Documentos oficiales      |
|  SIMAT / Reportes MEN      |
|  Habeas Data / Consent.    |
|  Comunicaciones            |
|  Historial / Auditoria     |
+----------------------------+
```

La Secretaria NO tiene acceso a modulos academicos editables (notas, asistencia, observador, boletines como editor, configuracion del colegio). Esos no aparecen en su sidebar. Las notas solo se leen indirectamente al generar certificados.

---

## Detalle por modulo

### Inicio

Vista de entrada. Tarjetas resumen:
- Matriculas del ano (matriculados / en proceso / sin documentos).
- Documentos de matricula pendientes (con conteo por vencer).
- Constancias / certificados / paz y salvos emitidos en el mes (consecutivos).
- Estado del ultimo reporte SIMAT (al dia / pendiente / con errores).

> Callout informativo: el inicio es de solo lectura; las acciones se hacen en cada modulo.

### Estudiantes

- **Sub-vistas:** lista de estudiantes / ficha del estudiante.
- **Filtros:** grupo, grado, estado de matricula, documentos pendientes, ano de ingreso.
- **Detalle:** datos personales del estudiante, datos del / los acudientes operativos (como contacto dentro de la ficha, no como usuario — RR-11, `RN-TU-410`), historial de matricula.
- **Acciones:** Crear estudiante · Editar estudiante · Editar datos de acudiente operativo · Adjuntar consentimiento de habeas data.
- Callout importante: el acudiente NO es un usuario del sistema; sus datos viven dentro de la ficha del estudiante como informacion de contacto.

**Como se usa este modulo:** cuando llega una familia nueva, la secretaria crea la ficha del estudiante, registra los datos del acudiente operativo como contacto, captura el consentimiento de tratamiento de datos (`RN-HD-001`) y deja el registro listo para vincularlo al proceso de matricula. (Ver [[Casos de Uso/RF-30 Registrar estudiantes y acudientes|CU RF-30]].)

### Matricula

- **Sub-vistas:** proceso de matricula del estudiante / asignacion de grupo.
- **Filtros:** estado del proceso (inscrito / con documentos / matriculado), grupo destino, grado.
- **Detalle:** checklist de documentos requeridos, grupo asignado, fecha de matricula.
- **Acciones:** Asignar estudiante a grupo · Cambiar grupo post-matricula (configurable, RR-05) · Marcar matricula completada.
- Callout warning: cambiar el grupo despues de matriculado puede estar restringido al Coordinador Academico segun la configuracion del colegio.

**Como se usa este modulo:** la secretaria toma un estudiante inscrito, verifica que el checklist de documentos este completo, lo asigna a un grupo segun cupo y cierra la matricula. Si el colegio restringe el cambio de grupo, el sistema deshabilita esa accion. (Ver [[Casos de Uso/RF-31 Asignar a grupo|CU RF-31]].)

### Documentos de matricula

- **Sub-vistas:** documentos por estudiante / pendientes globales.
- **Filtros:** tipo de documento, estado (recibido / pendiente / vencido), estudiante.
- **Detalle:** cada documento con su estado, fecha de recepcion y quien lo cargo.
- **Acciones:** Cargar documento · Marcar como recibido · Marcar como pendiente · Definir documentos requeridos por grado.
- Callout importante: los documentos pendientes alimentan el bloqueo configurable de emision (RR-08).

**Como se usa este modulo:** la secretaria recibe los documentos fisicos o digitales, los carga, los marca como recibidos y mantiene la lista de pendientes que el sistema usa para bloquear o advertir antes de emitir documentos oficiales. (Ver [[Casos de Uso/RF-32 Documentos de matricula|CU RF-32]].)

### Documentos oficiales

- **Sub-vistas:** generar documento / historial de emitidos.
- **Filtros:** tipo (constancia / certificado de notas / paz y salvo), estudiante, rango de fechas, consecutivo.
- **Detalle:** plantilla del documento, datos del estudiante, consecutivo asignado, estado de pendientes.
- **Acciones:** Generar constancia de estudio · Generar certificado de notas · Emitir paz y salvo · Reimprimir / descargar PDF.
- Callout warning: si hay documentos o pagos pendientes y el bloqueo esta activado (RR-08, `RN-GD-270`, `RN-PZ-002`), el sistema impide la emision; si solo esta en modo advertencia, deja emitir con sello de advertencia.

**Como se usa este modulo:** un acudiente solicita una constancia o certificado; la secretaria selecciona el estudiante y el tipo de documento, el sistema valida pendientes, asigna un consecutivo (`RN-GD-001`) y genera el PDF con trazabilidad (quien, cuando, consecutivo). El certificado de notas lee las calificaciones en formato consolidado, sin permitir editarlas. (Ver [[Casos de Uso/RF-34 Generar constancias de estudio|CU RF-34]] y [[Casos de Uso/RF-35 Certificados de notas|CU RF-35]].)

### SIMAT / Reportes MEN

- **Sub-vistas:** preparar reporte / historial de reportes.
- **Filtros:** periodo de reporte, novedad (matricula / retiro / traslado), grado.
- **Detalle:** archivo en el formato requerido por el Ministerio de Educacion Nacional, conteo de registros, validacion previa.
- **Acciones:** Generar archivo SIMAT · Validar antes de exportar · Descargar / exportar · Marcar reporte como enviado.
- Callout importante: el reporte SIMAT es obligatorio para los colegios (RR-15, `RN-MO-001`); el sistema valida la consistencia de los datos antes de exportar (`RN-MO-004`).

**Como se usa este modulo:** en la ventana de reporte, la secretaria genera el archivo SIMAT con las novedades de matricula del periodo, corre la validacion previa, descarga el formato oficial para cargarlo en el portal del MEN y marca el reporte como enviado para trazabilidad. (Ver [[Casos de Uso/RF-37 Reportar a SIMAT|CU RF-37]].)

### Habeas Data / Consentimientos

- **Sub-vistas:** consentimientos por estudiante / pendientes de firma.
- **Filtros:** estado (firmado / pendiente / revocado), tipo de consentimiento.
- **Detalle:** consentimiento de tratamiento de datos del menor, autorizaciones de imagen, fecha y firma.
- **Acciones:** Adjuntar consentimiento · Marcar como firmado · Registrar revocatoria.
- Callout importante: el tratamiento de datos del menor exige consentimiento del acudiente (`RN-HD-001`, `RN-HD-002`); la revocatoria se registra y respeta (`RN-HD-006`).

**Como se usa este modulo:** durante la matricula, la secretaria adjunta y marca como firmados los consentimientos de habeas data; si una familia revoca una autorizacion, registra la revocatoria para que el colegio cumpla la normativa colombiana de proteccion de datos.

### Comunicaciones

- **Sub-vistas:** mensajes con acudientes / comunicados.
- **Filtros:** estudiante, grupo, estado del mensaje.
- **Detalle:** hilo de mensajes con el acudiente operativo (como contacto), plantillas de aviso de documentos pendientes.
- **Acciones (configurables, RR-05):** Comunicarse con acudientes via portal · Enviar comunicados al colegio entero.
- Callout informativo: estas acciones son configurables; si el colegio no las activa para la secretaria, el modulo aparece en modo solo lectura.

**Como se usa este modulo:** cuando un estudiante tiene documentos vencidos, la secretaria envia un aviso al acudiente operativo desde una plantilla. Si el colegio lo permite, tambien puede difundir comunicados administrativos (fechas de matricula, plazos de documentos).

### Historial / Auditoria

- **Sub-vistas:** historial de cambios de un registro (configurable, RR-05).
- **Filtros:** estudiante, tipo de accion, rango de fechas.
- **Detalle:** quien cambio que y cuando sobre estudiantes, matricula y documentos.
- **Acciones:** Ver historial de un registro (no edita el log; es solo lectura, RR-03).
- Callout importante: la secretaria NO accede al log global del tenant (eso es del Rector); solo ve, si el colegio lo activa, el historial de los registros que ella opera.

**Como se usa este modulo:** ante una discrepancia (por ejemplo, un grupo cambiado), la secretaria consulta el historial del estudiante para ver quien hizo el cambio y cuando, sin poder alterar el registro de auditoria.

---

## Diferencias clave vs otros roles

| Aspecto | Secretaria (ROL-06) | Rector (ROL-02) | Coord. Academico (ROL-03) | Docente (ROL-07) |
| --- | --- | --- | --- | --- |
| Notas | Solo lectura para certificados | Editar | Configurable | Editar en su materia |
| Matricula y documentos | CRUD / emitir | Ver / supervisa | Asigna grupo (config.) | No participa |
| Documentos oficiales | Emite (con consecutivo) | Tambien puede emitir | No | No |
| SIMAT | Genera el reporte | Supervisa | No | No |
| Configuracion del colegio | No | Editar | No | No |
| Observador disciplinario | No accede | Editar | No (lo ve Convivencia) | Academico en su materia |
| Bloqueo por pendientes | Lo aplica (config.) | Lo configura | No | No |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo |  Buscador estudiantes     | Periodo | Perfil | Notif       |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Inicio |  [ Inicio: matricula + documentos pendientes + SIMAT ]   |
| Estud. |  [ Lista estudiantes + ficha + acudiente operativo ]     |
| Matric.|  [ Proceso de matricula + asignacion de grupo ]          |
| Docs   |  [ Checklist de documentos + recibido/pendiente ]        |
| Oficial|  [ Generar constancia/certificado/paz y salvo + consec ] |
| SIMAT  |  [ Generar y validar reporte MEN ]                       |
| Habeas |  [ Consentimientos de datos del menor ]                  |
| Comunic|  [ Mensajes con acudientes (configurable) ]              |
| Histor.|  [ Historial de cambios de un registro (configurable) ]  |
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
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/05-secretaria-academica.md`
