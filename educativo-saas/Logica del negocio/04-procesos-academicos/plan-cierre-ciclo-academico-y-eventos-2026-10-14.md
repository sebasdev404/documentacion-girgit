---
titulo: Siguiente etapa del ciclo académico y eventos
modulo: procesos-academicos
tipo: plan
estado: propuesta
tags: [calendario, eventos, aula, indicadores, observaciones, boletines]
---

# Siguiente etapa: calendario, eventos y cierre del ciclo académico

**Decisiones de producto registradas:** 14 de octubre de 2026.
**Estado:** plan histórico con eventos/calendario y varios incrementos académicos implementados localmente. No acredita despliegue de producción. La promoción sigue el cálculo reglado, sin consejo decisorio ni votación (decisión del 15 de octubre de 2026); la dirección de grupo ya tiene un primer vínculo local. Evidencia: `colegio-saas-backend/docs/CICLO_ACADEMICO_AVANCE.md` en el workspace.
**Documento base:** `PLAN_COMPLETAR_CICLO_ACADEMICO.md` del espacio de trabajo. Las decisiones expresas de este documento prevalecen sobre propuestas anteriores incompatibles, hasta reconciliar la documentación de Girgit y los contratos del producto.

**Corrección posterior del 19 de octubre de 2026:** las propuestas de este plan para valorar indicadores por estudiante, configurarles escala o filtrar «no alcanzados» quedaron descartadas. Los indicadores son exclusivamente textos descriptivos; la evaluación individual corresponde a notas SIEE y observaciones. Prevalece `logros-e-indicadores.md` en esos puntos.

**Corrección posterior del 21 de octubre de 2026:** tampoco se distingue en la interfaz entre indicador «institucional», «variante» o «propio». El rector configura por año el alcance por grado o por grupo; los docentes solo gestionan materias realmente asignadas. Los cambios entre alcances conservan datos y exigen confirmación. Prevalece `logros-e-indicadores.md` sobre las propuestas históricas de la sección de indicadores de este plan.

## 1. Alcance y límites

### Avance local: eventos/calendario

Se implementaron los apartados de tareas proyectadas del Aula, publicación de eventos y correo optativo solo a estudiantes, con outbox, lotes y reintentos. Migración local aplicada con respaldos; pruebas incluyen 1.000 destinatarios sintéticos y revisión de interfaz ES/EN y móvil. Evidencia y operación: `colegio-saas-backend/docs/EVENTOS_Y_CALENDARIO.md` y `colegio-saas-frontend/docs/EVENTOS_Y_CALENDARIO.md` en el workspace.

Decisiones de esta entrega: casilla de correo apagada inicialmente; una publicación por evento; sin reenvío implícito al editar ni avisos de cancelación. Queda congelado el alcance al publicar. Faltan el despliegue supervisado de worker/scheduler, confirmación de buzones reales y manejo del proveedor; la cola no garantiza llegada a bandeja. Correos específicos de tareas y otros hitos del calendario no se incorporaron.

Completar la conexión entre Aula y calendario, la publicación y notificación de eventos, los indicadores/desempeños, las observaciones académicas y el diseño y emisión de boletines. Conservar los controles actuales de colegio, plan, permisos, año, grupo, período y auditoría. No activar pagos, crear cuentas de acudiente ni considerar el boletín preliminar como documento oficial.

Los eventos de agenda, las tareas del Aula y los boletines son entidades distintas. Una tarea no se crea en Eventos y no se copia a la tabla de eventos para poder verla en el calendario.

## 2. Calendario y tareas del Aula

