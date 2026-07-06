---
titulo: Encuestas institucionales
modulo: 05-comunicacion
tipo: proceso
estado: borrador
tags: [encuestas, comunicacion, clima-escolar, autoevaluacion, proceso]
---

# Encuestas institucionales

## Descripción

Las **encuestas** permiten al colegio recoger percepción de su comunidad de forma estructurada: clima escolar, satisfacción de acudientes, autoevaluación institucional y evaluación docente por estudiantes. Como la [[agenda-y-publicaciones|agenda]] (`RN-AG-001`), son **unidireccionales**: el colegio publica un cuestionario y recibe respuestas, pero la encuesta **no abre chat ni hilo** de conversación entre quien responde y la institución.

## Objetivo del proceso

Que un rol con permiso pueda crear una encuesta dirigida a una audiencia controlada, con anonimato configurable y ventana de respuesta acotada, y obtener un consolidado de resultados confiable para tomar decisiones (planes de mejora, autoevaluación institucional anual, retroalimentación docente).

## Tipos de encuesta

| Tipo | Audiencia típica | Anonimato sugerido | Uso |
| --- | --- | --- | --- |
| Clima escolar | Estudiantes, docentes, acudientes | Anónima | Percepción de convivencia y ambiente. |
| Satisfacción de acudientes | Acudientes | Anónima o identificada | Calidad del servicio, comunicación, atención. |
| Autoevaluación institucional | Docentes, directivos, administrativos | Identificada (requisito de soporte) | Insumo de la autoevaluación anual del colegio. |
| Evaluación docente por estudiantes | Estudiantes de los grupos del docente | **Anónima obligatoria** | Retroalimentación al docente; sensible. |

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[roles/01-rector-administrador-colegio\|Rector]] | Aprueba o solicita encuestas institucionales (autoevaluación, clima) y consulta consolidados. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Crea encuestas académicas y de evaluación docente; consulta resultados de sus áreas. |
| [[roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Crea y analiza encuestas de clima escolar y convivencia. |
| [[roles/05-secretaria-academica\|Secretaría Académica]] | Apoya la configuración de audiencia y la difusión de la encuesta. |
| [[roles/06-docente\|Docente]] | Es **sujeto evaluado** en la evaluación docente; responde encuestas dirigidas a docentes. |
| [[roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | Responde las encuestas de la audiencia a la que pertenece; nunca ve respuestas de terceros. |

## Precondiciones

- El colegio (tenant) tiene habilitado el módulo de encuestas en su plan.
- El rol que crea la encuesta tiene permiso `encuestas.crear`.
- Existe el año/periodo lectivo activo para asociar la encuesta a un contexto.

## Disparadores (cuándo arranca)

- Cierre de periodo o de año (autoevaluación, evaluación docente).
- Necesidad institucional puntual (clima tras un incidente, satisfacción tras un evento).
- Requisito de la autoevaluación institucional anual.

## Flujo principal

1. Un rol con permiso crea la encuesta y selecciona su **tipo** (define plantilla y reglas por defecto, ej. anonimato obligatorio en evaluación docente).
2. Construye el cuestionario con preguntas (escala Likert, opción única, opción múltiple, abierta). Marca cuáles son obligatorias.
3. Define la **audiencia controlada**: por rol, por grado/grupo, por sede, por lista específica o por docente evaluado.
4. Configura **anonimato** (anónima / identificada), **ventana de respuesta** (fecha-hora de apertura y cierre) y si permite una sola respuesta por persona.
5. Publica la encuesta. El sistema notifica a la audiencia por los canales del colegio (ver [[notificaciones|notificaciones]]).
6. Cada destinatario responde dentro de la ventana; el sistema registra que respondió (control de cobertura) **sin asociar contenido a la persona si es anónima**.
7. Al cerrarse la ventana, el sistema **consolida** los resultados y los pone disponibles a los roles autorizados.

## Flujos alternativos

- **Borrador y revisión:** la encuesta puede guardarse en `Borrador` y enviarse a revisión antes de publicar.
- **Encuesta sin respuestas suficientes:** si una encuesta anónima cierra con menos respuestas que el mínimo configurado, el consolidado se bloquea para proteger el anonimato.
- **Reapertura:** un rol con permiso puede extender la ventana antes del cierre; no se permite reabrir una encuesta ya cerrada y consolidada.

## Estados y transiciones

### Encuesta

```
Borrador → En revisión → Publicada (ventana abierta) → Cerrada → Consolidada
   ↑___________________|
Publicada → Cancelada (solo si no hay respuestas o por decisión justificada con log)
```

### Respuesta de un destinatario

```
Pendiente → Respondida (dentro de ventana)
Pendiente → No respondida (al cerrar la ventana)
```

## Configurabilidad por colegio

- **Anonimato por tipo:** cada colegio define el anonimato por defecto de cada tipo, salvo evaluación docente que es **siempre anónima** y no se puede cambiar.
- **Mínimo de respuestas (n) para mostrar consolidado** de encuestas anónimas (umbral anti-reidentificación; por defecto 5).
- **Plantillas propias:** el colegio puede guardar plantillas de cuestionario reutilizables por año.
- **Canales de difusión:** push, correo, portal o WhatsApp, según lo habilitado en el tenant.
- **Escalas:** el colegio define la escala Likert institucional (ej. 1–5 o 1–4) y sus etiquetas.

## Integraciones con otros módulos

- [[notificaciones|Notificaciones]]: difusión de la publicación y recordatorios de cierre.
- [[agenda-y-publicaciones|Agenda]]: misma naturaleza unidireccional; la agenda puede anunciar que hay una encuesta abierta.
- [[roles/06-docente\|Docente]] y [[../02-usuarios-roles-y-permisos/matriz-de-permisos\|Matriz de permisos]]: permisos de creación y de lectura de consolidados.
- [[../09-reportes-y-analitica/indicadores-kpi\|Indicadores / KPI]]: los resultados alimentan tableros de clima y satisfacción.
- [[disciplina-y-observaciones|Observador del estudiante]]: una encuesta **no** escribe en el observador; los hallazgos se gestionan por fuera.

## Datos involucrados

- Encuesta: tipo, título, año/periodo, anonimato, ventana (apertura/cierre), mínimo de respuestas.
- Preguntas y opciones (tipo de pregunta, obligatoriedad, escala).
- Audiencia objetivo (resuelta a un conjunto de destinatarios del tenant).
- Marca de "respondió / no respondió" por destinatario (para cobertura, separada del contenido si es anónima).
- Respuestas y consolidado agregado por pregunta.

## Reglas de negocio

- **RN-EC-001 — Unidireccional como la agenda:** la encuesta solo recibe respuestas al cuestionario; no abre chat ni hilo. Para diálogo se usa la mensajería de flujos o las citaciones (alineado con `RN-AG-001`).
- **RN-EC-002 — Audiencia controlada y cerrada:** una encuesta solo es visible y respondible por los destinatarios de la audiencia definida (rol, grado, grupo, sede o lista); nadie fuera de ella puede verla ni responderla.
- **RN-EC-003 — Anonimato irreversible:** si una encuesta se publica como anónima, el sistema no almacena el vínculo respuesta–persona y ese vínculo no puede reconstruirse después por ningún rol, ni el Superadministrador.
- **RN-EC-004 — Evaluación docente siempre anónima:** las encuestas de tipo evaluación docente por estudiantes son anónimas de forma obligatoria y la configuración no permite hacerlas identificadas.
- **RN-EC-005 — Ventana de respuesta obligatoria:** toda encuesta tiene fecha-hora de apertura y cierre; fuera de esa ventana no se aceptan respuestas. La ventana puede extenderse antes de cerrar, nunca después de consolidar.
- **RN-EC-006 — Umbral mínimo para consolidar anónimas:** el consolidado de una encuesta anónima solo se muestra si las respuestas alcanzan el mínimo configurado por el colegio (por defecto 5), para evitar reidentificación.
- **RN-EC-007 — Una respuesta por destinatario:** por defecto cada destinatario responde una sola vez; permitir múltiples envíos es configurable y solo aplica a encuestas no anónimas.
- **RN-EC-008 — Separación cobertura/contenido:** el control de quién respondió (cobertura) se almacena separado del contenido de las respuestas cuando la encuesta es anónima, de modo que saber que alguien respondió no revele qué respondió.
- **RN-EC-009 — Aislamiento por tenant:** las encuestas, audiencias y resultados pertenecen al colegio que las creó; no se comparten ni agregan entre tenants.
- **RN-EC-010 — Auditoría de creación y cambios:** la creación, edición de audiencia/ventana, publicación, cierre y cancelación quedan en el log con autor, fecha y valor anterior; el contenido de respuestas anónimas no se audita por persona.

## Notas y pendientes

- **[Decisión tomada]** El anonimato es **irreversible** y la evaluación docente es siempre anónima (`RN-EC-003`, `RN-EC-004`). Esto se mantiene incluso para el Superadministrador.
- **[Decisión tomada]** El umbral mínimo de respuestas para mostrar consolidados anónimos es **configurable por colegio**, con valor por defecto 5 (`RN-EC-006`).
- **[Pendiente — producto]** Definir si la autoevaluación institucional debe exportar en el formato que pida el MEN / secretaría de educación cuando exista el módulo de [[../13-cumplimiento-colombia/reportes-oficiales-men|reportes oficiales]].
- **[Pendiente — UX]** Validar durante el piloto el flujo de respuesta en móvil para acudientes con varios hijos (una encuesta puede aplicar por hijo o una sola vez por acudiente).

## Documentos relacionados

- [[agenda-y-publicaciones|Agenda y publicaciones]]
- [[notificaciones|Notificaciones]]
- [[circulares-y-comunicados|Circulares y comunicados]]
- [[roles/06-docente|Rol Docente]]
- [[roles/08-estudiante-y-acudiente|Estudiante y Acudiente]]
- [[../02-usuarios-roles-y-permisos/matriz-de-permisos|Matriz de permisos]]
- [[../09-reportes-y-analitica/indicadores-kpi|Indicadores y KPI]]
- [[disciplina-y-observaciones|Observador del estudiante]]
