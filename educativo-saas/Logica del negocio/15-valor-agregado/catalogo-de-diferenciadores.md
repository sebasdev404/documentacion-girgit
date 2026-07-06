---
titulo: Catálogo de diferenciadores (valor agregado estándar)
modulo: valor-agregado
tipo: referencia
estado: borrador
tags: [valor-agregado, diferenciadores, competencia, roadmap]
---

# Catálogo de diferenciadores (valor agregado estándar)

Este módulo cataloga las **funcionalidades de valor agregado estándar** (`RN-VA-001` a `RN-VA-007`) que diferencian la plataforma frente a la competencia colombiana (**Phidias**, **Master2000**, **Ciudad Educativa**). Son features vendibles de bajo riesgo, sin componente de IA. Cada una es **opt-in y configurable por colegio**; varias dependen del plan contratado (ver [[../06-monetizacion-y-pagos/planes-y-suscripciones|Planes y suscripciones]]).

> **Aclaración estructural:** "acudiente" / "padre de familia" **no es un tipo de usuario propio**. El **estudiante** posee la única cuenta del menor y el acudiente la opera en la práctica. Toda referencia a "acudiente" se traduce a **"el usuario del estudiante"** (ver `RN-TU-410` en [[../02-usuarios-roles-y-permisos/tipos-de-usuario|Tipos de usuario]]).

## Cómo leer este catálogo

Cada diferenciador se describe con: **qué es**, **valor diferencial** frente a la competencia, **a quién beneficia**, **dependencias** (módulos previos requeridos) y **prioridad** de roadmap (`P1` = primero al mercado, `P3` = deseable). Las reglas operativas viven en `## Reglas de negocio`.

---

## RN-VA-001 — App / Portal de acudientes (push + vista multi-hijo)

- **Qué es:** aplicación móvil y portal responsive para que el usuario del estudiante consulte notas, asistencia, observador, estado de cuenta y comunicados, con **notificaciones push** y un **selector multi-hijo** cuando un mismo correo de acudiente está vinculado a varias cuentas de estudiante.
- **Valor diferencial:** Phidias y Master2000 son fuertes en web pero débiles en app nativa con push; la **vista consolidada multi-hijo** (un solo acceso para ver a todos los hijos sin re-loguearse) adelanta una capacidad hoy diferida en el roadmap base.
- **A quién beneficia:** acudientes (experiencia móvil real), colegio (mayor adopción y menos llamadas a secretaría).
- **Dependencias:** [[../05-comunicacion/notificaciones|Notificaciones]], [[../02-usuarios-roles-y-permisos/portal-del-estudiante|Portal del estudiante]], [[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos de pensiones]].
- **Prioridad:** P1.

## RN-VA-002 — Pagos sin fricción (medios locales + débito recurrente)

- **Qué es:** pago de pensiones y otros conceptos con **PSE, Nequi, Daviplata, link de pago, débito recurrente (domiciliación)** y **recordatorios automáticos** antes y después del vencimiento.
- **Valor diferencial:** la competencia suele limitarse a PSE o tarjeta; sumar **Nequi/Daviplata + débito recurrente + link de pago** cubre los medios reales de la familia colombiana y **reduce cartera** al automatizar el cobro mensual.
- **A quién beneficia:** acudiente (paga en menos clics), colegio (menos mora y conciliación manual), proveedor (más GMV transaccional).
- **Dependencias:** [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]], [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|Políticas de cobro y mora]], [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]].
- **Prioridad:** P1.

## RN-VA-003 — WhatsApp como canal oficial

- **Qué es:** canal de WhatsApp (API oficial / plantillas aprobadas) para comunicados, aviso de notas, estado de cuenta y recordatorios de pago, integrado con el motor de notificaciones.
- **Valor diferencial:** los padres colombianos viven en WhatsApp; la **tasa de lectura supera ampliamente al correo**. Es un canal que la competencia ofrece de forma limitada o como add-on costoso.
- **A quién beneficia:** colegio (mensajes que sí se leen), acudiente (recibe en el canal que ya usa).
- **Dependencias:** [[../10-integraciones-externas/correo-y-sms|Correo y SMS]], [[../05-comunicacion/circulares-y-comunicados|Circulares y comunicados]], [[../06-monetizacion-y-pagos/modelo-de-negocio|Modelo de negocio]] (costo por mensaje premium).
- **Prioridad:** P1.

## RN-VA-004 — Firma electrónica de documentos

