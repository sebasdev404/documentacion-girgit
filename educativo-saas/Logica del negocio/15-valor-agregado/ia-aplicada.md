---
titulo: IA aplicada (valor agregado con IA selectiva)
modulo: valor-agregado
tipo: referencia
estado: borrador
tags: [valor-agregado, ia, claude, alertas-tempranas, guardrails]
---

# IA aplicada (valor agregado con IA selectiva)

Este módulo documenta las **tres apuestas de IA selectiva** (`RN-VA-101` a `RN-VA-103`) de la plataforma. A diferencia del [[catalogo-de-diferenciadores|catálogo de diferenciadores]] (features sin IA), aquí la IA agrega valor en tareas acotadas y de alto retorno, **siempre con humano en el bucle** y bajo el principio de que la IA **propone y la persona decide**. Los modelos usados son de la familia **Claude (Anthropic)**: Claude Haiku 4.5 para alto volumen y bajo costo, Claude Sonnet 4.6 para redacción de calidad, y Claude Opus 4.8 reservado solo para razonamiento complejo.

> **Aclaración estructural:** "acudiente" / "padre de familia" **no es un tipo de usuario propio**. El **estudiante** posee la única cuenta del menor y el acudiente la opera en la práctica. Toda referencia a "acudiente" se traduce a **"el usuario del estudiante"** (ver `RN-TU-410` en [[../02-usuarios-roles-y-permisos/tipos-de-usuario|Tipos de usuario]]).

## Principios obligatorios de IA

Estos principios aplican a **toda** feature de este módulo y no son configurables a la baja por el colegio:

- **Humano en el bucle:** ninguna decisión que afecte al estudiante (riesgo, observación, certificado, comunicación a la familia) se ejecuta de forma autónoma. La IA produce un **borrador o sugerencia**; un rol con permiso revisa, edita y aprueba.
- **Trazabilidad:** cada invocación registra en el [[../11-plataforma-y-operacion/log-de-auditoria|log de auditoría]] el prompt enviado, el modelo usado, la salida generada, el usuario que la solicitó y quién la aprobó o descartó. La salida sin aprobar **no tiene efecto** en el expediente.
- **Aislamiento por tenant:** el contexto enviado al modelo se arma **solo** con datos del tenant que origina la solicitud. Nunca se mezclan datos de dos colegios en un mismo prompt ni en una misma respuesta.
- **Opt-in del colegio:** cada feature de IA es **opt-in independiente**; el colegio la activa explícitamente y acepta las condiciones de uso de IA. Por defecto está **desactivada**.
- **Sin entrenamiento con datos del menor:** los datos de estudiantes **no se usan para entrenar ni afinar modelos**. Las llamadas se hacen bajo acuerdo de no-retención / no-entrenamiento con el proveedor, coherente con [[../13-cumplimiento-colombia/habeas-data-y-consentimientos|Habeas Data]].

---

## RN-VA-101 — Alertas tempranas de riesgo

- **Qué es:** motor que detecta estudiantes en **riesgo de deserción, bajo rendimiento o convivencia** y emite un **semáforo** (verde / amarillo / rojo) con una **explicación en lenguaje natural** y una recomendación de acompañamiento. La decisión de actuar es siempre humana (director de grupo, coordinación, orientación).
- **Cómo funciona:** un **scoring propio y determinista** (reglas + umbrales configurables) cruza señales de varios módulos y produce el nivel de riesgo y los factores que lo explican. Solo **después** se invoca a Claude para **traducir** esos factores numéricos a una explicación clara para el docente. El modelo **no calcula el riesgo**; solo redacta la explicación de un resultado ya calculado por el sistema.
- **Datos que usa:** [[../04-procesos-academicos/asistencia|asistencia]] (inasistencias y tardanzas), [[../04-procesos-academicos/calificaciones|calificaciones]] (notas y tendencia), [[../04-procesos-academicos/observador-del-estudiante|observador del estudiante]] (anotaciones y seguimientos), y [[../06-monetizacion-y-pagos/pagos-de-pensiones|cartera]] (mora sostenida como señal de riesgo de deserción).
- **Modelo Claude sugerido:** **Claude Haiku 4.5** — alto volumen (cientos de estudiantes por corrida), bajo costo y latencia. La explicación es texto corto y estructurado, no requiere razonamiento complejo.
- **Guardrails:** el modelo recibe **solo los factores ya calculados** (nunca recalcula el score); la alerta nace en estado `Sugerida` y un rol con permiso debe revisarla; el semáforo **nunca** se comunica al acudiente de forma automática; los datos de cartera se usan como señal interna y **no se exponen** en la explicación que ve el docente, para no estigmatizar.

