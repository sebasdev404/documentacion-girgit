---
titulo: Matrículas por enlace
modulo: procesos-academicos
tipo: proceso
estado: implementado-local
tags: [matriculas, ingreso-estudiantil, documentos, pin]
---

# Matrículas por enlace — corte documental 14 de octubre de 2026

## Alcance vigente

El menú **Ingreso estudiantil** separa Matrículas por enlace, Matrículas académicas y Admisiones. Esta entrega permite matrícula directa de estudiantes nuevos. Admisiones con pruebas/entrevistas es una etapa futura, no un requisito artificial para el flujo actual.

**Sin pagos y sin cuentas de acudiente.** La pasarela se presenta como «Próximamente»; no existen cobros, facturas ni webhooks en este flujo. El solicitante externo no tiene un usuario de acudiente. Solo se crea una cuenta de estudiante cuando el colegio aprueba.

Esta decisión sustituye el borrador anterior que exigía pagar para obtener PIN y crear cuentas de acudientes. Aquellas condiciones NO aplican a esta versión.

## Actores y permisos

- Rector: configura la política institucional de matrículas y las convocatorias/requisitos, consulta, revisa, decide y asigna grupos.
- Secretaría: puede recibir los permisos explícitos, inicialmente desactivados.
- Coordinación académica/combinada: puede recibir consulta y asignación, inicialmente desactivadas.
- Solicitante: el enlace opaco fija la convocatoria; para consultar su expediente usa el enlace privado y PIN de cuatro dígitos, sin cuenta previa ni selector de convocatoria.
- Estudiante aprobado: cambia su contraseña; no configura logo ni información institucional.

Los seis permisos `ingreso.*` están en [[../02-usuarios-roles-y-permisos/matriz-de-permisos|Matriz de permisos]]. Requieren capacidad comercial `academico`. Revisar, decidir, cambiar grado y asignar exigen también `ingreso.ver`.

**Configuración de matrículas** requiere `ingreso.configurar` y capacidad de plan `academico`. El permiso es delegable según la matriz; no exige ser rector si existe una delegación válida. Su ubicación en Ajustes institucionales no lo convierte en `config.correo` ni le aplica el bloqueo de edición de la conexión de correo.

## Flujo implementado

1. **Convocatoria.** Seleccionar año planificado/en curso, fechas inclusivas u opcionalmente sin cierre, grados activos, cupo opcional por grado, campos y documentos. Habilitar/cerrar enlace por separado.
2. **Enlace.** Se genera en el dominio del colegio: `https://colegio.dominio/ingreso/<selector-opaco>`. Cada enlace abre directamente su convocatoria, sin que el aspirante elija una ronda. No se ofrece matrícula/seguimiento desde login; se utiliza el enlace privado del correo.
3. **Verificación.** Indicar correo y grado solo al iniciar; el colegio envía un PIN al correo y lo usa para verificarlo antes de cargar datos. El navegador conserva un desafío privado HttpOnly; desde otro dispositivo se usa el enlace privado del correo más el PIN de cuatro dígitos. No se crea usuario. Una solicitud por correo y convocatoria.
4. **Formulario local.** Nombres/apellidos, nacimiento, tipo/número de documento, celular, país, departamento/municipio, dirección y campos configurados. Sin Guardar ni guardado parcial. Datos/archivos nuevos solo viven en la pestaña hasta Enviar a revisión; cerrar/recargar pierde cambios no enviados. El registro mínimo de solicitud/PIN permanece.
5. **Documentos.** Seleccionar requisitos no sube archivos. Se respetan formatos configurados, nombre original y versiones tras envío. MIME, extensión, tamaño, cuota y escáner en servidor. Un aprobado no puede reemplazarse.
6. **Envío único.** Campos/documentos completos, sin rechazados pendientes de reemplazo, validación de edad y consentimiento sobre la versión vigente del aviso institucional según la política definida abajo. OCR local compara nombres, número y nacimiento con la identidad. Si falla, no conserva datos/versiones ni copias provisionales del intento. Si pasa: estado enviada, constancia de la validación y del consentimiento, correo y bandeja interna; UUID de reintento evita duplicados.
7. **Revisión.** Aprobar documentos o pedir correcciones con motivo obligatorio. Notificar al correo. El portal muestra observación/versiones. El solicitante corrige y reenvía.
8. **Decisión.** Aprobar, rechazar, pedir correcciones o dejar en espera. Las tres últimas requieren motivo. Aprobar valida envío, consentimiento, documentos aprobados, cupo de grado, límite de estudiantes del plan e identidad/correo no duplicados.
9. **Grado.** Se conservan solicitado y aprobado/propuesto. Cambiar requiere permiso y motivo; un grado de destino distinto exige revalidar la edad con la política vigente. Para requisitos nuevos se propone el cambio y se piden documentos antes de aprobar.
10. **Cuenta.** Aprobar crea una cuenta de estudiante, envía contraseña temporal de 72 horas y exige cambiarla al ingresar. Sin grupo se muestra aviso; aún no existe matrícula académica.
11. **Grupo.** Asignación individual o propuesta automática aleatoria, distribuida según ocupación y cupo de grupos del grado. El operador revisa/confirma. La propuesta no reserva cupos. Confirmación transaccional revalida cupos y crea una única matrícula activa estudiante/grupo/año.