- Eliminar «Tarea» del formulario, del catálogo y de la validación de categorías de Eventos. Antes de retirar el valor del backend, inventariar registros existentes con esa categoría y definir una migración/conversión no destructiva; no borrarlos ni transformarlos automáticamente en tareas del Aula.
- El calendario unifica en una respuesta o capa de lectura los eventos autorizados y las tareas **publicadas y visibles** del Aula. Cada entrada conserva su origen y un enlace con selector público opaco al recurso real. Un evento no adquiere permisos del Aula ni una tarea permisos de Eventos.
- La tarea con fecha límite aparece en la **fecha de entrega**, convertida a la zona horaria institucional. La tarea sin fecha límite aparece en su **fecha de publicación**, no en la creación de un borrador. Si se crea y publica en el mismo acto, ambas fechas coinciden. Guardar `publicado_en` cuando cambia de borrador a publicada; no reconstruirlo a partir de `updated_at` ni mover retrospectivamente la entrada por editarla.
- Borradores, recursos archivados o no visibles no aparecen a estudiantes. Una publicación programada solo aparece conforme a su estado y momento efectivo de publicación. Al editar una fecha límite, el calendario refleja la fecha vigente sin crear una segunda tarea.
- El estudiante ve exclusivamente tareas de sus grupos/matrículas aplicables; el docente, las de sus asignaciones y los gestores, las que permitan sus permisos. Comprobar cambios de grupo, año, período, zona horaria y acceso entre colegios.

**Criterio de aceptación:** una tarea creada ayer como borrador y publicada hoy sin límite se ve hoy; una tarea publicada hoy con límite el viernes se ve el viernes. Ninguna se puede crear desde Eventos y ninguna aparece dos veces.

## 3. Eventos y correo opcional por publicación

### Decisión funcional

- Eventos debe **ofrecer** envío por correo, pero el creador decide expresamente en cada publicación si activa «Enviar este evento por correo». Desactivado: se publica en el calendario sin envío masivo. No convertir «todos los eventos deben poder notificarse» en «todos los eventos envían correo obligatoriamente».
- Incorporar estado borrador/publicado y `publicado_en` para separar guardar de publicar. Capturar la decisión de correo al publicar; guardar un borrador no envía nada. Definir una acción posterior explícita para avisar cambios o cancelaciones, sin reenviar a todos por cualquier edición.
- El correo va **solo a estudiantes** con matrícula activa y correo válido en el alcance del evento: grupos seleccionados o toda la institución cuando el usuario autorizado publique un evento institucional. No enviar a docentes ni a cuentas de acudiente. Un estudiante en varios grupos recibe una sola copia por evento/publicación. Resolver los destinatarios con el colegio y el alcance del evento, no con los grupos que el navegador afirme tener.
- Docentes solo pueden publicar y notificar los grupos para los cuales el backend confirme asignación vigente y permisos; rector u otros roles con permiso institucional pueden elegir todo el colegio. La selección del formulario nunca amplía la autorización.
- Usar la configuración de correo institucional del colegio y una plantilla HTML/texto coherente con el SaaS: nombre del colegio, título, fecha/hora, descripción breve y enlace autorizado al evento. No incluir listas de destinatarios visibles ni datos escolares innecesarios.

### Entrega confiable y límite del proveedor

- Al publicar, registrar de forma transaccional la intención y el conjunto de destinatarios de esa publicación (outbox por destinatario, con clave única evento + versión/publicación + estudiante). Despachar después del commit. Reintentos de la petición, del worker o de la publicación no deben duplicar avisos ya marcados como enviados.
- Procesar por cola y lotes pequeños; **10 por lote es una propuesta inicial**, no una garantía de aceptación por Gmail. Hacer configurables el tamaño, la cadencia y la concurrencia según los límites vigentes del proveedor y verificarlo en el entorno de despliegue. No abrir mil conexiones simultáneas.
- Registrar pendientes, aceptados por SMTP, fallidos temporalmente y fallidos definitivamente; aplicar reintentos con espera progresiva, máximo de intentos, cola de fallidos, alerta al administrador y reenvío manual acotado. La pantalla debe mostrar progreso y fallos sin exponer direcciones completas a otros estudiantes.
- Una aceptación SMTP **no demuestra entrega a bandeja**. Rebotes, spam, cuotas del proveedor y errores de dirección requieren seguimiento operativo; el sistema no puede prometer que todos los mensajes llegarán. Si un correo no se acepta, no marcarlo como enviado ni perderlo silenciosamente.

**Pruebas mínimas:** destinatarios de un grupo, institucional con muchos estudiantes, exclusión de docentes/inactivos/otro colegio, deduplicación, permisos manipulando la API, caída y recuperación del worker, cuota/error transitorio SMTP, reintento idempotente y plantilla ES/EN. Probar con buzones controlados antes de la operación real; no disparar los avisos existentes de terceros durante el desarrollo.