## RN-VA-102 — Asistente de redacción de observaciones y boletín

- **Qué es:** asistente que genera **borradores** de anotaciones del observador y de **comentarios cualitativos del boletín** a partir de los indicadores del estudiante. El docente **edita y aprueba**; nada se publica sin su firma.
- **Cómo funciona:** el docente selecciona al estudiante y el tipo de texto (observación de convivencia, comentario de desempeño, refuerzo). El sistema arma el contexto con los indicadores del periodo y Claude devuelve un borrador en tono institucional. El docente lo ajusta y lo guarda; recién entonces entra al expediente.
- **Datos que usa:** [[../04-procesos-academicos/logros-e-indicadores|logros e indicadores]] del periodo, [[../04-procesos-academicos/calificaciones|calificaciones]], y la guía de estilo del colegio (tono, longitud, vocabulario permitido) configurada por la institución.
- **Modelo Claude sugerido:** **Claude Sonnet 4.6** — redacción de calidad, coherente con el tono institucional y sensible al matiz pedagógico, sin el costo de Opus.
- **Guardrails:** el texto sale marcado como **borrador generado por IA** hasta que el docente lo aprueba; el modelo no inventa hechos no soportados por los indicadores (no asigna notas ni eventos inexistentes); se prohíbe lenguaje despectivo o juicios sobre la familia; la versión final guardada es la **editada por el humano**, no la cruda del modelo.

## RN-VA-103 — Asistente conversacional para acudientes

- **Qué es:** asistente de chat (en el portal y en [[../05-comunicacion/comunicacion-con-padres|WhatsApp]]) que responde a los acudientes sobre **estado de cuenta, fechas del [[../04-procesos-academicos/calendario-escolar|calendario]], requisitos y emisión de certificados de estudio o paz y salvo**, con escalamiento a una persona cuando la consulta excede su alcance.
- **Cómo funciona:** el asistente usa **recuperación sobre datos del propio estudiante** (consultas parametrizadas, no acceso libre a la BD). Para emitir un [[../11-plataforma-y-operacion/gestion-documental|certificado]] o un [[../06-monetizacion-y-pagos/paz-y-salvo|paz y salvo]], dispara el flujo oficial del módulo correspondiente; el asistente **no genera el documento por su cuenta**, solo lo solicita y entrega el resultado del sistema.
- **Datos que usa:** estado de cuenta de [[../06-monetizacion-y-pagos/pagos-de-pensiones|pagos de pensiones]], [[../04-procesos-academicos/calendario-escolar|calendario escolar]], plantillas de [[../11-plataforma-y-operacion/gestion-documental|gestión documental]], y el vínculo acudiente-estudiante para resolver el alcance.
- **Modelo Claude sugerido:** **Claude Haiku 4.5** para el grueso de respuestas (alto volumen, bajo costo); escalar a **Claude Sonnet 4.6** solo si el colegio exige un tono de atención más elaborado.
- **Guardrails:** el asistente solo accede a datos de los estudiantes **vinculados a ese acudiente** (alcance por vínculo); ante temas sensibles (convivencia, salud, reclamos disciplinarios) **escala a un humano** y no improvisa; no revela notas de otros estudiantes ni datos internos; toda conversación queda en el log; si la confianza es baja, responde con un mensaje seguro de derivación a secretaría.

