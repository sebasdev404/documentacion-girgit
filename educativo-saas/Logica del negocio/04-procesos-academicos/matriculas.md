---
titulo: Matrículas por enlace
modulo: procesos-academicos
tipo: proceso
estado: implementado-local
tags: [matriculas, ingreso-estudiantil, documentos, pin]
---

# Matrículas por enlace — corte 7 de octubre de 2026

## Alcance vigente

El menú **Ingreso estudiantil** separa Matrículas por enlace, Matrículas académicas y Admisiones. Esta entrega permite matrícula directa de estudiantes nuevos. Admisiones con pruebas/entrevistas es una etapa futura, no un requisito artificial para el flujo actual.

**Sin pagos y sin cuentas de acudiente.** La pasarela se presenta como «Próximamente»; no existen cobros, facturas ni webhooks en este flujo. El solicitante externo no tiene un usuario de acudiente. Solo se crea una cuenta de estudiante cuando el colegio aprueba.

Esta decisión sustituye el borrador anterior que exigía pagar para obtener PIN y crear cuentas de acudientes. Aquellas condiciones NO aplican a esta versión.

## Actores y permisos

- Rector: configura convocatoria/requisitos, consulta, revisa, decide y asigna grupos.
- Secretaría: puede recibir los permisos explícitos, inicialmente desactivados.
- Coordinación académica/combinada: puede recibir consulta y asignación, inicialmente desactivadas.
- Solicitante: acceso solo a su expediente por correo + PIN, sin cuenta previa.
- Estudiante aprobado: cambia su contraseña; no configura logo ni información institucional.

Los seis permisos `ingreso.*` están en [[../02-usuarios-roles-y-permisos/matriz-de-permisos|Matriz de permisos]]. Requieren capacidad comercial `academico`. Revisar, decidir, cambiar grado y asignar exigen también `ingreso.ver`.

## Flujo implementado

1. **Convocatoria.** Seleccionar año planificado/en curso, fechas inclusivas, grados activos, cupos totales por grado, campos y documentos. Habilitar/cerrar enlace.
2. **Enlace.** Se genera en el dominio del colegio: `https://colegio.dominio/ingreso/<selector-opaco>`. La página `/ingreso` y el acceso desde login permiten iniciar/consultar.
3. **Verificación.** Indicar correo y grado. Recibir PIN y verificar email antes de cargar datos. No se crea usuario. Una solicitud por correo y convocatoria.
4. **Borrador.** Nombres/apellidos separados, fecha de nacimiento, tipo/número de documento, teléfono, dirección y campos configurados. «Guardar borrador» conserva avances en servidor; cambios sin guardar no sobreviven al cierre.
5. **Documentos.** Subir requisitos del grado. Se conserva nombre original y versiones. Validar MIME, tamaño, cuota y escáner. Un archivo aprobado no puede reemplazarse desde el portal.
6. **Envío.** Campos/documentos obligatorios completos, sin documentos rechazados, aceptación del texto de tratamiento de datos institucional. Estado `enviada`, correo al solicitante y disponibilidad en bandeja interna.
7. **Revisión.** Aprobar documentos o pedir correcciones con motivo obligatorio. Notificar al correo. El portal muestra observación/versiones. El solicitante corrige y reenvía.
8. **Decisión.** Aprobar, rechazar, pedir correcciones o dejar en espera. Las tres últimas requieren motivo. Aprobar valida envío, consentimiento, documentos aprobados, cupo de grado, límite de estudiantes del plan e identidad/correo no duplicados.
9. **Grado.** Se conservan solicitado y aprobado/propuesto. Cambiar requiere permiso y motivo. Para requisitos nuevos se propone el cambio y se piden documentos antes de aprobar.
10. **Cuenta.** Aprobar crea una cuenta de estudiante, envía contraseña temporal de 72 horas y exige cambiarla al ingresar. Sin grupo se muestra aviso; aún no existe matrícula académica.
11. **Grupo.** Asignación individual o propuesta automática aleatoria, distribuida según ocupación y cupo de grupos del grado. El operador revisa/confirma. La propuesta no reserva cupos. Confirmación transaccional revalida cupos y crea una única matrícula activa estudiante/grupo/año.

## Estados y límites

`borrador → enviada → revision → aprobada → matriculada`

Durante revisión se permite `correcciones → enviada`, `espera` o `rechazada`. La espera no se aprueba automáticamente. Aprobada = cuenta creada/grupo pendiente; matriculada = matrícula académica confirmada.

- Hasta 30 requisitos comunes o por grado: instrucciones, obligatoriedad, PDF/JPG/PNG/DOCX y 1–10 MB; además rigen límites globales.
- Hasta 20 versiones por requisito. Al llegar al límite se pide contactar al colegio; no se rechaza automáticamente el aspirante.
- Hasta 20 campos adicionales de texto/fecha, opcionales u obligatorios.
- Cupo de grado: matrículas activas más aprobados pendientes de grupo, para ese grado/año entre convocatorias. No se reserva al abrir formulario.
- La propuesta automática admite hasta 300 pendientes. Para volúmenes mayores se trabaja individualmente antes de generar otra propuesta.
- Año/requisitos se congelan desde la primera solicitud. Nombre, fechas y habilitación siguen editables. Nuevos requisitos requieren otra convocatoria.
- Cierre impide iniciar/editar/subir; permite seguimiento, recuperar PIN y revisión interna. Para recibir correcciones debe reabrirse dentro de un año válido.
- PIN alfanumérico de 15 días; recuperación reemplaza PIN sin duplicar expediente. Vigencia fija en esta entrega.
- Sesión pública de 2 horas con cookie HttpOnly host-only, CSRF y origen. Logout revoca sesiones previas.
- Contraseña vencida: «Olvidé mi contraseña». No reutilizar contraseñas anteriores.
- Un correo institucional por estudiante. Vincular/renovar usuarios existentes es otro flujo; no se fusionan identidades automáticamente.

