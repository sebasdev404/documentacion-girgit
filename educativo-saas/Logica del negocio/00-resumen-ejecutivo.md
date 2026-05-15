---
titulo: Resumen ejecutivo — Lógica de negocio consolidada
modulo: indice
tipo: referencia
estado: borrador
tags: [resumen, ejecutivo, moc, contexto-completo]
---

# Resumen ejecutivo — Lógica del negocio (SaaS de Gestión Escolar)

Documento consolidado de toda la lógica de negocio del producto, redactado en prosa detallada con referencia a las reglas de negocio (`RN-XX-NNN`) que las soportan. Este resumen es el **punto de entrada** para entender el sistema en una sola lectura. Los detalles operativos siguen viviendo en cada módulo del vault.

> **Convenciones.** Las reglas se identifican como `RN-XX-NNN` por módulo. Las decisiones tomadas durante el review estructural se concentran en los rangos `RN-110` a `RN-430`. Cuando algo está marcado como **funcionalidad futura** o **fuera de MVP**, no forma parte del alcance inicial pero sí del modelo de evolución.

---

## 1. Gestión de tenants (colegios)

Cada colegio es un **tenant** independiente. El [[02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma|Superadministrador de la Plataforma]] crea el tenant manualmente y el sistema provisiona automáticamente una **base de datos exclusiva**, un **subdominio `<slug>.<dominio>`** y un usuario administrador inicial con contraseña temporal autogenerada (`RN-OB-001`, `RN-OB-002`, `RN-AU-001`). El correo institucional recibe la URL y las credenciales del rector. El tenant queda en estado `Configurando` hasta que el rector complete la configuración mínima obligatoria, momento en el que pasa a `Activo`.

El **aislamiento es total**: ningún usuario de un tenant ve datos de otro, ni siquiera por error de filtro (`RN-AI-001`). El acceso del superadministrador a un tenant **no es libre**: requiere consentimiento del rector (ticket de soporte) y queda registrado y visible en el panel del propio rector (`RN-AD-210`, `RN-AD-211`). Los **backups y restauraciones se ejecutan por tenant** sin mezclar datos (`RN-AI-004`, `RN-AI-005`, `RN-BR-001`).

Si un tenant se elimina, su **subdominio entra en cuarentena temporal** antes de poder reutilizarse, para evitar suplantaciones (`RN-MT-240`). Los **upgrades de plan se aplican inmediatamente**; los **downgrades** se ejecutan al cierre del ciclo de facturación para no romper compromisos vigentes (`RN-MT-241`).

## 2. Modelo de negocio y comercial

La plataforma opera sobre un **doble flujo de monetización separable** (`RN-MN-001`): por un lado, el **SaaS cobra al colegio** una suscripción; por otro, el **colegio cobra a sus estudiantes** matrícula, pensiones y otros conceptos a través del módulo de pagos. Las **comisiones de pasarela son siempre transparentes** (`RN-MN-002`) y la **decisión de quién las asume** (colegio o pagador) es **configurable por colegio** (`RN-MN-003`). Mientras no exista un default global, se decide en onboarding.

El producto se comercializa con un **trial de 30 días**. Los planes, las bandas de precio y el tope para el modelo B2B2C son **decisión comercial pendiente** y se documentan fuera del vault. La **estrategia inicial es Colombia** con apertura progresiva a un segundo país piloto.

## 3. Suscripciones y pagos al SaaS

Las suscripciones del colegio al SaaS siguen las reglas `RN-PS-001..008`: contrato con vigencia, ciclo de facturación, suspensión por mora y cancelación. La **facturación electrónica** del SaaS al colegio depende de un **proveedor DIAN** que es decisión externa pendiente. Los reembolsos por anualidad prepagada y la política exacta de cobro están abiertos como decisión comercial.

## 4. Roles y tipos de usuario

