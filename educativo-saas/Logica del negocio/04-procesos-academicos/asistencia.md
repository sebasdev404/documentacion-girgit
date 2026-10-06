---
titulo: Asistencia
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [asistencia, proceso]
---

# Asistencia

## Descripción

Proceso por el cual los docentes registran la presencia o inasistencia de los estudiantes en cada franja de clase. La captura, la acumulación/alerta provisional y la solicitud, revisión y aprobación de justificaciones están en código de trabajo. Las consecuencias académicas automáticas por umbral siguen pendientes.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[roles/06-docente\|Docente]] | Registra la asistencia de las sesiones de las materias en las que tiene asignación activa. |
| [[roles/07-director-de-grupo\|Director de Grupo]] | Tiene visibilidad consolidada de la asistencia de su grupo. |
| [[roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Recibe alertas y gestiona casos de inasistencia recurrente. |
| [[roles/02-coordinador-academico\|Coordinador Académico]] | Recibe alertas relacionadas a desempeño académico. |
| [[roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | Consulta el registro propio y puede justificar inasistencias. |

## Tipos de marca

| Marca | Descripción | Cuenta para inasistencia |
| --- | --- | --- |
| Presente | El estudiante asistió a la sesión. | No |
| Ausente | El estudiante no asistió ni hay justificación. | Sí |
| Tarde | El estudiante llegó después del inicio de la sesión. | Configurable: si supera N tardes equivale a una inasistencia. |
| Justificada | Inasistencia o tardanza con corrección aprobada. | Permanece en el historial y en el total de franjas registradas; no suma a las faltas sancionables. |

## Flujo principal

1. El docente abre la sesión correspondiente al bloque y materia que está dictando.
2. El sistema muestra el listado del grupo con cada estudiante.
3. El docente marca el estado de cada estudiante (presente / ausente / tarde).
4. El docente guarda el registro.
5. El sistema actualiza los conteos acumulados por estudiante, materia y periodo.
6. Si algún estudiante **alcanza** el umbral de cantidad o porcentaje configurado, el sistema muestra una alerta provisional a quien puede consultar la asignación.

### Unidad de registro y política — decisión de producto del 5 de octubre de 2026

- Registrar la asistencia por **cada franja explícita programada del grupo y la asignatura**, incluso si el colegio no usa bloques horarios fijos. Una franja larga cuenta como una oportunidad, no como tantas horas dure. Dos faltas requieren dos franjas explícitas en Horarios; si asiste a una de ellas, solo hay una ausencia.
- La duración física de cada franja puede variar. No convertir automáticamente minutos de clase en "horas de inasistencia" sin una regla institucional explícita; la unidad inicial propuesta es la **sesión/franja** del horario.
- El colegio debe poder configurar si la asistencia solo informa y alerta, o si superar un umbral por asignatura repercute en su aprobación. La consecuencia nunca se aplica con un número fijo global como "tres faltas" para todos los colegios.
- Por año lectivo se pueden configurar umbrales por cantidad y porcentaje, combinación «uno cualquiera» o «ambos», acumulación por período o año y equivalencia de N tardanzas a una falta. Al configurar cuatro faltas, la alerta se enciende con la **cuarta**; no espera la quinta. El denominador usa exclusivamente las franjas con asistencia registrada para ese estudiante; los porcentajes son provisionales y la comparación usa el cociente antes de redondear el porcentaje mostrado.
- Captura de presente/ausente/tarde por franja y fecha, con instantánea de identidad y horario, auditoría, control de versión contra sobrescrituras concurrentes y bloqueo de edición ordinaria cuando el período está cerrado. Una falta ya registrada no se quita directamente de la planilla: requiere solicitud y aprobación. Una justificación aprobada tampoco se puede revertir desde la planilla.
- La interfaz principal es una planilla por **año lectivo → grupo → asignatura → período**. El año se elige junto al botón de configuración y, al entrar por primera vez, se preselecciona el año `en_curso`; no se repite su nombre en cada opción de grupo. Los filtros quedan en la URL mediante selectores públicos opacos para conservarse al recargar, sin IDs de base de datos ni datos personales en el almacenamiento del navegador. Cada franja explícita del horario proyecta una columna para cada fecha correspondiente dentro del período; si una clase ya se registró, su columna histórica permanece aunque cambie el horario. Se muestra la lista completa, numerada y ordenada por apellidos. Cada casilla presenta **✓** y **X** como acciones separadas: un clic elige la marca y otro clic en esa misma opción la deja **sin marcar**, antes de guardar. Tab/Mayús+Tab avanzan y retroceden por casillas; las flechas navegan entre filas, columnas y las dos opciones sin cambiar datos; Enter/Espacio activan la opción enfocada. `sin_marcar` es neutral: puede quedar guardada, pero no suma presencia, inasistencia ni denominador porcentual. La configuración institucional se abre en un modal para el año seleccionado; justificaciones y correcciones continúan como flujos separados y auditados. Al cambiar de año, grupo, asignatura o período con marcas pendientes se debe advertir antes de descartarlas. Un período cerrado sigue visible, muestra un aviso y no admite nuevas marcas ni ediciones ordinarias.
- La proyección de fechas **no equivale a una clase efectivamente dictada**. Una fecha futura o una casilla vacía no genera asistencia automáticamente. Queda pendiente integrar calendario de festivos, cancelaciones y vigencia temporal del horario para excluir columnas no dictadas y representar cambios antiguos no registrados; hasta entonces la planilla distingue columnas proyectadas de registradas y no debe usar las primeras como hechos en alertas o sanciones.
- **No hay reprobación automática todavía.** La alerta no modifica nota, boletín ni promoción. Antes de habilitar la consecuencia faltan la exclusión de clases canceladas/festivos, la verificación de completitud del registro, reglas de excepción y pruebas de cierre. El colegio deberá escoger explícitamente si el umbral solo alerta, remite a comité o reprueba.

## Justificaciones de inasistencia

1. El estudiante puede seleccionar una o varias faltas propias de la **misma asignación de grupo y asignatura** y enviar un motivo. Su solicitud queda en `revision_docente`; la marca original continúa vigente.
2. El docente actualmente asignado revisa y remite a aprobación o rechaza con motivo. Puede iniciar directamente una solicitud para una o varias franjas del mismo estudiante y asignatura sin que este envíe primero la justificación.
3. La solicitud remitida pasa a `pendiente_aprobacion`. Solo un usuario con rol habilitado **y** permiso `asistencia.correccion.aprobar` (rector estructural; secretaría o coordinación académica configurables en la matriz) puede aprobar o rechazar.
4. Al aprobar, todas las marcas de la solicitud pasan atómicamente a `justificada`; se registra auditoría por marca, solicitud, usuario y decisión, y se incrementa la versión de las clases afectadas. Si se rechaza, ninguna marca cambia. Una solicitud concurrente para una marca ya pendiente se rechaza.
5. La ausencia sigue visible en el historial de solicitudes, pero ya no suma en el numerador de faltas sancionables. Se conserva el total de franjas registradas. Es posible resolver una fecha de período cerrado mientras el año siga abierto; para corregir un año cerrado primero hay que reabrirlo.
6. Por ahora el motivo es texto. La carga de soportes médicos/adjuntos, el acceso de acudientes y la notificación automática quedan pendientes; no se deben anunciar como disponibles.

### Permisos de asistencia

| Acción | Permiso | Alcance |
| --- | --- | --- |
| Registrar marcas | `asistencia.registrar_clases` | Asignaciones vigentes del docente; rector/coord. con consulta amplia según matriz. |
| Enviar justificación propia | `asistencia.justificar_propia` | Solo rol estudiante y matrícula propia. |
| Solicitar o remitir corrección | `asistencia.correccion.solicitar` | Docente de la asignación vigente; rector/coordinación con acceso amplio y permiso. |
| Aprobar/rechazar | `asistencia.correccion.aprobar` | Rector; secretaría/coordinación solo si el permiso configurable fue concedido. |
| Configurar umbrales | `asistencia.configurar_politica` | Rector; coordinación si se le concede el permiso. |

El plan del colegio debe incluir la función `asistencia`. Añadir permisos a la matriz de código requiere actualizar el catálogo RBAC central y sincronizar cada tenant preservando los permisos configurables existentes.

## Alertas por inasistencia

- El colegio configura un umbral de faltas y/o porcentaje por materia, con alcance por período o año.
- Cuando un estudiante alcanza el umbral configurado, la lista de asistencia muestra una alerta provisional al docente y a los responsables que pueden consultar esa asignación. Las marcas justificadas no suman a las faltas sancionables. Todavía no se envían notificaciones automáticas.
- La consecuencia sobre la nota o la aprobación la define el colegio en su configuración (puede ser perder la materia automáticamente, requerir comité de evaluación, o ninguna).

## Estados y transiciones

### Marca de asistencia

```
No registrada → Registrada → Editada (mientras el periodo esté abierto)
```

### Justificación

```
No solicitada → Revisión docente → Pendiente de aprobación → Aprobada
                               ↘ Rechazada                ↘ Rechazada
No solicitada → Pendiente de aprobación (docente directo) → Aprobada / Rechazada
```

## Datos involucrados

- Sesión (combinación de fecha + bloque + grupo + materia).
- Estudiante.
- Marca (presente / ausente / tarde / justificada).
- Docente que registra.
- Fecha y hora del registro.
- Motivo textual, revisor docente, aprobador y observaciones de la solicitud. Adjuntos pendientes.

## Reportes asociados

- Asistencia por estudiante en un periodo / año.
- Asistencia por grupo y materia.
- % de inasistencia por estudiante (alerta si supera umbral).
- Listado de justificaciones pendientes.

Ver [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]].

## Reglas de negocio

- **RN-AS-001 — Registro solo con asignación activa:** un docente solo puede registrar asistencia en combinaciones materia × grupo donde tiene asignación activa.
- **RN-AS-002 — Asistencia por sesión:** el registro es por cada sesión del horario; no se permite consolidado diario sin granularidad por bloque.
- **RN-AS-003 — Justificación no elimina la inasistencia:** una justificación aprobada cambia la marca a `Justificada` pero la inasistencia permanece en el historial.
- **RN-AS-004 — Alertas automáticas:** la lista muestra alerta provisional al alcanzar el umbral configurado, sin cambiar la aprobación académica.
- **RN-AS-005 — Edición hasta cierre del periodo:** las marcas de asistencia se pueden editar hasta el cierre del periodo. Después solo con ventana de corrección autorizada.
- **RN-AS-006 — Festivos no generan asistencia:** las sesiones que caen en días marcados como festivo no generan registro de asistencia.
- **RN-AS-007 — Auditoría obligatoria:** ediciones de marcas de asistencia quedan registradas en el log con valor anterior y nuevo.

## Notas y pendientes

- **[Decisión tomada]** La acumulación de tardes/llegadas tarde como inasistencia es **configurable por colegio**: cada colegio define cuántas tardes equivalen a una inasistencia (puede dejarlo en cero si no quiere acumular). Regla: **RN-AS-020 — Acumulación de tardes configurable por colegio**.
- **[Pendiente UX]** Validar el flujo de "asistencia por toma rápida" para grupos grandes (marcar todo presente y solo individualizar ausentes) durante el piloto.