## Reglas de negocio vigentes

- **RN-MA-001 — Cupos:** verificar grado al aprobar y grupo al confirmar bajo bloqueo del año.
- **RN-MA-002 — PIN sin pago:** emitir por convocatoria/correo; recuperar no duplica expediente.
- **RN-MA-003 — Vigencia/acceso:** PIN 15 días, sesión 2 horas, consultas privadas del titular.
- **RN-MA-004 — Pagos futuros:** descuentos, cobros y reembolsos no condicionan esta versión.
- **RN-MA-005 — Requisitos:** comunes o por grado; congelados al recibir solicitudes.
- **RN-MA-006 — Aprobación:** todos los documentos aplicables cargados aprobados, sin faltar obligatorios; correcciones reenviadas.
- **RN-MA-007 — Cuenta/matrícula separadas:** aprobación crea estudiante; asignación crea matrícula; sin usuarios de acudiente.
- **RN-MA-008 — Archivos:** privados, consumen cuota y atraviesan el pipeline del tenant.
- **RN-MA-009 — Trazabilidad:** versiones, motivos, revisión y decisiones; auditoría sin PIN/contraseña ni cuerpos de formulario.
- **RN-MA-010 — Identidad:** no duplicar correo ni documento de perfiles creados por este módulo. Usuarios históricos sin documento requerirán conciliación para renovación.
- **RN-MA-011 — Reintentos:** no duplicar cuentas/matrículas/aviso de credenciales al repetir aprobación o confirmar el mismo grupo.
- **RN-MA-012 — Autorización:** permiso + plan + tenant + pertenencia a solicitud, incluidos documentos.

## Almacenamiento y correo

Archivos bajo `storage/app/tenants/<Colegio_identificador>/matriculas/Ano_lectivo_<año>/<convocatoria>/Solicitud_<selector>/<requisito>/Version_<n>/<nombre_original>`. Espacios normalizados por StorageService; el selector evita mezclar homónimos. Ruta física no pública.

PIN y contraseña temporal cifrados en bandeja de notificaciones hasta envío; después se borra el contenido. PIN de autenticación almacenado como hash. Los jobs contienen referencias, no contraseñas. Envío después del commit y reintentos sin repetir operaciones de negocio. SMTP puede duplicar un correo si el worker cae justo después de enviarlo; no duplica cuenta ni matrícula.

No se añadió scheduler permanente: se usa cola existente y comando de recuperación. Sin Gmail institucional ni otro transporte real, `log`/`array` no entrega mensajes; administración advierte y producción impide abrir convocatorias en esas condiciones.

El rector conecta Gmail desde **Ajustes institucionales → Conexión de correo electrónico**, accesible también en el menú del usuario, con dirección, nombre y contraseña de aplicación. Hay guía visual y enlaces oficiales. No se usa la contraseña habitual. «Probar y guardar» envía al remitente y solo guarda al ser aceptado por el transporte. Una prueba fallida no sustituye la configuración anterior.

**RN-CO-001 — Conexión guardada bloqueada:** después de la primera conexión, cualquier edición o desconexión requiere una solicitud con motivo. Solo el superadministrador central puede aprobar/rechazar; recibe aviso persistente en su bandeja. No se desbloquea asignando permisos. La autorización es de un uso, dura 24 horas y corresponde únicamente al rector solicitante, colegio, acción y versión de configuración. Guardar vuelve a bloquear; una prueba fallida permite reintentar mientras siga vigente. Rechazo requiere observación. Desconectar conserva un registro bloqueado, sin clave; reconectar requiere nueva autorización. `config.correo` y rol rector son requisitos para la pantalla, no un permiso permanente de edición.

La clave queda cifrada en cada tenant, nunca visible en API/auditoría ni almacenamiento persistente del navegador. Los avisos de matrícula y recuperación de contraseña usan el remitente de ese colegio; transporte nuevo en cada envío para no mezclar credenciales en workers. Desconectar elimina la copia local y el rector debe revocarla en Google. La prueba no garantiza futura recepción: rigen límites, spam y posibles revocaciones. Referencia: [Google: contraseñas de aplicación](https://support.google.com/accounts/answer/185833?hl=es). No hay OAuth ni pasarela de pago en esta entrega.

## Verificación y pendientes de producción

API: recorrido completo, reenvío, documentos privados, PIN/cookies/CSRF, límites, duplicados, permisos, grado, contraseña, idempotencia y enlaces de sedes. Navegador: configuración, carga/corrección, seguimiento, aprobación, grupos y móvil, con datos simulados. Migraciones: esquema nuevo y restauración PostgreSQL con respaldo y comparación de datos existentes.

Antes de publicar: verificar correo real, worker supervisado, HTTPS, escáner, respaldos y política institucional de conservación/tratamiento. Las pruebas locales no equivalen a validación VPS. Quedan fuera pasarela, cuentas/acceso de acudientes, entrevistas/exámenes de admisión, firma de contratos, renovación automática, importación masiva y WhatsApp.

Relacionados: [[admisiones]], [[../08-casos-de-uso/CU-002-matricular-estudiante]], [[../08-casos-de-uso/CU-003-pre-matricula-desde-portal]]. Runbook: `colegio-saas-backend/docs/INGRESO_ESTUDIANTIL.md`.