El catálogo de **tipos de usuario** es cerrado y coincide 1 a 1 con los roles principales (ver [[02-usuarios-roles-y-permisos/tipos-de-usuario|Tipos de usuario]]). Los roles definidos son: **Superadministrador de la Plataforma** (global), **Rector / Administrador del Colegio**, **Coordinador Académico**, **Coordinador de Convivencia**, **Coordinador combinado** (cuando una sola persona asume ambas coordinaciones), **Secretaría Académica**, **Docente** (con el complemento opcional **Director de Grupo**) y **Estudiante**.

Una decisión estructural clave es que **el "acudiente" / "padre de familia" NO es un tipo de usuario** (`RN-TU-410`): la única cuenta del menor es la del **estudiante** y el acudiente la opera de hecho. Los datos del acudiente se registran como **información de contacto del estudiante** dentro de su ficha, sin credenciales propias ni perfil propio. El caso del docente cuyo hijo estudia en el mismo colegio queda resuelto por esta decisión: el hijo tiene su propia cuenta de estudiante y no se modela "doble rol".

Se incorpora el rol **Personal de apoyo** (psicólogo, enfermería, biblioteca, etc.) con permisos mínimos de consulta y aporte al observador, según la visibilidad triple de `RN-OB-081` (`RN-TU-411`).

Las **acciones sensibles** están centralizadas en un catálogo (`RN-RT-400`), con **retención diferenciada del log de auditoría** según criticidad (`RN-RT-401`). La **impersonación de usuarios es exclusiva del superadministrador** y queda doblemente auditada (`RN-RT-402`).

## 5. Autenticación y ciclo de vida de usuario

El **login es por subdominio** del tenant; un usuario solo existe en su tenant (`RN-AU-001`, `RN-AU-005`). Toda alta nueva entrega **contraseña temporal** y obliga al **cambio en el primer ingreso** (`RN-AU-002`, `RN-AU-360`). La **complejidad de contraseña** y el **bloqueo por intentos fallidos** son políticas globales (`RN-AU-003`, `RN-AU-004`). Cualquier evento de autenticación queda en el log (`RN-AU-007`).

El ciclo de vida del usuario contempla los estados `Pendiente → Activo → Inactivo → Suspendido` con transiciones auditadas (`RN-CV-001..005`). **La eliminación nunca borra datos históricos**: el usuario inactivo queda **oculto por defecto** en los listados, pero su huella en notas, asistencia, observador y pagos persiste íntegramente (`RN-CV-002`, `RN-CV-370`). **Los correos no se reutilizan** dentro del tenant (`RN-CV-003`).

El **MFA es obligatorio para el superadministrador y para roles de alto privilegio** desde el MVP, con expansión progresiva al resto de roles (`RN-RG-421`).

La **carga masiva de usuarios** acepta CSV y Excel con **plantilla descargable y validación estricta de cabeceras** (`RN-OU-390`), y opera en **dos modos** seleccionables: **transaccional (todo o nada)** por defecto en procesos críticos, y **tolerante** para procesar válidos y reportar errores por fila (`RN-OU-391`).

## 6. Configuración académica del colegio

Cada colegio define su **estructura organizacional** en `RN-JO-001..005`: sedes (opcionales), niveles, grados, jornadas y grupos. Un grupo pertenece a **un único año lectivo** y un estudiante pertenece a **un único grupo** dentro de ese año. Los **traslados entre sedes** dentro del mismo año son **configurables** (`RN-JO-231`). El **catálogo de jornadas y bloques** parte de un set base con posibilidad de personalización (`RN-JO-230`).

El **plan de estudios** es obligatorio (`RN-PE-001`) y se versiona por año lectivo: un cambio en el año vigente **no afecta los años cerrados** (`RN-PE-004`). Hay un **catálogo base de áreas con personalización por colegio** (`RN-PE-090`).

La **asignación docente** sigue las reglas `RN-AD-001..006`: titularidad por defecto única, asignación obligatoria para registrar notas, validación contra el plan, dentro del año activo. Se admite **co-titularidad configurable** (`RN-AD-010`) y un **soft-delete con reasignación obligatoria** (`RN-AD-011`) que evita huérfanos cuando un docente se retira.