- **Qué es:** firma electrónica de contrato de matrícula, autorizaciones (salidas, imagen), paz y salvo y demás documentos, con sello de tiempo y trazabilidad legal.
- **Valor diferencial:** elimina el papel y las filas de firma presencial; **acelera la matrícula** y deja evidencia auditable. Pocos competidores lo ofrecen nativo.
- **A quién beneficia:** secretaría académica (menos papel y archivo físico), acudiente (firma desde casa), colegio (soporte legal).
- **Dependencias:** [[../11-plataforma-y-operacion/gestion-documental|Gestión documental]], [[../04-procesos-academicos/matriculas|Matrículas]], [[../11-plataforma-y-operacion/log-de-auditoria|Log de auditoría]], [[../13-cumplimiento-colombia/habeas-data-y-consentimientos|Habeas Data]].
- **Prioridad:** P2.

## RN-VA-005 — Carné digital con QR y control de acceso

- **Qué es:** carné digital del estudiante con **código QR** que sirve para control de entrada/salida en portería; al registrarse el ingreso o la salida se **notifica al usuario del estudiante**.
- **Valor diferencial:** funcionalidad de seguridad que la competencia rara vez integra al SIS; genera **dato de asistencia** y tranquilidad al acudiente sin hardware costoso (basta un lector/celular en portería).
- **A quién beneficia:** acudiente (aviso de ingreso/salida), colegio (control de acceso y seguridad), coordinación (cruce con asistencia).
- **Dependencias:** [[../04-procesos-academicos/asistencia|Asistencia]], [[../05-comunicacion/notificaciones|Notificaciones]], [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]] (portería como punto de control).
- **Prioridad:** P2.

## RN-VA-006 — Tablero ejecutivo en tiempo real para el Rector

- **Qué es:** panel único con cartera, asistencia, convivencia y desempeño académico **en tiempo (casi) real**, con semáforos y drill-down por sede, jornada, grado y grupo.
- **Valor diferencial:** consolida en una pantalla lo que en la competencia exige varios reportes exportados; orientado a la **decisión directiva**, no solo a la operación.
- **A quién beneficia:** rector / administrador del colegio (visión 360 inmediata), coordinaciones (foco en focos de riesgo).
- **Dependencias:** [[../09-reportes-y-analitica/indicadores-kpi|Indicadores y KPI]], [[../09-reportes-y-analitica/reportes-financieros|Reportes financieros]], [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]], [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rector]].
- **Prioridad:** P2.

## RN-VA-007 — Generador automático de horarios

- **Qué es:** motor de optimización con restricciones (docente, aula, grupo, intensidad horaria, jornada) que **propone un horario válido** y minimiza conflictos y huecos; la coordinación ajusta y aprueba.
- **Valor diferencial:** la competencia normalmente exige armar el horario a mano; **ahorra días de trabajo** a la coordinación académica cada inicio de año.
- **A quién beneficia:** coordinador académico (ahorro de tiempo), colegio (horario sin conflictos desde el día 1).
- **Dependencias:** [[../04-procesos-academicos/horarios|Horarios]], [[../04-procesos-academicos/asignacion-docentes|Asignación de docentes]], [[../04-procesos-academicos/plan-de-estudios|Plan de estudios]], [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]].
- **Prioridad:** P3.

---

## Estados y disponibilidad por feature

Cada diferenciador atraviesa los mismos estados de disponibilidad dentro del tenant:

| Estado | Significado |
| --- | --- |
| No incluido | El plan del colegio no contempla la feature. No aparece en la consola. |
| Disponible | El plan la incluye pero el colegio aún no la activó (opt-in pendiente). |
| Activa | El colegio la activó y configuró; visible para los roles habilitados. |
| Suspendida | Activa pero pausada por mora del colegio, falla de un proveedor externo o decisión del colegio. |

Transiciones: `No incluido -> Disponible` (cambio de plan); `Disponible -> Activa` (opt-in + configuración); `Activa <-> Suspendida` (mora, incidente externo o decisión); `Activa -> Disponible` (desactivación voluntaria, conservando histórico).

## Configurabilidad por colegio

- Cada feature es **opt-in independiente** y se habilita según el plan (ver [[../06-monetizacion-y-pagos/planes-y-suscripciones|Planes y suscripciones]]).
- Los **medios de pago** (`RN-VA-002`), los **canales** (`RN-VA-003`) y los **eventos notificables** se activan/desactivan por colegio.
- El **tablero ejecutivo** (`RN-VA-006`) permite ocultar widgets sensibles según política de la institución.
- Quién asume el costo transaccional o de mensajería premium se define por colegio (coherente con [[../06-monetizacion-y-pagos/modelo-de-negocio|Modelo de negocio]]).

## Integraciones con otros módulos

Los diferenciadores **no son módulos aislados**: reutilizan la infraestructura existente. Pagos sin fricción se apoya en [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]]; WhatsApp y push extienden [[../05-comunicacion/notificaciones|Notificaciones]]; firma electrónica se ancla en [[../11-plataforma-y-operacion/gestion-documental|Gestión documental]]; el carné QR alimenta [[../04-procesos-academicos/asistencia|Asistencia]]; el tablero consume [[../09-reportes-y-analitica/indicadores-kpi|Indicadores y KPI]]; y el generador de horarios opera sobre [[../04-procesos-academicos/horarios|Horarios]].