## Estados y límites

`borrador → enviada → revision → aprobada → matriculada`

Durante revisión se permite `correcciones → enviada`, `espera` o `rechazada`. La espera no se aprueba automáticamente. Aprobada = cuenta creada/grupo pendiente; matriculada = matrícula académica confirmada.

- Hasta 30 requisitos comunes o por grado: instrucciones, obligatoriedad y formatos PDF/JPG/PNG/DOCX. El tamaño no se configura por requisito: el límite interno es 1 GB decimal (1.000.000.000 bytes) por archivo para todos los colegios, sujeto además a la capacidad efectiva del servidor, al lote final y a la cuota del plan.
- Hasta 20 versiones por requisito. Al llegar al límite se pide contactar al colegio; no se rechaza automáticamente el aspirante.
- Hasta 20 campos adicionales de texto/fecha, opcionales u obligatorios.
- Cupo de convocatoria por grado: opcional. Si se define, cuenta matrículas activas más aprobados pendientes de grupo para ese grado/año; vacío significa sin tope propio del enlace. No modifica la cuota comercial de estudiantes ni el cupo de cada grupo al confirmar.
- El correo de matrícula es multipartes: HTML con identidad visual del SaaS y alternativa de texto. Un mensaje de vista previa al remitente institucional debe usar datos ficticios y no crea solicitud.
- La apertura real para menores requiere que el colegio revise y apruebe su aviso de privacidad y cómo se obtiene la autorización de su representante legal. No asumir que la casilla genérica o una plantilla en borrador cumplen ese requisito; mantener la convocatoria cerrada hasta resolverlo.
- La propuesta automática admite hasta 300 pendientes. Para volúmenes mayores se trabaja individualmente antes de generar otra propuesta.
- Año/requisitos se congelan desde la primera solicitud. Nombre, fechas y habilitación siguen editables. Nuevos requisitos requieren otra convocatoria.
- Cierre impide iniciar/editar/subir; permite consultar con PIN y revisión interna. Para recibir correcciones debe reabrirse dentro de un año válido.
- PIN de cuatro dígitos + enlace privado de 256 bits/desafío HttpOnly. Vencimiento fijo opcional por convocatoria; sin fecha no caduca por tiempo. Cinco errores bloquean; reemisión sustituye PIN/enlace. Códigos largos y acceso legado eliminados.
- Sesión pública de 2 horas con cookie HttpOnly host-only, CSRF y origen. Logout revoca sesiones previas.
- Contraseña vencida: «Olvidé mi contraseña». No reutilizar contraseñas anteriores.
- Un correo institucional por estudiante. La renovación reutiliza el expediente solo tras verificar enlace privado, PIN, correo y documento; no fusiona identidades ni crea otra cuenta.

## Renovación de estudiantes existentes — alcance definido, aún no implementado