Los **horarios** validan ausencia de conflictos (docente, grupo, aula) y son inmutables en años cerrados (`RN-HO-001..006`). Se permiten **excepciones puntuales** y **rotación A/B semanal** (`RN-HR-040`, `RN-HR-041`). Los **espacios físicos** se modelan con capacidad y detección automática de doble ocupación (`RN-EF-001..004`). El **calendario escolar** versiona festivos, eventos y cierres por año (`RN-CE-001..004`).

## 7. Calificaciones, logros y recuperaciones

El **registro de calificaciones** exige asignación vigente del docente (`RN-CA-001`) y se realiza dentro del **rango de la escala configurada** (`RN-CA-003`). Los **periodos académicos** abren y cierran formalmente; durante el cierre el sistema **bloquea ediciones** (`RN-CA-005`). El **recálculo del consolidado es automático** (`RN-CA-004`) y los **años cerrados son inmutables** (`RN-CA-006`).

Las **correcciones tras el cierre** se permiten dentro de una **ventana configurable por colegio** (`RN-CL-030`); si la ventana ya expiró, se requiere **aprobación del coordinador o rector** y la corrección queda doblemente auditada (`RN-CL-031`). La **importación masiva de notas** queda como funcionalidad futura.

Los **logros e indicadores** se gestionan por periodo (`RN-LI-001..005`); el sistema soporta **modos de evaluación configurables** —cualitativo, cuantitativo o mixto— (`RN-LI-050`) y **ponderación opcional de logros** dentro de la nota final del área (`RN-LI-051`).

Las **nivelaciones y habilitaciones** se generan automáticamente cuando el estudiante reprueba (`RN-NH-001..006`). El **tratamiento de la nota recuperada** es configurable por colegio (reemplazo, máximo entre las dos, promedio, tope, etc.) según `RN-NH-070`, y la **simultaneidad** de varias recuperaciones es opcional (`RN-NH-071`).

El **consejo académico** decide casos límite y **su decisión sobreescribe el cálculo automático** con auditoría de participantes y motivos (`RN-CO-001..007`).

## 8. Asistencia

La **asistencia se registra por sesión y solo si el docente tiene asignación vigente** (`RN-AS-001`, `RN-AS-002`). La justificación **no elimina** la inasistencia: queda como histórico con su estado (`RN-AS-003`). Las **alertas automáticas** se disparan al superar umbrales (`RN-AS-004`). La **edición es libre hasta el cierre del periodo** (`RN-AS-005`); los **festivos y días no lectivos no generan registros** (`RN-AS-006`); todo movimiento queda en el log (`RN-AS-007`).

La **acumulación de tardes / retardos en inasistencia** es **configurable por colegio** (`RN-AS-020`): cuántas tardes equivalen a una falla, si aplica solo a la primera hora del día, etc.

## 9. Boletines y promoción

Los **boletines se generan tras el cierre del periodo** o al cierre del año, son un **PDF persistente** (`RN-BR-001`, `RN-BR-005`) y se versionan fielmente con la configuración vigente cuando se generaron (`RN-BR-002`). Su descarga puede **bloquearse por paz y salvo** (`RN-BR-003`) y, cuando aplica, requiere **confirmación digital auditada** (`RN-BR-004`). La **personalización profunda de la plantilla** es **un servicio** del equipo de la plataforma (`RN-BR-006`); el **constructor visual de plantillas** es funcionalidad futura (`RN-RA-310`).

La **promoción** se calcula automáticamente (`RN-PR-001`), validada por coordinador (`RN-PR-002`); la decisión del consejo académico **prevalece** (`RN-PR-003`). El **cierre del año dispara la generación del siguiente** (`RN-PR-004`); los **datos del año cerrado son inmutables** (`RN-PR-005`); los **egresados pasan al rol Egresado** (`RN-PR-007`); el **cierre exige que no queden habilitaciones pendientes** (`RN-PR-008`). Las **plantillas de constancia/certificado** se ofrecen base + personalización por servicio (`RN-PR-100`); la **reapertura intra-ventana** del año es por permiso (`RN-PR-101`).

## 10. Observador y disciplina