## Reglas de negocio

- **RN-VA-001 — App con vista multi-hijo sin fusión de expedientes:** la app permite a un mismo correo de acudiente alternar entre las cuentas de varios estudiantes mediante un selector, **sin fusionar expedientes ni permisos**; cada estudiante conserva su privacidad (alineado con `RN-CP-002` y `RN-CP-004`).
- **RN-VA-002 — Medios de pago configurables por colegio:** cada colegio activa el subconjunto de medios (PSE, Nequi, Daviplata, link de pago, débito recurrente) que ofrece; el desglose de comisiones se muestra al pagador antes de confirmar (coherente con `RN-MN-002`).
- **RN-VA-003 — WhatsApp solo con consentimiento y plantillas aprobadas:** el envío por WhatsApp requiere **opt-in del usuario del estudiante** y el uso de plantillas aprobadas por el proveedor; sin consentimiento o sin plantilla válida el sistema cae al canal por defecto (portal + correo).
- **RN-VA-004 — Firma electrónica con trazabilidad inmutable:** todo documento firmado registra firmante, fecha, hora, IP y hash del documento en el [[../11-plataforma-y-operacion/log-de-auditoria|log de auditoría]]; el documento firmado **no se puede alterar** sin invalidar la firma.
- **RN-VA-005 — Registro de acceso por QR notifica al usuario del estudiante:** cada lectura válida del carné en portería genera un evento de ingreso/salida y dispara la notificación; un QR vencido, suspendido o de estudiante no matriculado **es rechazado** y se registra el intento.
- **RN-VA-006 — Tablero respeta alcance y permisos del rol:** el tablero ejecutivo solo muestra datos del tenant del rector y respeta la [[../02-usuarios-roles-y-permisos/matriz-de-permisos|matriz de permisos]]; el drill-down nunca expone datos de otro colegio (aislamiento por tenant).
- **RN-VA-007 — Horario generado requiere aprobación humana:** la propuesta del generador automático **no se publica sola**; queda en borrador hasta que el coordinador académico la revisa y aprueba, y siempre cumple las validaciones de conflicto de `RN-HO-001`.
- **RN-VA-008 — Activación condicionada al plan y al estado del colegio:** una feature de valor agregado solo puede pasar a `Activa` si el plan la incluye y el colegio está al día; ante mora del colegio o caída de un proveedor externo, la feature pasa a `Suspendida` sin perder configuración ni histórico.

## Notas y pendientes

- **[Decisión tomada]** El catálogo estándar (`RN-VA-001..007`) son features **sin IA**, opt-in por colegio.
- **[Decisión tomada]** Toda feature es **opt-in y configurable por colegio**, vinculada al plan contratado.
- **[Pendiente — producto]** Definir si el **débito recurrente** (`RN-VA-002`) se ofrece desde el MVP o en una segunda fase, según la pasarela elegida y los requisitos de domiciliación bancaria en Colombia.
- **[Pendiente — producto]** Decidir si el **carné digital con QR** (`RN-VA-005`) incluye lector propio para portería o se apoya en la cámara del celular del portero en el MVP.
- **[Pendiente — comercial]** Definir qué features entran en el plan base y cuáles son add-on premium, en conjunto con [[../06-monetizacion-y-pagos/planes-y-suscripciones|Planes y suscripciones]].
- **[Pendiente — legal]** Validar el proveedor de **firma electrónica** (`RN-VA-004`) y su nivel de validez jurídica (firma electrónica simple vs. avanzada) frente a la normativa colombiana.

## Documentos relacionados

- [[../../_PLAN MAESTRO DE COMPLETADO|Plan Maestro de Completado]] — origen de los IDs `RN-VA` y prioridades.
- [[../02-usuarios-roles-y-permisos/tipos-de-usuario|Tipos de usuario]] — modelo de cuenta del estudiante (acudiente no usuario).
- [[../02-usuarios-roles-y-permisos/matriz-de-permisos|Matriz de permisos]] — alcance de roles para el tablero ejecutivo.
- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]] — fuente del tablero de convivencia.
- [[../04-procesos-academicos/horarios|Horarios]] — base del generador automático.
- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]] — portería como punto de control de acceso.
- [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]] — medios de pago sin fricción.
- [[../06-monetizacion-y-pagos/planes-y-suscripciones|Planes y suscripciones]] — qué plan habilita cada feature.
- [[../05-comunicacion/notificaciones|Notificaciones]] — base de push, WhatsApp y avisos de acceso.
- [[../11-plataforma-y-operacion/gestion-documental|Gestión documental]] — soporte de la firma electrónica.