## 4. Indicadores, desempeños y descripciones visibles por materia

La imagen de referencia muestra **objetivos de aprendizaje desplegados bajo cada asignatura** y una valoración visual. Esto no equivale a la descripción administrativa del área ni a un párrafo libre de la materia. En el código actual existe `areas.descripcion`, pero no un catálogo operativo de objetivos por materia/grupo/período que alimente ese bloque del boletín.

- Crear un catálogo ordenado de indicadores/desempeños por colegio, materia y grado/grupo según la configuración académica vigente. Admitir una **base institucional reutilizable entre años lectivos y en todos sus períodos**, además de variantes por año y por períodos seleccionados. Evitar duplicar el texto común; resolver la versión aplicable al año/período antes de valorar y conservarla en el histórico. Un cambio institucional nuevo no reescribe valoraciones ni boletines anteriores.
- Rector, coordinación académica y secretaría académica pueden gestionar conforme a permisos específicos de la matriz. El Rector configura si el docente asignado puede editar indicadores: cuando se habilita, la edición crea o cambia **solo la variante de su materia × grupo**, visible y editable en ese grupo; no cambia la base institucional ni los demás grupos. No basta tener el rol docente ni poder consultar otro grupo.
- Registrar la valoración del estudiante por indicador y período, separada del texto del indicador. El colegio define el modo de valoración: visual (por ejemplo, caritas), cualitativo o numérico, con etiquetas, escala y significado explícitos. Las caritas de la imagen son una referencia de presentación, no una escala obligatoria ni un cálculo implícito de la nota SIEE.
- El boletín agrupa por área/dimensión y materia, despliega los indicadores aplicables al período y muestra únicamente valoraciones registradas. No inventar «alcanzado» ni cero cuando falte evaluación. El sumatorio anual no crea indicadores nuevos automáticamente; su representación se define con la política del boletín final.
- Bloquear edición ordinaria al cerrar el período y conservar evidencia de quién creó, cambió y valoró cada indicador. Las correcciones históricas necesitan proceso auditado.

**Criterio de aceptación:** un indicador institucional común aparece en P1 y P2 y puede reutilizarse el año siguiente sin volver a digitarlo; otro definido solo para P2 no aparece en P1. Cambiar la base el año siguiente no altera el boletín anterior. Un docente de Segundo 01 no puede modificar indicadores de Primero 01 aunque cambie el selector en la petición.

## 5. Observación académica antes del boletín

- La observación del boletín es **por estudiante y período**; no es la observación opcional de una nota ni una anotación disciplinaria del observador. Debe tener autor, fecha, versión, estado y ámbito (general del período; observaciones por materia, si se habilitan, separadas).
- Antes de **preparar/generar el boletín individual**, comprobar que la observación general de ese estudiante y período esté guardada. Si falta, mostrar qué debe completarse y bloquear la generación; no insertar un texto ficticio o vacío para superar la validación. La persona autorizada puede redactarla y revisarla según la matriz de permisos y su vínculo con el grupo.
- Un cambio antes de aprobar requiere revisar de nuevo el borrador. La emisión aprobada conserva la observación exacta como parte de sus datos congelados; una corrección posterior produce nueva versión, no sustituye silenciosamente el PDF anterior.
- El Rector u otro rol con permiso configura si el boletín final anual requiere una observación final **distinta** de las observaciones de períodos reales. La emisión final la exige solo cuando esa opción esté activa. La vista preliminar puede señalar observaciones pendientes sin presentarse como documento emitido.

## 6. Plantillas y emisión de boletines