Cada estudiante tiene **un observador por año lectivo** (`RN-OE-001`), de **solo lectura para el estudiante** (`RN-OE-002`), con **anulación que preserva la historia** (`RN-OE-003`) e **inmutabilidad post-cierre** del año (`RN-OE-004`). Los **reportes respetan la visibilidad** de cada anotación (`RN-OE-005`).

El **catálogo de tipos de anotación** es base + personalización por colegio (`RN-OB-080`). La novedad importante es la **visibilidad por anotación con tres niveles** —pública (visible al estudiante / acudiente operativo), docentes (solo personal del colegio) e interna (solo coordinación y rector)— elegida por el autor al crear (`RN-OB-081`).

El módulo de **disciplina y observaciones** se rige por `RN-DI-001..006`: acceso por rol, lectura para el estudiante, **confirmación auditada** (con fecha, hora e IP), anulación que preserva, e inmutabilidad cuando el año cerró.

## 11. Matrículas y documentos

El proceso de matrícula sigue `RN-MA-001..009`: cupos limitados por grupo, **PIN único de matrícula** con vigencia configurable, documentos requeridos por nivel, confirmación que exige documentos cargados, **creación automática de la cuenta del estudiante** al cierre del proceso, cuota de almacenamiento aplicada y auditoría completa. Los **estudiantes son independientes** entre sí: aunque un acudiente tenga varios hijos, cada cuenta opera por separado y el sistema **no agrupa pagos entre hermanos** (`RN-MT-060`).

La **gestión documental** soporta plantillas versionadas, asociación al recurso, antivirus obligatorio, inmutabilidad del documento emitido y validación de requeridos (`RN-GD-001..006`). Los **documentos cargados por el estudiante o su acudiente operativo** pasan por un **flujo de revisión administrativa** con aprobación o rechazo, y el sistema **notifica automáticamente** vencimientos; el bloqueo de servicios por documento vencido es **configurable** (`RN-GD-270`).

## 12. Pensiones, cobros y mora

Cada pago tiene **trazabilidad completa** y se prioriza la **aplicación a conceptos antiguos** primero (`RN-PP-001`, `RN-PP-002`). El **webhook de la pasarela es la fuente de verdad** (`RN-PP-003`); el **doble registro está prohibido** mediante idempotencia (`RN-PP-004`). Cualquier **conciliación manual queda auditada** (`RN-PP-005`); el **comprobante se emite automáticamente** (`RN-PP-006`); las **anulaciones requieren motivo** (`RN-PP-007`).

La **deuda es única por estudiante**, sin split entre pagadores; el colegio puede dividir cobros en cuotas pero el sistema mantiene un saldo único (`RN-PP-120`). El **retiro a mitad de mes** soporta **prorrateo configurable**; el sistema **no ejecuta devoluciones automáticas**: si hay sobrepago, queda como **saldo a favor**, y la devolución efectiva se gestiona offline (`RN-PP-121`).

Las **políticas de mora** (`RN-CM-001..006`) parten de un **catálogo legal predefinido** (`RN-PCM-140`) y permiten **diferenciar configurables por concepto** —matrícula vs. pensión vs. extras— (`RN-PCM-141`). La cartera **no bloquea automáticamente** el acceso académico (`RN-CM-001`); los topes legales se respetan (`RN-CM-002`); los **acuerdos de pago son auditables** (`RN-CM-003`); la **restricción del boletín** es configurable (`RN-CM-004`); el **paz y salvo** documenta el estado de obligaciones (`RN-CM-005`).

Las **pasarelas de pago externas** se integran con webhook firmado, idempotencia, credenciales cifradas, conciliación diaria y soporte multi-pasarela (`RN-PE-001..005`). La **matriz común de pruebas** garantiza paridad funcional entre proveedores (`RN-PE-350`); los **estados intermedios** se manejan con **alerta y reintento sin cancelación unilateral** (`RN-PE-351`).

## 13. Becas, descuentos y facturación