- El colegio prepara una nueva convocatoria para el siguiente año lectivo copiando **su configuración** (por ejemplo, de 2026 a 2027) y ajustando nombre, fechas, grados y requisitos. No se duplican solicitudes, matrículas, PIN ni archivos de los estudiantes.
- Un estudiante ya registrado debe vincularse con su expediente mediante una verificación privada/autorizada; escribir solo un número de documento en una página pública nunca puede revelar datos personales. Después de esa verificación, el documento permite localizar el expediente existente y precargar datos estables para revisión y actualización de contacto, dirección y representante.
- Los requisitos documentales de la nueva convocatoria se evalúan para ese año. El boletín o certificado del año anterior corresponde al año realmente cursado (para 2027, el de 2026); un comprobante con antigüedad máxima de tres meses debe ser reciente a la nueva presentación. El colegio configura qué requisitos vuelven a exigirse y su vigencia; no se considera vigente un archivo anterior solo porque ya esté almacenado.
- Los documentos nuevos se mantienen locales en la pestaña hasta «Enviar a revisión», igual que en el ingreso nuevo. Tras validación y aprobación se crea **una nueva matrícula para el año destino**, enlazada al mismo estudiante y conservando el historial de años previos. No se crea una segunda cuenta. Los pagos quedan fuera de este incremento.
- El grado de la renovación se determina con el resultado académico previo: si aprobó Primero, la solicitud del año siguiente apunta a Segundo; si reprobó, apunta al grado que corresponda repetir. Esto no modifica la matrícula del año anterior ni crea automáticamente la nueva.
- La renovación por enlace privado/PIN permite precargar los datos tras cotejar correo y documento con una cuenta activa, matrícula previa y promoción aprobada de un año cerrado. Si antes del envío se seleccionó otro grado, se corrige al destino institucional único de la convocatoria. El nuevo año exige sus documentos, actualiza el perfil únicamente al aprobar y conserva usuario/contraseña e historial. La matrícula nueva se crea al confirmar grupo. Una convocatoria se puede copiar a un año futuro solo con equivalencias institucionales únicas; nunca copia solicitudes ni archivos.
- Salir del colegio (`egresado`) es un estado de usuario distinto del resultado académico (`promovido`/`reprobado`). Se marca **manualmente** para quien no continúa, sin depender del grado cursado. Bloquea acceso a la plataforma y conserva la cuenta, las matrículas y el expediente. No cambia el rol histórico de estudiante por un rol ficticio «Egresado».
- El permiso `estudiantes.egreso.gestionar` existe en la matriz: ningún rol del colegio lo recibe por defecto, por lo que inicialmente actúa el superadministrador de plataforma. El rector puede habilitarlo para su rol o delegarlo en los roles configurables. La acción se audita. La reincorporación de un egresado requerirá un flujo explícito y verificado; la edición genérica de usuarios no lo reactiva.

## Reglas de negocio vigentes

- **RN-MA-001 — Cupos:** verificar grado al aprobar y grupo al confirmar bajo bloqueo del año.
- **RN-MA-002 — PIN sin pago:** emitir por convocatoria/correo; consultar por enlace privado/desafío más PIN, sin elegir convocatoria ni volver a escribir el correo.
- **RN-MA-003 — Vigencia/acceso:** PIN de cuatro dígitos con secreto independiente, vencimiento fijo opcional, sesión privada de dos horas y cinco intentos por desafío.
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

Nuevos archivos bajo `storage/app/tenants/<Colegio_identificador>/matriculas/Envio_<uuid>/<requisito>/<nombre_original>`. El lote único impide que la limpieza de un intento fallido borre archivos previos. Rutas históricas conservadas. Ruta física no pública.

PIN y contraseña temporal cifrados en bandeja de notificaciones hasta envío; después se borra el contenido. PIN almacenado como hash; el HMAC indexado por colegio corresponde al secreto del enlace privado, no a cuatro dígitos. Los jobs contienen referencias, no contraseñas. Envío después del commit y reintentos sin repetir operaciones de negocio. SMTP puede duplicar un correo si el worker cae justo después de enviarlo; no duplica cuenta ni matrícula.

