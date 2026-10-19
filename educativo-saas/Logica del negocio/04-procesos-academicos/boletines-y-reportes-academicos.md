---
titulo: Boletines y reportes académicos
modulo: procesos-academicos
tipo: proceso
estado: propuesta vigente
tags: [boletines, reportes, proceso]
---

# Boletines y reportes académicos

## Descripción

Proceso individual de preparación, revisión, aprobación y emisión persistente del PDF académico de un estudiante. Conviven una vista de notas preliminar y un flujo independiente de emisión oficial individual; imprimir la vista preliminar no constituye emisión. El plan de cierre del ciclo académico de octubre de 2026 prevalece sobre los apartados históricos incompatibles de este documento.

**Avance local del 14 de octubre de 2026:** ya existen diseños base de período/final y un editor de bloques con vista previa viva ficticia, guardado de borradores y publicación de revisiones. El permiso de gestión y la capacidad `boletines_personalizables` se verifican en servidor. La preview todavía no contiene datos académicos reales ni sustituye la preparación, aprobación y emisión individual del PDF. Contrato implementado: `colegio-saas-backend/docs/BOLETIN_PLANTILLAS.md`.

**Segundo incremento local del 14 de octubre:** preparación individual contra notas completas y observación aprobada, aprobación con PDF privado y SHA-256, y publicación separada para el estudiante. Se aplicaron migraciones a central y cinco colegios locales sin emitir documentos reales. La vista previa de notas permanece preliminar. Contrato, evidencia y límites: `colegio-saas-backend/docs/BOLETIN_EMISION.md`. Siguen pendientes firma/confirmación digital, paz y salvo, asistencia por materia, algunos datos estudiantiles y paridad visual completa del editor con PDF; no se declara terminado el ciclo académico.

## Tipos de boletín

| Tipo | Descripción |
| --- | --- |
| Boletín parcial | Generado al cierre de cada periodo académico durante el año lectivo. |
| Boletín final | Generado al cierre del año lectivo, con la nota definitiva de cada materia y el resultado de promoción. |
| Consolidado | Documento que reúne todos los periodos en una vista única. |

## Plantillas

- Todo colegio con el módulo académico puede emitir mediante una **plantilla base de la plataforma** con nombre, logo y datos reales del colegio, sin marca del SaaS en el documento.
- La capacidad efectiva `boletines_personalizables` permite al Rector autorizado crear, duplicar, ordenar y publicar diseños en un editor visual de bloques controlados. Está incluida por defecto en Estándar y Premium; un plan personalizado depende de sus capacidades efectivas. El backend comprueba tanto capacidad como permiso.
- La asistencia profesional de diseño puede ofrecerse adicionalmente, pero no reemplaza ni bloquea el editor autoservicio de un plan autorizado.

### Versionado de plantillas

Una revisión publicada de plantilla es inmutable. Cada PDF emitido conserva esa revisión, configuración, resultados, indicadores, observación exacta, actor, archivo y huella. Cambiar de diseño o plan no altera lo ya emitido.

## Contenido del boletín

Por defecto el boletín incluye:

- Datos del estudiante (nombre, documento, grado, grupo, foto).
- Periodo académico (o consolidado del año si es final).
- Cada materia con su nota final.
- Indicadores descriptivos del aprendizaje esperado por asignatura y período, sin valoración individual propia.
- Observación académica general guardada para ese estudiante y período por un actor autorizado. No es una anotación disciplinaria ni la observación opcional de una nota.
- Registro de inasistencias por materia y total del periodo.
- Nota de comportamiento si el colegio la maneja.
- Logo y datos institucionales del colegio.

El colegio configura qué secciones aparecen y cuáles se ocultan.

### Pesos visibles en el boletín — decisión de producto del 5 de octubre de 2026

- Junto al encabezado de cada período se mostrará su peso anual configurado, por ejemplo, **Primer período · 25 %**. Ese peso se aplica al resultado de cada asignatura y, cuando corresponda, al área; no es un porcentaje propio de la materia.
- Si el SIEE calcula un área por **promedio ponderado**, se podrá mostrar además el peso de cada asignatura dentro de esa área, claramente separado del peso del período.
- Si el SIEE calcula un área por **promedio simple**, no se mostrará un porcentaje por asignatura: se suman los resultados de sus asignaturas y se dividen entre la cantidad correspondiente.
- Esta visualización no cambia la fórmula vigente: los cálculos conservan su precisión interna y redondean solo el resultado publicado. Se descartó añadir un desglose técnico de los valores internos al boletín.
- **Estado:** el flujo de emisión individual y PDF ya existe en desarrollo local; la paridad visual de todos los pesos y secciones entre vista previa y PDF sigue pendiente de revisión.