---

## Estados y transiciones de una salida de IA

Toda salida de IA que afecte al estudiante atraviesa el mismo ciclo, lo que materializa el principio de humano en el bucle:

| Estado | Significado |
| --- | --- |
| Sugerida | La IA generó un borrador o alerta. Visible solo para el rol responsable; sin efecto en el expediente. |
| Aprobada | Un rol con permiso revisó y aceptó (con o sin edición). Recién aquí surte efecto. |
| Editada | El humano modificó el borrador antes de aprobar; se guarda la versión humana, no la cruda. |
| Descartada | El rol rechazó la sugerencia. Queda registrada en el log, sin impacto en el estudiante. |

Transiciones: `Sugerida -> Aprobada`, `Sugerida -> Editada -> Aprobada`, `Sugerida -> Descartada`. No existe transición que publique una salida **sin pasar por un humano**.

## Configurabilidad por colegio

- Cada feature (`RN-VA-101..103`) es **opt-in independiente**; el colegio puede activar una sin activar las otras.
- El colegio define los **umbrales del scoring** de alertas (qué cuenta como amarillo o rojo) y qué señales pesan, respetando los mínimos del sistema.
- La **guía de estilo** del asistente de redacción (tono, longitud, vocabulario) se configura por institución.
- El colegio define el **alcance temático** y el punto de **escalamiento a humano** del asistente conversacional.
- El colegio elige el **canal** del asistente conversacional (solo portal, o portal + WhatsApp), coherente con `RN-VA-003`.

## Integraciones con otros módulos

La IA **no es un módulo aislado**: consume los datos existentes y devuelve sus salidas a los flujos ya documentados. Las alertas (`RN-VA-101`) cruzan [[../04-procesos-academicos/asistencia|asistencia]], [[../04-procesos-academicos/calificaciones|calificaciones]], [[../04-procesos-academicos/observador-del-estudiante|observador]] y [[../06-monetizacion-y-pagos/pagos-de-pensiones|cartera]], y se muestran en el [[catalogo-de-diferenciadores|tablero ejecutivo]] (`RN-VA-006`); el asistente de redacción (`RN-VA-102`) alimenta el observador y los [[../04-procesos-academicos/boletines-y-reportes-academicos|boletines]]; el asistente conversacional (`RN-VA-103`) se apoya en [[../05-comunicacion/notificaciones|notificaciones]] y [[../11-plataforma-y-operacion/gestion-documental|gestión documental]]. Toda invocación se ancla en el [[../11-plataforma-y-operacion/log-de-auditoria|log de auditoría]].

## Reglas de negocio