Las **becas y descuentos** exigen **vigencia obligatoria** y **auditoría completa** (`RN-DB-001`, `RN-DB-002`); las becas requieren **motivo registrado** (`RN-DB-003`); por defecto **no son retroactivos** (`RN-DB-004`); existe **límite acumulado** configurable (`RN-DB-005`); la **revocación queda con motivo** (`RN-DB-006`). El sistema genera un **reporte mensual configurable** de becas y descuentos otorgados (`RN-DB-110`) y soporta **traslado configurable** del beneficio cuando se cambia de plan o de año (`RN-DB-111`).

La **facturación electrónica y los recibos** siguen `RN-FR-001..005`: documento por pago, numeración consecutiva, datos actualizados al momento de emitir, nota crédito siempre referenciada al original e **inmutabilidad post-emisión**. La integración con DIAN se apoyará en **exportaciones genéricas CSV/Excel** con un **plan de cuentas configurable por colegio** (`RN-RF-320`); los **conectores específicos** (Siigo, World Office, etc.) son **evolución posterior**.

## 14. Comunicación con la comunidad

La **agenda institucional** es **unidireccional** (sin chat ni foro) (`RN-AG-001`), con permisos configurables (`RN-AG-002`), un docente solo puede dirigirse a sus grupos (`RN-AG-003`), audiencia controlada (`RN-AG-004`), edición restringida (`RN-AG-005`), archivado sin borrado (`RN-AG-006`), urgencia que salta throttling (`RN-AG-007`), adjuntos que consumen cuota (`RN-AG-008`) y expiración que no borra (`RN-AG-009`).

Los **límites de adjunto** son **20 MB por archivo y 50 MB por mensaje** (`RN-AP-200`, `RN-CC-160`). Los **destinatarios deben ser explícitos**: nada de "@todos" implícitos (`RN-AP-201`). Los **comentarios están desactivados por defecto** y deben habilitarse explícitamente para no convertir la agenda en chat (`RN-AP-202`). Las **plantillas de circular son reutilizables** (`RN-CC-161`).

La **comunicación con padres / acudientes** opera **sobre la cuenta del estudiante** (`RN-TU-410`, `RN-CP-001`). Cuando el mismo correo está vinculado a varios estudiantes (acudiente con varios hijos), el portal **puede ofrecer un selector de estudiante**, sin fusionar permisos ni expedientes (`RN-CP-002`). Los **eventos notificables** están definidos en catálogo (`RN-CP-003`); la **privacidad por estudiante** se respeta (`RN-CP-004`); las **citaciones quedan registradas** (`RN-CP-005`); el **reagendamiento es configurable** (`RN-CP-170`).

## 15. Notificaciones y mensajería

La **mensajería interna NO es chat libre**: está **ligada a un flujo** —cita, justificación, citación— y la privacidad respeta el contexto (`RN-MI-001`, `RN-MI-002`, `RN-MI-180`). Toda interacción queda auditada (`RN-MI-003`, `RN-MI-181`).

Las **notificaciones** distinguen **eventos críticos no desactivables** (cierre de matrícula, pago confirmado, alertas legales) de eventos **configurables por colegio** (`RN-NO-001`, `RN-NO-003`). La **urgencia salta el throttling** (`RN-NO-002`); las **preferencias del usuario operan dentro de los límites del colegio** (`RN-NO-004`); todos los envíos son trazables (`RN-NO-005`). Existe **agrupamiento configurable** para evitar spam (`RN-NT-190`) y **suspensión automática del envío de correo** ante bounces (`RN-NT-191`).

## 16. Multi-tenancy e identidad visual

Cada tenant tiene **identidad visual triple**: logo / colores / dominio personalizable, configurable por el colegio dentro de los límites del plan (`RN-CC-220`). El **catálogo de eventos del calendario** es base + custom por tenant (`RN-CC-221`).

El **modelo de tenants** garantiza aislamiento estricto (`RN-AI-001..005`) y soporta los matices ya descritos: cuarentena de subdominio (`RN-MT-240`), upgrades inmediatos / downgrades al cierre de ciclo (`RN-MT-241`), sesiones de soporte con consentimiento explícito y visibles para el rector (`RN-AD-210`, `RN-AD-211`).

## 17. Almacenamiento, backups y cuarentena