## Generación del boletín

1. Seleccionar individualmente estudiante y período cerrado, o el contexto final anual aprobado.
2. Guardar la observación académica general de ese estudiante y período. Si falta, bloquear la preparación; no inventar texto para continuar.
3. Preparar con datos académicos completos y plantilla publicada, revisar el borrador y sus advertencias.
4. Aprobar con permiso, generar el PDF desde datos congelados y guardar archivo y huella.
5. Publicar la emisión aprobada para consulta del estudiante autorizado. Una corrección genera nueva versión y conserva el PDF anterior.

El Rector o un rol autorizado configura si el boletín final anual exige una **observación final adicional**; si no se exige, no se bloquea por ella. El período sumatorio, si se activa, es un resultado calculado P(N+1), no otro período real de captura.

## Aprobación / firma del boletín

- Diseño de plantilla, captura académica, revisión, aprobación, emisión y publicación tienen permisos y estados separados.
- El Rector debe poder revisar y aprobar una emisión individual. Dirección de grupo y coordinación requieren vínculo y alcance comprobados por el servidor antes de recibir acceso.
- El documento publicado queda accesible únicamente a perfiles autorizados y al estudiante titular; no hay portal de acudiente implementado.

La aprobación confirma el documento congelado, no modifica las calificaciones. La decisión posterior del 14 de octubre de 2026 sustituye la aprobación/generación por lote como flujo principal: **la emisión solicitada es estudiante por estudiante**. Una operación masiva futura requerirá nueva decisión de producto y controles equivalentes. Ya existe aprobación de la emisión y PDF histórico privado; no existe firma digital certificada.

## Confirmación digital del estudiante

Si el colegio lo exige, el estudiante debe **confirmar el boletín digitalmente** desde su portal antes de que quede como entregado. El sistema registra la fecha, hora e IP de esa confirmación.

## Bloqueo por paz y salvo

El sistema puede bloquear la disponibilidad del boletín si el estudiante tiene un [[../06-monetizacion-y-pagos/paz-y-salvo|paz y salvo]] pendiente, según la configuración del colegio.

## Distribución a padres y estudiantes

- El boletín publicado está disponible en el portal del estudiante autorizado. No se habilitan cuentas ni correo a acudientes por inferencia documental.
- Una notificación futura requiere política de destinatarios y cola verificadas; no se envía automáticamente durante el desarrollo.
- El bloqueo por paz y salvo solo puede habilitarse con integración real de cartera; no se declara a alguien «al día» por ausencia de datos.

## Otros reportes académicos

Más allá del boletín por estudiante, el sistema genera:

- **Consolidado de notas por grupo** — PDF con todas las notas de todas las materias del grupo en un periodo. Para uso del director de grupo y coordinación.
- **Certificado de notas final del año** — documento oficial al cierre del año.
- **Constancia de estudio** — documento que acredita la matrícula activa del estudiante.

Ver [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]] y [[../11-plataforma-y-operacion/gestion-documental|Gestión documental]].

## Reglas de negocio

- **RN-BR-001 — Generación tras cierre del periodo:** los boletines parciales solo pueden generarse después del cierre del periodo correspondiente.
- **RN-BR-002 — Versionado fiel:** la regeneración de un boletín histórico usa la plantilla y configuración vigente al momento de su emisión original, no la actual.
- **RN-BR-003 — Bloqueo por paz y salvo configurable:** el bloqueo de boletín por paz y salvo es configurable por el colegio. Por defecto los boletines están disponibles.
- **RN-BR-004 — Confirmación digital opcional:** la confirmación digital del boletín por parte del estudiante es opcional, configurable por el colegio.
- **RN-BR-005 — PDF persistente:** los PDFs generados se almacenan en el tenant. La integración con cuota y una regeneración fiel tras pérdida del archivo siguen pendientes; hasta entonces el sistema alerta y no reconstruye el histórico con recursos actuales.
- **RN-BR-006 — Editor por capacidad y permiso:** un plan con `boletines_personalizables` y permiso efectivo habilita editor autoservicio; el plan básico conserva emisión con plantilla base.

## Notas y pendientes

- **[Decisión tomada]** Rector o rol autorizado configura si se exige una observación final anual distinta de las de cada período.
- **[Pendiente — funcionalidad futura]** Firma digital sobre certificados oficiales y sellos del rector. No bloquea el lanzamiento; el certificado lleva firma escaneada del rector cargada por el colegio.