No se añadió scheduler permanente: se usa cola existente y comando de recuperación. Sin Gmail institucional ni otro transporte real, `log`/`array` no entrega mensajes; administración advierte y producción impide abrir convocatorias en esas condiciones.

El rector conecta Gmail desde **Ajustes institucionales → Conexión de correo electrónico**, accesible también en el menú del usuario, con dirección, nombre y contraseña de aplicación. Hay guía visual y enlaces oficiales. No se usa la contraseña habitual. «Probar y guardar» envía al remitente y solo guarda al ser aceptado por el transporte. Una prueba fallida no sustituye la configuración anterior.

**RN-CO-001 — Conexión guardada bloqueada:** después de la primera conexión, cualquier edición o desconexión requiere una solicitud con motivo. Solo el superadministrador central puede aprobar/rechazar; recibe aviso persistente en su bandeja. No se desbloquea asignando permisos. La autorización es de un uso, dura 24 horas y corresponde únicamente al rector solicitante, colegio, acción y versión de configuración. Guardar vuelve a bloquear; una prueba fallida permite reintentar mientras siga vigente. Rechazo requiere observación. Desconectar conserva un registro bloqueado, sin clave; reconectar requiere nueva autorización. `config.correo` y rol rector son requisitos para la pantalla, no un permiso permanente de edición.

