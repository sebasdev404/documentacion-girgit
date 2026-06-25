---
titulo: Bienestar y orientación escolar
modulo: bienestar-y-servicios
tipo: proceso
estado: borrador
tags: [bienestar, orientacion, psicologia, confidencialidad, proceso]
---

# Bienestar y orientación escolar

## Descripción

Proceso por el cual el área de orientación escolar (psicología / bienestar) realiza seguimiento psicosocial confidencial de los estudiantes: agenda citas, registra atenciones, gestiona remisiones internas y externas, construye planes de acompañamiento y atiende alertas de riesgo. La información de orientación es **sensible y de visibilidad restringida**: no se publica en el boletín ni es visible para el cuerpo docente general.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo\|Personal de apoyo (Orientador / Psicólogo)]] | Crea y gestiona el expediente de bienestar, agenda citas, registra atenciones, remisiones y planes de acompañamiento. |
| [[../02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Recibe remisiones internas, da contexto de convivencia y autoriza acciones de acompañamiento. |
| [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico\|Coordinador Académico]] | Recibe remisiones por desempeño y coordina apoyos académicos del plan. |
| [[../02-usuarios-roles-y-permisos/roles/07-director-de-grupo\|Director de Grupo]] | Origina remisiones internas y hace seguimiento operativo del acompañamiento en aula. |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Rector]] | Visibilidad consolidada de casos críticos; aprueba protocolos y configuración del módulo. |
| [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | Solicita o confirma citas, recibe el plan de acompañamiento en su parte visible y otorga consentimiento para remisiones externas. |

## Objetivo del proceso

Brindar acompañamiento psicosocial trazable y confidencial, articulando aula, convivencia, salud y familia, sin exponer información sensible del estudiante en canales no autorizados.

## Tipos de atención

| Tipo | Descripción | Origen típico |
| --- | --- | --- |
| Cita individual | Sesión de orientación con el estudiante. | Solicitud propia, remisión interna o seguimiento. |
| Cita con acudiente | Atención al acudiente o a la familia. | Plan de acompañamiento o citación. |
| Atención de crisis | Intervención no agendada por situación urgente. | Alerta de riesgo o reporte del docente. |
| Seguimiento | Registro de avance de un caso ya abierto. | Plan de acompañamiento activo. |
| Remisión | Derivación a otra instancia interna o a un servicio externo. | Evaluación del orientador. |

## Flujo principal

1. Un caso se abre por uno de tres disparadores: solicitud del estudiante/acudiente, remisión interna (director de grupo, coordinador o docente) o alerta de riesgo del sistema (`RN-VA-101`).
2. El orientador crea o ubica el **expediente de bienestar** del estudiante (uno por estudiante, transversal al año).
3. El orientador **agenda una cita** con el estudiante o con el acudiente, seleccionando fecha, hora y modalidad (presencial / virtual).
4. El sistema notifica la cita al destinatario por los canales habilitados, sin revelar el motivo clínico en el cuerpo de la notificación.
5. Realizada la atención, el orientador **registra la nota de seguimiento** con su nivel de confidencialidad.
6. Si procede, define o actualiza un **plan de acompañamiento** con objetivos, responsables y fechas de revisión.
7. Si el caso excede el alcance escolar, genera una **remisión externa** que requiere consentimiento del acudiente.
8. El caso permanece **abierto** hasta que el orientador lo cierra con un resumen; el historial queda preservado.

## Agendamiento de citas

1. La cita puede originarse desde el portal del estudiante/acudiente (solicitud) o directamente desde el orientador (citación).
2. El orientador confirma, reprograma o rechaza la solicitud con observación.
3. La agenda de orientación reutiliza el modelo de espacios físicos cuando la cita ocupa un consultorio o sala (ver [[../04-procesos-academicos/espacios-fisicos\|Espacios físicos]]).
4. La notificación al estudiante/acudiente informa fecha, hora y lugar, **nunca el contenido sensible** del caso.

## Remisiones

- **Internas:** derivación a coordinación de convivencia, coordinación académica o salud/enfermería. Quedan dentro del tenant y respetan la visibilidad interna.
- **Externas:** derivación a EPS, profesional particular o entidad de protección. Requieren **consentimiento explícito del acudiente** registrado en el expediente antes de compartir cualquier dato.

## Planes de acompañamiento

- Un plan agrupa objetivos, acciones, responsables y fechas de revisión.
- Tiene una **parte visible** para el estudiante/acudiente (compromisos y citas) y una **parte interna** (hipótesis, notas clínicas) que no se comparte.
- Se revisa periódicamente; cada revisión genera una nota de seguimiento fechada.

## Alertas de riesgo

- El sistema de alertas tempranas (`RN-VA-101`) cruza asistencia, notas, observador y cartera, y emite un semáforo con recomendación.
- Cuando una alerta alcanza el umbral configurado, se enruta al área de orientación para abrir o actualizar un caso.
- La decisión de intervención es **siempre humana**; la alerta es insumo, no acción automática sobre el estudiante.

## Confidencialidad y visibilidad

- Las notas de orientación usan los tres niveles de visibilidad del observador (`RN-OB-081`): **pública**, **docentes** e **interna**. Por defecto, bienestar registra en nivel **interna**.
- La información sensible (diagnósticos, hipótesis clínicas, situaciones familiares) **no alimenta el boletín** ni los reportes académicos (ver [[../04-procesos-academicos/boletines-y-reportes-academicos\|Boletines y reportes académicos]]).
- El cuerpo docente general **no** ve el expediente de bienestar; solo accede a la parte del plan de acompañamiento que el orientador marque como visible para aula.

## Estados y transiciones

### Caso de bienestar

```
Abierto → En seguimiento → Cerrado
        → Remitido (interno / externo) → En seguimiento
```

### Cita

```
Solicitada → Confirmada → Realizada
           → Reprogramada → Confirmada
           → Rechazada / Cancelada
```

## Configurabilidad por colegio

- Catálogo de **tipos de atención** y de **motivos de remisión** base + personalización por colegio.
- Nivel de visibilidad **por defecto** de las notas de bienestar (interna recomendada).
- Si el portal del acudiente permite **autosolicitar** citas o solo recibir citaciones.
- Plantillas de **consentimiento informado** para remisiones externas según política del colegio.
- Qué roles, además de orientación, ven el resumen consolidado de casos críticos (rector siempre; coordinaciones configurable).

## Integraciones con otros módulos

- **Observador del estudiante:** las notas internas se rigen por la visibilidad de `RN-OB-081` (ver [[../04-procesos-academicos/observador-del-estudiante\|Observador del estudiante]]).
- **Salud y enfermería:** remisiones internas y casos que mezclan salud física y emocional (ver [[salud-y-enfermeria\|Salud y enfermería]]).
- **Valor agregado / IA:** consume las alertas tempranas (`RN-VA-101`).
- **Comunicación:** las citas se notifican por los canales habilitados sin exponer el motivo (ver [[../05-comunicacion/notificaciones\|Notificaciones]]).
- **Convivencia:** los casos disciplinarios pueden originar remisiones a orientación (ver [[../13-cumplimiento-colombia/convivencia-ley-1620\|Convivencia escolar (Ley 1620)]]).

## Reglas de negocio

- **RN-BW-001 — Expediente de bienestar único por estudiante:** cada estudiante tiene un único expediente de bienestar, transversal a los años lectivos, que acumula citas, atenciones, remisiones y planes.
- **RN-BW-002 — Acceso restringido al área de orientación:** solo el personal de apoyo con rol de orientación accede al expediente completo; el cuerpo docente general no lo ve.
- **RN-BW-003 — Información sensible fuera del boletín:** las notas, diagnósticos e hipótesis de orientación nunca se publican en el boletín ni en reportes académicos.
- **RN-BW-004 — Visibilidad interna por defecto:** las notas de bienestar se registran por defecto en nivel `interna` según `RN-OB-081`; cambiarlas a un nivel más abierto exige acción explícita del orientador.
- **RN-BW-005 — Consentimiento obligatorio para remisión externa:** ninguna remisión externa comparte datos del estudiante sin el consentimiento del acudiente registrado previamente en el expediente.
- **RN-BW-006 — Notificación de cita sin motivo sensible:** la notificación de una cita informa fecha, hora y lugar, pero nunca el motivo clínico ni el contenido del caso.
- **RN-BW-007 — Alerta de riesgo no decide por sí sola:** las alertas tempranas (`RN-VA-101`) abren o actualizan un caso, pero toda intervención sobre el estudiante requiere decisión humana del orientador.
- **RN-BW-008 — Plan con doble capa de visibilidad:** todo plan de acompañamiento separa una parte visible para el estudiante/acudiente de una parte interna que no se comparte.
- **RN-BW-009 — Cierre preserva la historia:** cerrar un caso exige un resumen y conserva todas las notas y remisiones; no se permite borrado físico del historial.
- **RN-BW-010 — Auditoría de acceso a datos sensibles:** toda consulta y edición del expediente de bienestar queda registrada en el log con usuario, fecha, hora e IP.

## Notas y pendientes

- **[Decisión tomada]** El expediente de bienestar es **transversal al año lectivo** (a diferencia del observador, que es por año), porque el acompañamiento psicosocial puede extenderse varios periodos. Regla: **RN-BW-001**.
- **[Decisión tomada]** El nivel de visibilidad por defecto de las notas de bienestar es **interna** (`RN-OB-081`), configurable por colegio. Regla: **RN-BW-004**.
- **[Pendiente — producto]** Definir si el menor de edad puede solicitar una cita de orientación **sin notificar al acudiente** y bajo qué edad/condiciones, alineado con la normativa colombiana de protección al menor. Tiene implicaciones con Habeas Data.
- **[Pendiente — producto]** Validar el formato de **consentimiento informado** para remisiones externas con firma electrónica (`RN-VA-004`) durante el piloto.
- **[Pendiente — producto]** Acordar la **retención** del expediente de bienestar tras el egreso del estudiante (alinear con política de Habeas Data, Ley 1581).

## Documentos relacionados

- [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo|Rol: Personal de apoyo]]
- [[../02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia|Rol: Coordinador de Convivencia]]
- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]]
- [[../04-procesos-academicos/disciplina-y-observaciones|Disciplina y observaciones]]
- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]]
- [[../04-procesos-academicos/boletines-y-reportes-academicos|Boletines y reportes académicos]]
- [[salud-y-enfermeria|Salud y enfermería]]
- [[../13-cumplimiento-colombia/convivencia-ley-1620|Convivencia escolar (Ley 1620)]]
- [[../13-cumplimiento-colombia/habeas-data-y-consentimientos|Habeas Data y consentimientos]]
- [[../05-comunicacion/notificaciones|Notificaciones]]