- **Plan básico/Esencial:** plantilla base provista por la plataforma, con logo, nombre e identidad del colegio y datos académicos reales; no rotular el documento con la marca del SaaS. El colegio puede generar/consultar boletines aunque no tenga la capacidad comercial de editar plantillas.
- **Planes con `boletines_personalizables` (hoy Estándar y Premium):** editor visual tipo Canva para crear, duplicar, organizar y publicar diseños propios con bloques controlados, vista previa, tipografía, colores, logo, tablas, indicadores, observaciones y secciones configurables. Comprobar **capacidad efectiva** y permiso en backend; el nombre comercial del plan por sí solo no autoriza.
- Disponer de diseño para boletín de cada período real y para **boletín final anual**. Puede reutilizarse la misma plantilla con datos/contexto distintos o publicar una variante final. Si el colegio activa el período sumatorio, representarlo como P(N+1) calculado, sin convertirlo en un período real con notas o fechas propias. Si no lo activa, el final anual sigue pudiendo mostrar la definitiva conforme al SIEE.
- La plantilla publicada es inmutable y versionada. Vista previa con datos sintéticos claramente marcados. La emisión conserva revisión de plantilla, configuración, resultados, indicadores, observación, actor y PDF/huella; cambiar de plan o diseño no altera boletines ya emitidos.
- El flujo solicitado ahora es **individual, estudiante por estudiante**: seleccionar estudiante/período, guardar observación, preparar y revisar, aprobar y generar/publicar el PDF. No ejecutar una generación o aprobación masiva por grupo como camino principal ni saltarse la observación. Una posible operación masiva futura requiere decisión nueva y controles equivalentes.
- Mantener separadas edición de plantilla, captura académica, revisión, aprobación y publicación. Conservar acceso histórico y reemplazos auditados; no llamar «emitido» a imprimir la vista preliminar del navegador.

**Criterios de aceptación:** Esencial emite usando plantilla institucional sin acceso al editor; un plan habilitado diseña y publica una revisión; P1/P2 y final muestran los datos que corresponden; un estudiante sin observación no se puede generar; una emisión anterior no cambia al editar plantilla, indicadores u observación.

## 7. Orden propuesto de trabajo y reconciliación documental

1. Fijar contratos y pruebas de publicación de tareas/eventos: `publicado_en`, alcance y lectura unificada del calendario. Migrar de forma segura la categoría antigua «tarea» en Eventos.
2. Implementar notificación de eventos con outbox, cola supervisada, plantilla y seguimiento operativo. Separar aceptación SMTP de entrega efectiva.
3. Implementar indicadores/desempeños, modos de valoración y permisos por asignación. Definir representación de los indicadores comunes y por período.
4. Implementar observaciones académicas individuales y controles previos al boletín.
5. Construir plantilla base y editor por capacidad/permiso; después, aprobación y emisión oficial individual con PDF histórico. Mantener dependencias del resto del ciclo: asistencia, resultados y promoción calculada según las reglas institucionales.
6. Ejecutar pruebas aisladas de API, permisos, migraciones, colas, correo, render/PDF e histórico; luego pruebas de campo autorizadas por el propietario. No tomar la aprobación de tests locales como certificación de producción.

**Documentos a reconciliar antes de marcar módulos como completos:**

- `PLAN_COMPLETAR_CICLO_ACADEMICO.md`: sustituir la propuesta de aprobación/generación por lote por el flujo individual y agregar estas condiciones de observación, indicadores y eventos.
- `documentacion-girgit/.../boletines-y-reportes-academicos.md`: reemplazar personalización profunda como servicio obligatorio por editor autoservicio según plan; actualizar emisión individual y acceso solo de estudiante, sin portal de acudiente implementado.
- `documentacion-girgit/.../logros-e-indicadores.md`: permitir indicadores comunes a todos los períodos además de los específicos, sin perder valoración individual ni bloqueo histórico.
- `documentacion-girgit/.../calendario-escolar.md`, `tareas-y-actividades.md` y `notificaciones.md`: separar tarea de evento, registrar fecha de publicación y política de correo optativo por evento, con destinatarios estudiantes únicamente.
- Matriz de permisos y criterios de aceptación: añadir alcances de rector, coordinación, secretaría, docente asignado, revisión y emisión. No ampliar acceso solo desde la interfaz.

## 8. Decisiones aún por confirmar al diseñar cada módulo

- Si las tareas publicadas con vencimiento deben verse **solo el día límite** (regla asumida aquí) o también como una banda continua desde publicación hasta límite.
- Quién puede cambiar indicadores compartidos entre grupos y si necesita aprobación antes de que afecten valoraciones futuras.
- Cómo se presenta la observación final en cada plantilla publicada; la obligatoriedad ya se decidió como configuración del colegio.
- Destinatarios de avisos por edición/cancelación de eventos y valor inicial del control «Enviar por correo». Ninguna de estas decisiones debe causar envíos masivos implícitos.