El **almacenamiento opera en bucket por tenant** con antivirus obligatorio, whitelist de tipos, URLs firmadas y bloqueo al 100% de la cuota con notificación al 80% (`RN-AC-001..006`). Las **cuotas se configuran por plan**: tamaños diferenciados según el tier comercial (`RN-AC-250`). Cualquier eliminación pasa por **soft-delete con cuarentena**, se notifica al superadministrador antes de la **purga definitiva**, y permite restauración dentro de la ventana (`RN-AC-251`).

Los **backups se aíslan por tenant**, se cifran en reposo, se restauran auditadamente con **RPO/RTO declarado**; la **eliminación es soft-delete por defecto** (`RN-BR-001..005`). Las **pruebas de restauración se ejecutan trimestralmente** (`RN-BR-260`) para validar que los respaldos son funcionales, no solo existentes.

## 18. Histórico, cierre y egresados

El **cierre del año lectivo es formal y único**, con auditoría completa (`RN-HA-001`). La **inmutabilidad por defecto** protege todos los datos del año cerrado (`RN-HA-002`); cualquier **reapertura debe estar motivada y registrada** (`RN-HA-003`). La **configuración relevante se versiona por año** —escalas, periodos, plantillas, plan de estudios— para que los reportes históricos sean fieles (`RN-HA-004`). Los **egresados conservan acceso al portal** con sus boletines y certificados (`RN-HA-005`); los **boletines son reimprimibles** (`RN-HA-006`).

La **reapertura intra-ventana** del año es por rol (`RN-HC-280`); la reapertura **post-cierre fuera de ventana** queda **exclusivamente en manos del superadministrador**. Los **certificados de egresados** soportan **tarifa configurable** por colegio (`RN-HC-281`).

El **log de auditoría** registra el **diff JSON entre valor previo y nuevo** y referencia un **snapshot completo** cuando aplica, para reconstruir el estado de cualquier entidad en cualquier momento (`RN-LA-001..006`, `RN-LA-290`).

## 19. Reportes y analítica

Los **KPIs operan con aislamiento estricto por tenant**: **cero benchmark cross-tenant**; ningún colegio ve métricas comparadas con otros (`RN-KP-001`, `RN-KP-300`). Los **KPIs internos** del SaaS —MRR, ARR, churn, etc.— son de **uso exclusivo del equipo de plataforma** (`RN-KP-002`, `RN-KP-301`). El **cálculo es trazable** (`RN-KP-003`) y la **frescura del dato se declara** explícitamente (`RN-KP-004`).

Los **reportes académicos** se rigen por `RN-RA-001..004`: visibilidad por rol, históricos consistentes con la configuración del año, exportación auditada y enmascaramiento de datos sensibles cuando aplica. El **catálogo de plantillas** es base + variantes administradas por el equipo (`RN-RA-310`); el **constructor visual** es funcionalidad futura.

Los **reportes financieros** (`RN-RF-001..004`) tienen **acceso restringido**, **históricos inmutables**, **auditoría de exportación** y **conciliación diaria**. La **exportación es genérica** (CSV/Excel) con **plan de cuentas configurable por colegio**; los **conectores específicos** son evolución comercial (`RN-RF-320`). Las **proyecciones financieras y los escenarios de mora avanzados quedan fuera del MVP**.

## 20. Integraciones externas

El **correo y SMS** opera con plantillas versionadas, suspensión automática por bounces, SMS y WhatsApp como canales **premium** (con cobro y modelo por definir comercialmente) y trazabilidad completa (`RN-CS-001..004`). En la **fase 1** la entrega es **best effort por canal** (`RN-CS-330`): se intenta el canal solicitado, se reintenta y, si falla, se cae al canal alternativo configurado.

Las **otras integraciones** (`RN-OI-001..005`) son **activadas por colegio**, con credenciales cifradas, **SSO que no sustituye permisos**, trazabilidad completa y aislamiento entre tenants. **LMS y aula virtual** se construyen como **módulos nativos** del producto, **no como integraciones externas** (`RN-OI-340`), porque son parte del corazón académico.