La clave queda cifrada en cada tenant, nunca visible en API/auditoría ni almacenamiento persistente del navegador. Los avisos de matrícula y recuperación de contraseña usan el remitente de ese colegio; transporte nuevo en cada envío para no mezclar credenciales en workers. Desconectar elimina la copia local y el rector debe revocarla en Google. La prueba no garantiza futura recepción: rigen límites, spam y posibles revocaciones. Referencia: [Google: contraseñas de aplicación](https://support.google.com/accounts/answer/185833?hl=es). No hay OAuth ni pasarela de pago en esta entrega.

## Verificación y pendientes de producción

API: recorrido completo, reenvío, documentos privados, PIN/cookies/CSRF, límites, duplicados, permisos, grado, contraseña, idempotencia y enlaces de sedes. Navegador: configuración, carga/corrección, seguimiento, aprobación, grupos y móvil, con datos simulados. Migraciones: esquema nuevo y restauración PostgreSQL con respaldo y comparación de datos existentes.

Antes de publicar: verificar correo real, worker supervisado, HTTPS, escáner, respaldos y política institucional de conservación/tratamiento. Las pruebas locales no equivalen a validación VPS. La renovación exige matrícula previa activa, año anterior cerrado/archivado, promoción aprobada y grado correspondiente; usuarios históricos sin perfil de identidad necesitan conciliación autorizada. Quedan fuera pasarela, cuentas/acceso de acudientes, entrevistas/exámenes de admisión, firma de contratos, importación masiva y WhatsApp.

Relacionados: [[admisiones]], [[../08-casos-de-uso/CU-002-matricular-estudiante]], [[../08-casos-de-uso/CU-003-pre-matricula-desde-portal]]. Runbook: `colegio-saas-backend/docs/INGRESO_ESTUDIANTIL.md`.

## Validaciones de envío

Incorporadas el 10 de octubre; RN-MA-015 se actualiza con la política institucional aceptada el 14 de octubre de 2026.

- **RN-MA-013 — Sin persistencia parcial:** una sola acción final; quitar/sustituir selecciones es local. No se aceptan guardados de borrador ni cargas individuales. Fallos de validación/escáner/OCR revierten el intento; versiones previas intactas.
- **RN-MA-014 — Requeridos:** primer nombre/apellido, nacimiento, tipo/número de identidad, celular, país, departamento/municipio, dirección y adicionales configurados. Espacios no cuentan; segundo nombre/apellido opcionales. Asterisco rojo y validación cliente/servidor.
- **RN-MA-015 — Edad:** fecha de nacimiento válida y no futura. Edad en años cumplidos a la fecha actual en la zona horaria institucional. Un único rango institucional permanente por grado estable, con mínimo y máximo inclusivos; deshabilitado significa sin límite de edad para ese grado. No hay fecha de corte configurable, exclusión automática por nacer en el año actual ni copia anual de rangos. Para solicitudes ya enviadas rige la constancia de RN-MA-019; cambiar nacimiento o grado de destino exige revalidación.
- **RN-MA-016 — Correspondencia documental:** requisito de identidad explícito o identificación inequívoca del requisito legado; PDF/JPG/PNG legibles según configuración. OCR local compara nombres/número/nacimiento; ilegibilidad/discrepancia bloquea con motivo. No acredita autenticidad ante Registraduría ni reemplaza revisión humana.
- **RN-MA-017 — Ubicación:** Colombia por defecto, catálogo DIVIPOLA local, departamento/municipio dependiente validados por código. País/región/ciudad libres para domicilio extranjero. Fuente: [DANE / Datos Abiertos](https://www.datos.gov.co/Mapas-Nacionales/DIVIPOLA-C-digos-municipios/gdxc-w37w), consulta 10-10-2026.

Operación: dependencias OCR/Poppler y límites PHP/proxy documentados en el runbook backend. Pruebas OCR con identidades sintéticas, nunca documentos personales en el repositorio. Sin cuentas de representante legal.

## Política institucional de matrículas — decisión aceptada el 14 de octubre de 2026

Esta sección es la fuente canónica de la política aceptada. Actualiza las referencias anteriores a edades por convocatoria/fecha de referencia y al aviso por convocatoria. Su incorporación documental no acredita despliegue en producción, pruebas de correo real ni selección de edades para un colegio.

### Ubicación, alcance y permisos

**RN-MA-018 — Configuración institucional:** la pantalla se encuentra en **Ajustes institucionales > Configuración de matrículas** y tiene un acceso directo desde **Matrículas por enlace**. Ambos accesos abren el mismo formulario y exigen `ingreso.configurar` más la capacidad `academico`, también en servidor. El rector puede delegar el permiso según la matriz vigente; no se crean usuarios de acudiente ni se concede al solicitante acceso a Ajustes.

El formulario reúne los rangos de edad por grado y el aviso de privacidad del colegio. Las convocatorias mantienen su año, fechas de apertura/cierre, grados ofrecidos, cupos, campos, requisitos y vencimiento fijo opcional del acceso privado. Esos parámetros de convocatoria no crean políticas institucionales independientes.

### Rangos permanentes y cálculo de edad

- Existe una sola configuración de edad por colegio y grado de identidad estable. No pertenece al grado de un año lectivo concreto ni se duplica por convocatoria. Crear o copiar un año reutiliza la misma política, sin copiar rangos ni pedir que se definan de nuevo.
- Cada grado permite habilitar o deshabilitar su rango. Habilitado requiere mínimo y máximo en años cumplidos, con mínimo menor o igual al máximo; ambos extremos son inclusivos. Fuera del rango se bloquea el envío o el cambio de grado que requiera una nueva validación.
- Deshabilitado significa **sin límite de edad** para ese grado; no activa un rango oculto o predeterminado. Se conserva la validación de una fecha de nacimiento válida y no futura.
- La edad se calcula a la fecha actual del colegio en su zona horaria institucional, considerando si ya ocurrió el cumpleaños. No se usa la fecha local del navegador, una fecha de corte arbitraria, el inicio/fin del año ni una fecha elegida en la convocatoria. El servidor es autoritativo.
- Los rangos concretos los decide el colegio. Esta documentación no asigna edades reales ni deduce límites a partir del nombre del grado.

### Solicitudes enviadas y correcciones

**RN-MA-019 — Constancia de edad validada:** cuando un envío supera las validaciones se conserva una instantánea de la fecha de nacimiento y del grado de destino validados, junto con la evidencia del cálculo y de la política aplicada: edad, fecha y zona horaria de evaluación, rango aplicado o estado sin límite. La constancia pertenece al expediente enviado, no a las selecciones locales ni al registro mínimo previo al envío.

Si una corrección mantiene esa misma fecha de nacimiento y ese mismo grado, se conserva la validación del envío aceptado. Cumplir años mientras se revisa la solicitud o editar después la política del colegio no invalida esa constancia ni impide corregir otros datos o documentos. Esto también protege una validación realizada cuando el grado no tenía límite de edad.

Cambiar la fecha de nacimiento o el grado de destino, incluido un grado propuesto por el colegio, obliga a validar nuevamente con la fecha actual institucional y la política vigente para ese grado. La nueva constancia solo se registra si la validación y el envío correspondiente prosperan; un intento fallido no sobrescribe la constancia anterior. Una solicitud aún no enviada no tiene esta protección. La constancia de edad no omite requisitos documentales, cupos ni la validación del consentimiento vigente.

### Aviso institucional y consentimiento versionado

**RN-MA-020 — Aviso vigente al enviar:** el aviso de privacidad se administra y versiona por colegio en Configuración de matrículas. Tras el primer guardado institucional, todas sus convocatorias usan ese aviso; editar una convocatoria no crea otro texto independiente. El envío registra la aceptación vinculada a la versión y al texto efectivamente presentados, con la fecha de aceptación.

Al pulsar **Enviar a revisión**, también en un reenvío por correcciones, el servidor compara la versión aceptada con la vigente. Si el aviso cambió mientras el formulario estaba abierto, detiene el envío antes de darlo por recibido, muestra el aviso actualizado y exige una nueva aceptación explícita. La aceptación anterior no autoriza el texto nuevo ni se marca automáticamente. Los datos y archivos seleccionados permanecen disponibles en la pestaña para reintentar, conforme a RN-MA-013. La evidencia de consentimientos anteriores se conserva; guardar un aviso nuevo no los reescribe.

### Transición desde valores de convocatoria

**RN-MA-021 — Adopción explícita sin suposiciones:** hasta el primer guardado institucional se conservan los valores heredados de rangos y avisos de las convocatorias existentes. Abrir la pantalla o consultar una convocatoria no cuenta como guardado ni reemplaza esos valores. El primer guardado explícito establece la política compartida para las convocatorias y años siguientes, respetando las constancias de solicitudes enviadas.

El formulario solo sugiere valores existentes cuya correspondencia con el grado estable y cuyo contenido sean inequívocos. Una sugerencia no es una adopción automática. Si los valores heredados discrepan —incluido un rango frente a una configuración sin límite o varios textos de aviso— se muestran los conflictos y se exige elegir o definir el valor institucional en **ese mismo formulario**, antes de guardar. No se elige por antigüedad, por año, por mayoría ni por coincidencia de nombres. Si faltan datos suficientes, no se inventan edades ni un aviso: el colegio debe definirlos. Las antiguas fechas de referencia no se trasladan como fechas de corte a la política nueva.

Durante la transición, el consentimiento identifica el aviso efectivo que se mostró al solicitante. Si el primer guardado institucional cambia ese aviso mientras el formulario está abierto, se aplica la detección de cambio y nueva aceptación de RN-MA-020.

### Criterios de aceptación de esta política

Estos escenarios describen resultados requeridos; no son un reporte de pruebas ejecutadas.

| Escenario | Resultado requerido |
| --- | --- |
| Acceso desde Ajustes o desde Matrículas por enlace | Mismo formulario, `ingreso.configurar` delegable y plan `academico`; sin usuarios de acudiente. |
| Nuevo año o convocatoria con el mismo grado estable | Usa la política institucional existente, sin copia anual ni nuevos rangos. |
| Edad exactamente en un extremo del rango; rango deshabilitado | Ambos extremos se aceptan; deshabilitado no limita la edad. |
| Navegador y colegio tienen fechas distintas | La fecha de la zona horaria institucional determina los años cumplidos. |
| Corrección tras cumpleaños o cambio de política, sin cambiar nacimiento/grado | Conserva la constancia validada del envío. |
| Corrección de nacimiento o cambio de grado de destino | Revalida con fecha actual y política vigente; un fallo conserva la constancia previa. |
| Aviso cambia antes de enviar, incluido el primer guardado institucional | Detiene el envío y pide aceptar expresamente la versión actualizada. |
| Valores heredados inequívocos o en conflicto | Los primeros solo se sugieren; los conflictos se resuelven en el mismo formulario antes del primer guardado. |
