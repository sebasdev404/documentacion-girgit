---
titulo: Convivencia escolar (Ley 1620)
modulo: cumplimiento-colombia
tipo: proceso
estado: borrador
tags: [convivencia, ley-1620, cumplimiento, comite-convivencia, rai, legal]
---

# Convivencia escolar (Ley 1620)

## Descripción

Proceso que da soporte al Sistema Nacional de Convivencia Escolar exigido por la **Ley 1620 de 2013** y su Decreto reglamentario **1965 de 2013** (hoy compilado en el Decreto Único 1075 de 2015). Cubre el **Comité Escolar de Convivencia (CEC)**, la clasificación de **situaciones tipo I, II y III**, la **Ruta de Atención Integral (RAI)** con sus cuatro componentes (promoción, prevención, atención y seguimiento), y el registro y seguimiento de casos articulado con el [[../04-procesos-academicos/observador-del-estudiante|observador del estudiante]] y la coordinación de convivencia. Es **requisito legal**: todo colegio debe tenerlo operando.

## Objetivo del proceso

Garantizar que cada caso de convivencia se clasifique, atienda y registre conforme a la ruta y los protocolos exigidos por la ley, dejando trazabilidad inmutable para auditoría, para el reporte al Sistema de Información Unificado de Convivencia Escolar (SIUCE) y para la respuesta ante autoridades cuando aplique.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Recibe, clasifica y activa la ruta; secretaría técnica del comité; consolida actas y seguimiento. |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Rector / Administrador del Colegio]] | Preside el Comité Escolar de Convivencia; firma actas; decide situaciones tipo III y reportes a autoridades. |
| [[../02-usuarios-roles-y-permisos/roles/07-director-de-grupo\|Director de Grupo]] | Reporta situaciones de su grupo, acompaña al estudiante y ejecuta acuerdos de seguimiento. |
| [[../02-usuarios-roles-y-permisos/roles/06-docente\|Docente]] | Reporta situaciones observadas en aula y aplica medidas pedagógicas inmediatas (tipo I). |
| [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | Es parte del caso; consulta lo que le corresponde y firma acuerdos y compromisos. |
| Orientación escolar | Recibe remisiones, hace seguimiento psicosocial y aporta al caso (ver bienestar y orientación). |

## Composición del Comité Escolar de Convivencia (CEC)

El comité es **obligatorio** y su composición mínima la fija la ley. El sistema permite registrar a los integrantes por año lectivo:

| Integrante | Notas |
| --- | --- |
| Rector (preside) | Obligatorio. |
| Personero estudiantil | Obligatorio. |
| Docente con función de orientación | Obligatorio si existe en el colegio. |
| Coordinador de convivencia | Actúa como secretaría técnica (configurable por colegio). |
| Presidente del consejo de padres | Obligatorio. |
| Presidente del consejo estudiantil | Obligatorio. |
| Docente líder de procesos de convivencia | Configurable por colegio. |

## Clasificación de situaciones (tipo I, II y III)

La tipificación es **fija por ley** y determina la ruta y el protocolo aplicable:

| Tipo | Definición legal | Quién resuelve | Reporte externo |
| --- | --- | --- | --- |
| **Tipo I** | Conflictos manejados inoportunamente y situaciones esporádicas que inciden negativamente en el clima escolar y no generan daño al cuerpo ni a la salud. | Docente / director de grupo, en el aula. | No. |
| **Tipo II** | Situaciones de agresión escolar, acoso (bullying) y ciberacoso que no revisten las características de un delito; o que causan daño al cuerpo o a la salud sin generar incapacidad. | Comité Escolar de Convivencia. | Remisión a EPS / salud cuando hay afectación física. |
| **Tipo III** | Situaciones que constituyen presunto delito (abuso, violencia sexual, porte de armas, etc.). | Rector activa protocolo y reporta a autoridad competente. | Obligatorio: Policía de Infancia, ICBF, Fiscalía y/o autoridad de salud según el caso. |

## Ruta de Atención Integral (RAI) y sus componentes

La RAI organiza la respuesta institucional en cuatro componentes que el módulo modela de forma diferenciada:

| Componente | Qué cubre en el sistema |
| --- | --- |
| **Promoción** | Definición del manual de convivencia vigente, proyectos pedagógicos y movilización de la comunidad. Se registra como configuración institucional del año. |
| **Prevención** | Identificación de factores de riesgo (cruce con asistencia, observador y alertas tempranas) y acciones para evitar la ocurrencia de situaciones. |
| **Atención** | Activación del protocolo según el tipo, con plazos, responsables y registro de actuaciones. Es el núcleo operativo del caso. |
| **Seguimiento** | Verificación del cumplimiento de acuerdos y de la efectividad de la medida; reapertura del caso si reincide. |

## Flujo principal

1. Cualquier actor autorizado (docente, director de grupo, coordinador) **reporta** una situación desde el módulo o desde el observador.
2. El **coordinador de convivencia clasifica** la situación en tipo I, II o III. La clasificación queda auditada y puede reclasificarse con justificación.
3. El sistema **activa el protocolo** correspondiente al tipo, abriendo un **caso de convivencia** con número consecutivo, responsable, plazos y lista de actuaciones esperadas.
4. Se ejecutan las **actuaciones del protocolo** (escuchar a las partes, garantizar atención en salud si aplica, medidas pedagógicas o restaurativas, citación a acudientes).
5. Para tipo II y III se **convoca el Comité Escolar de Convivencia**; el sistema genera la **acta** con asistentes, hechos, decisiones y compromisos.
6. En tipo III el **rector reporta a la autoridad competente** y el sistema deja constancia del reporte (entidad, fecha, radicado).
7. Se registran **acuerdos y compromisos** firmados por estudiante y acudiente; cada uno alimenta el [[../04-procesos-academicos/observador-del-estudiante|observador del estudiante]].
8. El caso entra en **seguimiento** hasta verificar el cumplimiento; al cerrarse queda con su resolución.

## Flujos alternativos

- **Reclasificación:** si nueva información cambia la gravedad, el coordinador reclasifica el tipo; el sistema ajusta el protocolo y registra el cambio con motivo y autor.
- **Reincidencia:** un seguimiento incumplido o un nuevo hecho reabre el caso o escala su tipo.
- **Atención en salud prioritaria:** ante daño al cuerpo, la remisión a EPS/urgencias es la primera actuación y bloquea el cierre hasta registrarse.
- **Caso de tipo III detectado por docente:** cualquier rol puede marcar "presunto delito"; el sistema escala de inmediato al rector y restringe la visibilidad del caso.

## Estados y transiciones

### Caso de convivencia

```
Reportado → Clasificado → En atención → En comité (tipo II/III)
                                      → Reportado a autoridad (tipo III)
En atención → En seguimiento → Cerrado
En seguimiento → Reabierto (reincidencia) → En atención
Cualquier estado → Reclasificado (con justificación)
```

## Configurabilidad por colegio

- **Manual de convivencia:** cada colegio carga y versiona su manual; las medidas pedagógicas sugeridas se toman de él.
- **Integrantes del comité:** se configuran por año lectivo respetando la composición mínima legal.
- **Plazos de cada protocolo:** se parametrizan dentro de los topes que la norma permite (no por debajo de lo exigido).
- **Catálogo de medidas restaurativas y pedagógicas:** base de plataforma más medidas propias del colegio.
- **Canales de notificación:** correo, portal y WhatsApp según lo habilitado por el colegio.
- **Visibilidad del caso:** por defecto interna (coordinación y rector); las partes ven solo lo que les corresponde.

## Integraciones con otros módulos

- **Observador del estudiante:** todo acuerdo, compromiso o sanción derivado de un caso se refleja como anotación en el [[../04-procesos-academicos/observador-del-estudiante|observador]], respetando su visibilidad (`RN-OB-081`).
- **Disciplina y observaciones:** comparte el catálogo de anotaciones y el flujo de confirmación con [[../04-procesos-academicos/disciplina-y-observaciones|disciplina y observaciones]].
- **Notificaciones:** las citaciones y comunicados a acudientes usan [[../05-comunicacion/notificaciones|notificaciones]] y [[../05-comunicacion/comunicacion-con-padres|comunicación con padres]].
- **Alertas tempranas:** el cruce de asistencia, notas y observador alimenta la prevención (ver `RN-VA-101`).
- **Log de auditoría:** clasificación, reclasificación, actas y reportes a autoridad quedan en [[../11-plataforma-y-operacion/log-de-auditoria|log de auditoría]].
- **Gestión documental:** actas, acuerdos firmados y soportes se almacenan en [[../11-plataforma-y-operacion/gestion-documental|gestión documental]] sujetos a cuota.
- **Reportes oficiales:** los datos de convivencia alimentan los reportes al MEN y al SIUCE (ver reportes oficiales).

## Datos involucrados

- Caso de convivencia (consecutivo, tipo, estado, responsable, fechas).
- Estudiantes involucrados (presuntos generadores y afectados) y su rol en el hecho.
- Actuaciones del protocolo con responsable, fecha y resultado.
- Actas del comité (asistentes, hechos, decisiones, compromisos, firmas).
- Acuerdos y compromisos firmados.
- Constancia de reporte a autoridad (entidad, fecha, radicado) en tipo III.

## Salidas / artefactos generados

- Caso de convivencia con su historial completo.
- Actas del Comité Escolar de Convivencia en PDF.
- Acuerdos y compromisos firmados.
- Anotaciones en el observador del estudiante.
- Reporte consolidado de convivencia institucional para auditoría y SIUCE.

## Reglas de negocio

- **RN-CVE-001 — Comité obligatorio por colegio:** cada tenant debe tener un Comité Escolar de Convivencia con la composición mínima legal registrada por año lectivo; el sistema impide cerrar la configuración del año sin él.
- **RN-CVE-002 — Clasificación obligatoria y auditada:** todo caso debe clasificarse en tipo I, II o III antes de avanzar; la clasificación y cualquier reclasificación quedan en el log con autor, fecha y justificación.
- **RN-CVE-003 — Protocolo según el tipo:** el sistema instancia las actuaciones, plazos y responsables del protocolo correspondiente al tipo y no permite saltarse actuaciones obligatorias antes de cerrar el caso.
- **RN-CVE-004 — Tipo III escala al rector y exige reporte:** un caso clasificado como tipo III escala automáticamente al rector y no puede cerrarse sin registrar la constancia de reporte a la autoridad competente (entidad, fecha, radicado).
- **RN-CVE-005 — Atención en salud prioritaria:** cuando hay daño al cuerpo o a la salud, la remisión a EPS/urgencias es actuación obligatoria y bloquea el cierre del caso hasta registrarse.
- **RN-CVE-006 — Acta firmada para tipo II y III:** las decisiones del comité requieren acta con asistentes, hechos, decisiones y firma del rector; el acta es inmutable una vez firmada.
- **RN-CVE-007 — Articulación con el observador:** todo acuerdo, compromiso o medida derivado del caso genera la anotación correspondiente en el observador del estudiante, respetando la visibilidad configurada por anotación.
- **RN-CVE-008 — Visibilidad restringida del caso:** el detalle del caso es de visibilidad interna por defecto (coordinación y rector); estudiantes y acudientes solo ven las actuaciones y acuerdos que les corresponden.
- **RN-CVE-009 — Inmutabilidad post-cierre:** los casos, actas y reportes de un año lectivo cerrado son inmutables y solo consultables; cualquier corrección posterior exige reapertura autorizada y queda auditada.
- **RN-CVE-010 — Plazos no inferiores a la ley:** los plazos configurables por colegio no pueden fijarse por debajo de los mínimos exigidos por la norma; el sistema valida el tope al guardar la parametrización.

## Notas y pendientes

- **[Decisión tomada]** La tipificación I/II/III es **fija por ley** y no editable por el colegio; lo configurable son los plazos (dentro de topes legales), el catálogo de medidas y los canales de notificación. Regla: **RN-CVE-003**.
- **[Decisión tomada]** El reporte al **SIUCE / Sistema de Información Unificado de Convivencia Escolar** se modela como exportación dentro de los reportes oficiales MEN, no como integración en tiempo real en el MVP.
- **[Pendiente — producto]** Definir el modelo de **firma de actas y acuerdos**: si se usa firma electrónica nativa (`RN-VA-004`) o carga de acta escaneada en el MVP.
- **[Pendiente — producto]** Definir el grado de **anonimización del reportante** en casos sensibles (tipo II/III) y cómo se concilia con la trazabilidad de auditoría.
- **[Pendiente — producto]** Validar con asesoría jurídica los **mínimos de plazo por protocolo** que el sistema debe imponer como tope inferior en `RN-CVE-010`.

## Documentos relacionados

- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]]
- [[../04-procesos-academicos/disciplina-y-observaciones|Disciplina y observaciones]]
- [[../02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia|Rol: Coordinador de Convivencia]]
- [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rol: Rector / Administrador del Colegio]]
- [[../05-comunicacion/notificaciones|Notificaciones]]
- [[../05-comunicacion/comunicacion-con-padres|Comunicación con padres]]
- [[../11-plataforma-y-operacion/log-de-auditoria|Log de auditoría]]
- [[../11-plataforma-y-operacion/gestion-documental|Gestión documental]]
- [[../04-procesos-academicos/asistencia|Asistencia]]