- **RN-VA-110 — Humano en el bucle obligatorio:** ninguna salida de IA que afecte al estudiante surte efecto en estado `Sugerida`; requiere `Aprobada` o `Editada -> Aprobada` por un rol con permiso. No existe publicación autónoma.
- **RN-VA-111 — Scoring determinista, IA solo explica:** el nivel de riesgo de `RN-VA-101` lo calcula el motor propio de reglas; Claude **solo redacta la explicación** del resultado y nunca altera el score.
- **RN-VA-112 — Trazabilidad completa del prompt y la salida:** cada invocación registra en el [[../11-plataforma-y-operacion/log-de-auditoria|log de auditoría]] prompt, modelo, salida, solicitante y aprobador. Una salida sin registro de aprobación **no impacta** el expediente.
- **RN-VA-113 — Aislamiento por tenant en el contexto:** el contexto enviado al modelo se arma exclusivamente con datos del tenant solicitante; queda prohibido mezclar datos de dos colegios en un prompt o respuesta.
- **RN-VA-114 — Opt-in por colegio y por feature:** cada feature de IA está desactivada por defecto y solo se habilita con activación explícita del colegio y aceptación de las condiciones de uso de IA.
- **RN-VA-115 — Sin entrenamiento con datos del menor:** los datos de estudiantes no se usan para entrenar ni afinar modelos; las llamadas se hacen bajo acuerdo de no-retención/no-entrenamiento con el proveedor.
- **RN-VA-116 — Alcance por vínculo en el asistente conversacional:** `RN-VA-103` solo accede a datos de los estudiantes vinculados al acudiente que pregunta; cualquier dato fuera de ese vínculo es inaccesible.
- **RN-VA-117 — Escalamiento ante temas sensibles:** ante consultas de convivencia, salud, reclamos disciplinarios o baja confianza, el asistente conversacional escala a un humano y no improvisa respuestas.
- **RN-VA-118 — Selección de modelo por tarea:** se usa Claude Haiku 4.5 para alto volumen/bajo costo (`RN-VA-101`, `RN-VA-103`), Claude Sonnet 4.6 para redacción de calidad (`RN-VA-102`) y Claude Opus 4.8 solo cuando una tarea exija razonamiento complejo justificado.
- **RN-VA-119 — IA no genera documentos oficiales por su cuenta:** certificados, paz y salvo y boletines se emiten por el flujo oficial de su módulo; la IA solo solicita o redacta borradores, nunca produce el documento final con validez por sí misma.

## Notas y pendientes

- **[Decisión tomada]** La IA es **selectiva y con humano en el bucle**; se descarta cualquier automatización que afecte al estudiante sin aprobación humana. Origen en la sección C del [[../../_PLAN MAESTRO DE COMPLETADO|Plan Maestro de Completado]].
- **[Decisión tomada]** El score de riesgo (`RN-VA-101`) es **determinista y propio**; Claude solo redacta la explicación, no calcula el riesgo.
- **[Pendiente — producto]** Definir los **umbrales por defecto** del semáforo de riesgo (qué inasistencia, qué caída de notas o qué mora dispara amarillo vs. rojo) como base configurable por colegio.
- **[Pendiente — producto]** Decidir si el asistente conversacional (`RN-VA-103`) entra al MVP en el portal y deja WhatsApp para una segunda fase, atado a `RN-VA-003`.
- **[Pendiente — legal]** Validar la **cláusula de no-retención/no-entrenamiento** con el proveedor de IA y reflejarla en los consentimientos de [[../13-cumplimiento-colombia/habeas-data-y-consentimientos|Habeas Data]].
- **[Pendiente — comercial]** Definir si las features de IA son **add-on premium** o parte del plan, en conjunto con [[../06-monetizacion-y-pagos/planes-y-suscripciones|Planes y suscripciones]].

## Documentos relacionados

- [[catalogo-de-diferenciadores|Catálogo de diferenciadores]] — valor agregado estándar sin IA; el tablero ejecutivo consume las alertas.
- [[../../_PLAN MAESTRO DE COMPLETADO|Plan Maestro de Completado]] — origen de los IDs `RN-VA-101..103` y los principios de IA.
- [[../11-plataforma-y-operacion/log-de-auditoria|Log de auditoría]] — trazabilidad obligatoria de prompts y salidas.
- [[../13-cumplimiento-colombia/habeas-data-y-consentimientos|Habeas Data y consentimientos]] — tratamiento de datos del menor y no-entrenamiento.
- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]] — fuente de las alertas y destino de la redacción asistida.
- [[../04-procesos-academicos/asistencia|Asistencia]] — señal de las alertas tempranas.
- [[../04-procesos-academicos/calificaciones|Calificaciones]] — señal de riesgo y base del comentario de boletín.
- [[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos de pensiones]] — estado de cuenta y señal de cartera.
- [[../05-comunicacion/comunicacion-con-padres|Comunicación con padres]] — canal del asistente conversacional.
- [[../02-usuarios-roles-y-permisos/matriz-de-permisos|Matriz de permisos]] — quién puede aprobar salidas de IA.