Las **pasarelas de pago externas** ya descritas en la sección 12 (`RN-PE-001..005`, `RN-PE-350`, `RN-PE-351`) cubren conciliación, idempotencia y matriz común de pruebas.

## 21. Plataforma, operación y soporte

El **soporte y observabilidad** se apoya en el log de auditoría, los backups con prueba periódica y el flujo de sesiones de soporte con consentimiento del rector (`RN-AD-210`, `RN-AD-211`). El superadministrador interviene de forma puntual y siempre auditada.

Las **cuotas de almacenamiento** se calibran por plan (`RN-AC-250`); la **purga** siempre es soft-delete + cuarentena + notificación previa (`RN-AC-251`). La **gestión documental** institucional incluye flujo de revisión con aprobación/rechazo y notificación automática al vencimiento (`RN-GD-270`).

La **reapertura del año cerrado** está controlada por permisos y limitada en ventana (`RN-HC-280`). Los **certificados de egresados** son emitibles desde el portal con cobro configurable (`RN-HC-281`).

## 22. Auditoría, seguridad, internacionalización y validaciones

El **log de auditoría es append-only** y **preserva valores previo y nuevo** con IP y user-agent (`RN-LA-001`, `RN-LA-003`, `RN-LA-004`). Las **acciones privilegiadas se auditan doblemente** (`RN-LA-002`); la **retención es legal** y configurable (`RN-LA-005`); el **acceso al log mismo está auditado** (`RN-LA-006`). El registro guarda **diff JSON + snapshot** cuando la operación lo amerita (`RN-LA-290`).

La **seguridad** descansa sobre: aislamiento estricto por tenant (`RN-AI-001`), MFA obligatorio para roles de alto privilegio con expansión progresiva (`RN-RG-421`), credenciales temporales en alta y cambio en primer login (`RN-AU-360`), credenciales de integraciones cifradas (`RN-OI-002`), validación dual frontend/backend con backend autoritativo (`RN-VL-430`), e impersonación restringida al superadministrador (`RN-RT-402`).

La **internacionalización está activa desde el MVP** con `es-CO` como locale por defecto y un **catálogo i18n compartido entre frontend y backend** para mensajes de validación y notificaciones (`RN-RG-420`, `RN-VL-430`). Nuevos locales se incorporan progresivamente.

Las **validaciones** se aplican como **defensa en profundidad**: el frontend valida formato y experiencia de usuario; el **backend es la autoridad de seguridad** y **nunca se confía solo en el frontend** (`RN-VL-430`).

---

## Apéndice — Decisiones externas pendientes

Estas decisiones no son técnicas y se definen fuera del vault, pero condicionan parte de la implementación:

1. **Bandas de precio** y **tope del modelo B2B2C** (comercial).
2. **Default de quién asume la comisión** de pasarela (colegio vs. pagador) cuando el colegio no lo elige explícitamente.
3. **Proveedor DIAN** para facturación electrónica del SaaS al colegio.
4. **Segundo país piloto** tras Colombia.
5. **Cuotas finales de almacenamiento por plan** (`RN-AC-250`).
6. **Política de reembolso anual prepago** del SaaS al colegio.
7. **Costo y modelo de cobro** de WhatsApp como canal premium (`RN-CS-003`).
8. **Lista exacta de reportes incluidos por plan**, gestionada vía sistema de suscripciones y permisos comerciales (`RN-RA-310`).

## Apéndice — Funcionalidades futuras

- **Constructor visual de plantillas** de boletines y certificados (hoy: catálogo base + variantes administradas).
- **Vista consolidada multi-hijo** para acudientes con varios estudiantes (hoy: selector de estudiante por correo común).
- **Importación masiva de notas**.
- **Conectores contables específicos** (Siigo, World Office, etc.).
- **Análisis predictivo** y **proyecciones financieras avanzadas**.
- **App móvil nativa** para estudiantes y acudientes operativos.
- **FSM formal** documentada e **índice automático de RN**.

---

> Para detalles operativos, ver el [[00-indice|índice del vault]] y los archivos por módulo. Cualquier cambio sustantivo a una RN debe reflejarse en este resumen.
