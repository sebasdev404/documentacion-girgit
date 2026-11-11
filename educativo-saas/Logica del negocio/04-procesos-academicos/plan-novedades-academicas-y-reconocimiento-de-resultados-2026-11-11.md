---
titulo: Plan de novedades académicas y reconocimiento de resultados
fecha: 2026-11-11
modulo: procesos-academicos
tipo: propuesta
estado: propuesto-pendiente-de-revision
tags: [matriculas, trayectoria, traslados, calificaciones, siee, promocion, auditoria]
---

# Plan de novedades académicas y reconocimiento de resultados

**Propuesta pendiente de revisión funcional, institucional y técnica.** Las etapas y asignaciones de permisos descritas aquí requieren validación antes de su implementación. El objetivo es atender correcciones de matrícula, cambios de grupo o grado, ingresos durante el año y reconocimiento de estudios previos, conservando la trayectoria del estudiante y la procedencia de cada resultado.

El colegio necesita decidir cómo tratar las diferencias de currículo, actividades, escalas y periodos. El sistema debe presentar las evidencias, aplicar las reglas aprobadas y registrar la decisión. La propuesta inicial mantiene pendientes los resultados que requieren soporte o valoración hasta que el colegio resuelva su tratamiento.

## Relación con los procesos existentes

- [Matrículas](matriculas.md) describe el ingreso y la confirmación de la matrícula.
- [Calificaciones](calificaciones.md) contiene el registro y cálculo académico ordinario.
- [Promoción y reprobación](promocion-y-reprobacion.md) corresponde al cierre ordinario del año.
- [Boletines y reportes académicos](boletines-y-reportes-academicos.md) contiene el proceso de emisión.
- [Matriz de permisos](../02-usuarios-roles-y-permisos/matriz-de-permisos.md) mantiene el catálogo y las autorizaciones operativas.

Las reglas propuestas en esta página deben incorporarse a esos procesos y a la matriz cuando se apruebe cada etapa. La sección de permisos de este plan sirve como base de discusión.

## Base técnica observada

La revisión del código local realizada el 11 de noviembre de 2026 identificó los siguientes puntos de integración.

| Componente actual | Comportamiento observado | Ampliación propuesta |
| --- | --- | --- |
| Matrícula académica | Existe una matrícula por estudiante y año, asociada a un grupo. | Incorporar la trayectoria de ubicaciones con fechas efectivas. |
| Cambio de grado de la inscripción | Permite cambiar el grado autorizado durante la revisión y antes de confirmar la matrícula. | Añadir una operación académica para estudiantes ya matriculados. |
| Calificaciones | Las notas conservan su relación con la actividad y la matrícula. Los informes consultan las asignaciones del grupo actual. | Resolver también el contexto histórico y los resultados reconocidos del destino. |
| Definitivas manuales | Existen resultados manuales sujetos a los modos configurados en el SIEE. | Permitir el reconocimiento individual de resultados con procedencia y aprobación propias. |
| Resultados incompletos | El cálculo estricto devuelve un estado pendiente cuando faltan notas. | Identificar la causa y el procedimiento de resolución de cada pendiente. |
| Escritura de notas | Exige año en curso y periodo abierto. | Crear una autorización específica para incorporar resultados anteriores de un estudiante. |
| Boletines emitidos | La emisión utiliza una copia de los datos académicos y una huella de contenido. | Vincular rectificaciones y nuevas emisiones con sus antecedentes. |
| Promoción ordinaria | El cálculo requiere periodos cerrados y resultados completos. | Integrar resultados reconocidos aprobados y desarrollar el flujo de promoción anticipada. |

Las referencias de implementación están en el repositorio `colegio-saas-backend`, principalmente en `EnrollmentWorkflow`, `EnrollmentIntake`, `GradebookService`, `GradeCalculationService`, `AcademicPromotionService`, `BulletinIssueService` y el modelo `Matricula`. Esta revisión identifica puntos de partida para el diseño.

## Casos que debe atender

| Caso | Tratamiento propuesto | Evidencia o decisión requerida |
| --- | --- | --- |
| Grado o grupo equivocado antes de iniciar actividad académica | Corregir la ubicación y registrar el movimiento. | Motivo, responsable, fecha y comprobación de la información existente. |
| Cambio de grupo dentro del mismo grado con notas | Conservar el contexto de origen y reconocer los resultados pertinentes en el destino. | Revisión de actividades, materias, periodos y pendientes. |
| Corrección de grado con información académica | Registrar la corrección y revisar las equivalencias del nuevo currículo. | Justificación del error y tratamiento aprobado de los resultados. |
| Llegada de otro colegio con certificados | Registrar las definitivas de los periodos cursados y aprobar su correspondencia. | Institución de origen, certificado, escala y periodos acreditados. |
| Llegada con estudios previos y certificados pendientes | Registrar la incorporación y abrir pendientes de soporte. | Responsable de seguimiento y plazo definido por el colegio. |
| Incorporación tardía con periodos no cursados | Registrar la circunstancia y definir un plan individual de valoración. | Motivo, competencias por valorar, responsables y procedimiento institucional. |
| Promoción anticipada | Tramitar la decisión y sus efectos en currículo, grupo y resultados. | Condiciones normativas, consentimiento y acta correspondiente. |
| Cambio durante un periodo en curso | Consolidar individualmente las evidencias anteriores y posteriores. | Regla de integración, ponderaciones cuando correspondan y aprobación. |
| Materia presente únicamente en el destino | Crear un pendiente de equivalencia o valoración. | Evidencia, evaluación o decisión institucional que resuelva el resultado. |
| Rectificación de un movimiento aplicado | Registrar una actuación vinculada al movimiento anterior. | Motivo, responsable y análisis de los efectos ya producidos. |

La comprobación de actividad académica debe abarcar notas, asistencias, entregas del aula, recuperaciones, observaciones y documentos emitidos. El flujo debe admitir varios movimientos durante el mismo año, incluido el retorno a un grupo anterior.

## Condiciones normativas para el diseño

### Evaluación y promoción en básica y media

El SIEE debe contemplar criterios de evaluación, escala y equivalencia nacional, estrategias de valoración y apoyos para situaciones pedagógicas pendientes. La propuesta utiliza esas reglas institucionales para decidir el tratamiento de resultados anteriores, diferencias de currículo y periodos no cursados. Las reglas que se configuren deben corresponder al SIEE adoptado por el colegio. [Decreto 1075 de 2015, artículos 2.3.3.3.3.4 a 2.3.3.3.3.6](https://normograma.sena.edu.co/compilacion/docs/decreto_1075_2015_pr011.htm)

La promoción anticipada ordinaria se contempla durante el primer periodo. Requiere consentimiento de los padres, recomendación del Consejo Académico y decisión del Consejo Directivo consignada en acta. El ejemplo de un ascenso por rendimiento durante el tercer periodo queda pendiente de determinar su fundamento aplicable antes de habilitar una operación de ese tipo. [Orientaciones del Ministerio de Educación sobre el SIEE](https://www.mineducacion.gov.co/portal/micrositios-preescolar-basica-y-media/Evaluacion/Evaluacion-de-estudiantes/397381%3ASistema-Institucional-de-Evaluacion-de-los-Estudiantes-SIEE)

Una constancia de promoción del colegio de procedencia acredita el grado al que debe ingresar el estudiante. La evaluación diagnóstica permite identificar apoyos. El Ministerio indica que esa evaluación no autoriza ubicarlo en un grado inferior al certificado. La corrección de un error administrativo debe comprobar el antecedente que sustenta la ubicación correcta. [Orientaciones del Ministerio de Educación sobre movilidad y evaluación diagnóstica](https://www.mineducacion.gov.co/portal/micrositios-preescolar-basica-y-media/Evaluacion/Evaluacion-de-estudiantes/397381%3ASistema-Institucional-de-Evaluacion-de-los-Estudiantes-SIEE)

### Revisión institucional pendiente

Cada colegio debe definir las evidencias y el procedimiento para valorar competencias de quien ingresa con periodos no cursados. Registrar una evaluación y asignarla a un resultado anterior requiere una decisión sustentada en ese procedimiento. La fecha real de la valoración y el periodo al que se aplica deben quedar registrados.

Las reglas de evaluación y promoción deberán revisarse por nivel educativo, incluyendo preescolar cuando corresponda. La interfaz y el cálculo deben admitir las escalas cualitativas y visuales configuradas para el nivel.

## Trayectoria y datos de la matrícula

Se propone conservar una matrícula por estudiante y año, con ubicaciones históricas por grado y grupo. Cada ubicación tendrá un intervalo de vigencia y el movimiento que la originó. La ubicación actual se derivará de la trayectoria aplicada.

Cada movimiento registrará el tipo de caso, matrícula, ubicación anterior y destino, fecha efectiva, fecha de registro, motivo, responsable, soportes y decisión de aprobación. Los intervalos deben ser coherentes y permitir reconstruir dónde estaba el estudiante en una fecha determinada.

Las calificaciones conservarán su actividad, asignatura, docente y contexto de origen. Las equivalencias apuntarán a esos resultados o a los certificados externos que las sustentan. Las notas ya registradas deberán seguir consultables desde el expediente individual.

Los datos propuestos se agrupan en las siguientes entidades conceptuales. Su representación definitiva se resolverá al revisar las tablas y servicios existentes.

| Información | Datos principales |
| --- | --- |
| Movimiento académico | Caso, origen, destino, fechas, motivo, autor, aprobador y soportes. |
| Ubicación histórica | Matrícula, grado, grupo e intervalo de vigencia. |
| Resultado reconocido | Estudiante, materia y periodo de destino, valor original, escala, valor reconocido, origen y versión. |
| Correspondencia académica | Materia o área de origen, destino, fechas cubiertas y criterio de equivalencia. |
| Pendiente académico | Causa, competencias o soporte requerido, responsable, plazo y resolución. |
| Decisión y documento | Acta, constancia, resultado aprobado, fecha, versión y vínculos con antecedentes. |

Un cambio dentro del mismo colegio debe actualizar cupos de grupo y listados conservando el cómputo único del estudiante en el contrato. La incorporación desde otra sede con base aislada requiere resolver explícitamente el intercambio autorizado de antecedentes y la identidad del estudiante.

## Reconocimiento de resultados

### Periodos completos de otra institución

El expediente ofrecerá una tabla individual por materia o área y periodo acreditado. Permitirá registrar institución de procedencia, fechas cubiertas, valor original, escala, soporte, correspondencia de destino y resultado reconocido.

Si las escalas difieren, el responsable deberá utilizar una equivalencia institucional aprobada. El valor original y el criterio aplicado quedarán disponibles en la revisión. La conversión deberá contemplar también resultados cualitativos.

Los periodos se relacionarán por su cobertura académica y temporal. Un calendario de tres periodos y otro de cuatro requerirán una correspondencia explícita. Cuando el origen informe un área conjunta y el destino varias materias, el colegio deberá resolver la distribución mediante evidencia o valoración.

### Actividades y preinformes diferentes

Para un periodo completo se propone reconocer la definitiva aprobada de la materia. Por ejemplo, las seis actividades cursadas en un grupo seguirán consultables en su contexto original, mientras la planilla del grupo de destino mostrará la definitiva reconocida y un acceso a su procedencia.

Las celdas de actividades que no correspondan al estudiante mostrarán una condición explícita de aplicabilidad. Esto debe funcionar con preinformes, actividades simples, actividades ponderadas y resultados manuales.

La coincidencia del nombre de una asignatura permitirá sugerir una correspondencia. La aprobación considerará el grado, las competencias y la evidencia. Matemáticas de Primero y Matemáticas de Segundo requieren esa revisión académica.

### Cambio durante un periodo abierto

La consolidación individual reunirá la evidencia obtenida antes del cambio y la evaluación realizada después. El responsable definirá el tratamiento conforme al SIEE y revisará el resultado propuesto antes de aprobarlo.

El cálculo deberá identificar qué evidencia interviene, la fecha de corte y las ponderaciones utilizadas. El procedimiento también deberá contemplar actividades anteriores a la incorporación que el estudiante todavía necesite realizar como parte de su plan de apoyo.

### Materias nuevas y periodos no cursados

Una materia pendiente tendrá una causa identificable, como falta de certificado, falta de correspondencia, periodo no cursado o valoración por realizar. Se asignarán responsable y seguimiento.

La propuesta permite la incorporación al grupo mientras se resuelven esos pendientes. Los informes y decisiones que requieran resultados completos indicarán los elementos todavía necesarios.

Para quien no cursó los periodos anteriores, el colegio podrá registrar un plan individual de valoración y apoyo. Cada resultado tendrá evidencia y aprobación. La propuesta inicial mantendrá pendientes esos periodos hasta resolver su tratamiento.

La eventual exclusión de periodos del cálculo anual y la redistribución de pesos quedan como decisión pendiente. Su implementación requerirá una regla institucional explícita y validación de su aplicabilidad al caso.

## Resultados efectivos y periodos cerrados

El sistema resolverá un único resultado efectivo por estudiante, materia y periodo, con su procedencia identificada. Podrá corresponder al cálculo de actividades, a un reconocimiento de estudios externos, a un reconocimiento interno o a una valoración autorizada.

Cuando concurran un resultado ordinario y otro propuesto, la interfaz mostrará el conflicto. Una decisión motivada determinará el resultado efectivo y conservará sus versiones y antecedentes. Una recuperación posterior deberá poder identificar el resultado sobre el que se aplicó.

Se propone una operación específica para incorporar resultados anteriores en periodos cerrados. Su autorización delimitará estudiante, materia, periodo, motivo y soporte. Los registros conservarán la fecha real de incorporación.

El tratamiento de años ya cerrados debe integrar el procedimiento institucional existente de corrección y reapertura autorizada. La primera etapa se centrará en el año de la matrícula que todavía esté en curso o preparación, según la operación.

Los promedios anuales consumirán resultados efectivos aprobados y las reglas de ponderación correspondientes. El estado pendiente tendrá un motivo visible. La vista provisional y el resultado oficial deberán identificar su grado de completitud.

## Boletines constancias y certificados

Cada boletín emitido conservará su archivo, datos de emisión y relación con la ubicación académica de ese momento. Si una rectificación requiere otro boletín, se generará una nueva emisión vinculada al antecedente y al motivo.

El expediente reunirá los certificados externos recibidos y los documentos expedidos por el colegio. Las constancias generadas por el sistema deberán identificar consecutivo, estudiante, año, decisión, responsables, fecha y versión. Su expedición dependerá del estado aprobado de la actuación correspondiente.

Antes de implementar la generación se deben definir los tipos de documento, firmantes y mecanismo de validación que necesita el colegio. El flujo debe registrar la aprobación del órgano competente cuando la decisión sea colegiada.

## Propuesta de interfaz

La ficha del estudiante será accesible desde Matriculados y Gestión de usuarios. La navegación propuesta comprende Trayectoria académica, Resultados anteriores, Pendientes académicos, Documentos e Historial.

La acción **Registrar novedad académica** iniciará el proceso con los siguientes pasos.

1. Seleccionar el caso y la fecha efectiva.
2. Seleccionar el destino cuando corresponda y describir el motivo.
3. Consultar el resumen de notas, asistencias, entregas, recuperaciones y documentos existentes.
4. Registrar correspondencias, resultados propuestos y pendientes del destino.
5. Adjuntar los soportes requeridos por el caso y revisar los efectos previstos.
6. Presentar la actuación para revisión y aprobación según los permisos configurados.
7. Aplicar la decisión y publicar la información que deba conocer el estudiante.

Una corrección administrativa con escasa información podrá usar un recorrido más breve, conservando motivo, responsable, fecha y registro de la actuación. Las aprobaciones deberán identificar al usuario que las ejecutó.

En Configuración SIEE se propone administrar las reglas de equivalencias, escalas, incorporación tardía, periodos no cursados y aprobación de resultados excepcionales. Cada decisión aplicada referenciará la versión institucional utilizada.

## Permisos propuestos para revisión

Las acciones siguientes deberán conciliarse con el catálogo existente antes de definir claves nuevas. La autorización efectiva comprobará colegio, recurso, permiso y asignación académica cuando corresponda.

| Acción | Asignación inicial propuesta | Alcance |
| --- | --- | --- |
| Consultar trayectoria | Rector y coordinación académica o combinada | Estudiantes del colegio bajo su autorización. |
| Consultar antecedentes para docencia | Docente o director autorizado | Estudiantes y materias de su alcance académico. |
| Registrar una novedad | Rector, coordinación o secretaría autorizada | Presentar el caso con motivo y soportes. |
| Cargar resultados externos | Secretaría o coordinación autorizada | Registrar certificados y valores de origen. |
| Proponer equivalencias o valoraciones | Coordinación y docentes autorizados | Materias y casos que les correspondan. |
| Aprobar movimientos y reconocimientos | Rector o responsable académico autorizado | Decisión motivada y evidencia de la competencia institucional. |
| Incorporar resultados en periodos cerrados | Permiso adicional específico | Estudiante, materia y periodo delimitados. |
| Rectificar una actuación aplicada | Permiso específico | Nueva actuación vinculada al antecedente. |
| Expedir constancias | Responsable autorizado por el colegio | Decisiones aprobadas y plantillas institucionales. |
| Consultar decisiones publicadas | Estudiante | Su propio expediente. |

El número de revisores y la posibilidad de que una persona registre y apruebe quedarán sujetos al procedimiento institucional y a los requisitos del caso. La matriz deberá reflejar esas decisiones para los roles base y adicionales.

## Auditoría notificaciones y aplicación de cambios

La auditoría conservará actor, fecha, operación, valores anteriores y nuevos, motivo, soportes y versión de la política aplicada. La fecha efectiva académica se distinguirá de la fecha de ejecución.

Los borradores, observaciones de revisión, decisiones y rectificaciones formarán parte del historial autorizado. Una rectificación tendrá relación explícita con la actuación que corrige.

Registros mostrará las operaciones administrativas. Novedades mostrará las decisiones publicadas que deba consultar el estudiante y enlazará su expediente. El correo acompañará esas decisiones y tendrá seguimiento de entrega y reintento.

La aplicación de una decisión deberá comprobar que el expediente, los resultados y los cupos siguen correspondiendo a la versión revisada. El backend resolverá de forma transaccional el movimiento y sus efectos. Los reintentos deberán reconocer una operación ya aplicada.

Las listas de aula, asistencia, planillas y reportes deberán utilizar las fechas efectivas. El estudiante tendrá acceso al contexto académico vigente y a sus antecedentes según la autorización. Las asistencias anteriores al ingreso se tratarán conforme a su fecha real de vinculación.

## Etapas propuestas

| Etapa | Entrega | Criterio de revisión |
| --- | --- | --- |
| 1 | Trayectoria y corrección de matrícula | Cambios auditados, fechas coherentes y efectos correctos sobre ubicación, listados y cupos. |
| 2 | Resultados anteriores y equivalencias | Registro individual de certificados, correspondencias, versiones y aprobación. |
| 3 | Integración del cálculo | Planillas, preinformes, áreas, resultados anuales y boletines consumen el resultado efectivo correcto. |
| 4 | Incorporación tardía y cambios dentro del periodo | Pendientes, planes de valoración y consolidación individual sustentada. |
| 5 | Promoción anticipada y expedición documental | Condiciones aplicables, actas, constancias, publicaciones y rectificaciones. |

Cada etapa incluirá frontend, backend, esquema PostgreSQL cuando corresponda, permisos, auditoría y criterios de aceptación. Los cambios de esquema deberán ser compatibles con matrículas y resultados existentes. Las pruebas de migración se realizarán sobre copias y bases de prueba.

## Criterios de aceptación propuestos

| Escenario | Resultado esperado |
| --- | --- |
| Corrección antes de clases | Se registra el motivo y la ubicación correcta con su fecha efectiva. |
| Corrección con asistencias o entregas y sin notas | Se detecta la información existente y se conserva su contexto. |
| Cambio de grupo con seis actividades de origen y tres de destino | El expediente conserva el detalle original y la planilla muestra el resultado reconocido aprobado. |
| Cambio de grado con una materia nueva | Se crea un pendiente visible con responsable y forma de resolución. |
| Mismo nombre de materia en grados distintos | Se requiere la revisión de la correspondencia académica. |
| Ingreso en tercer periodo con dos periodos certificados | Los resultados reconocidos intervienen en el cálculo con sus soportes y reglas aprobadas. |
| Certificados todavía pendientes | Se identifica la falta de soporte y se permite hacer seguimiento. |
| Periodos no cursados | Se registra la circunstancia y su plan de tratamiento, con resultados pendientes hasta resolverlo. |
| Escala numérica, cualitativa o visual diferente | Se conserva el valor original y se aplica una correspondencia aprobada. |
| Calendarios de tres y cuatro periodos | La correspondencia identifica fechas y cobertura académica. |
| Área de origen distribuida en varias materias de destino | Se documenta el criterio o la valoración necesaria para resolver los resultados. |
| Cambio a mitad de periodo | La consolidación muestra evidencia, fechas y ponderaciones aplicadas. |
| Resultado ordinario y reconocido concurrentes | El conflicto exige una decisión motivada sobre el resultado efectivo. |
| Periodo cerrado | La incorporación excepcional queda delimitada y auditada. |
| Boletín previamente emitido | Sigue consultable y una rectificación enlaza una nueva emisión cuando corresponda. |
| Varios movimientos o retorno al grupo anterior | La trayectoria permite reconstruir las ubicaciones y resultados por fecha. |
| Dos operadores o reintento de una petición | Se detecta el conflicto de versión o la operación ya aplicada. |
| Actor sin permiso o recurso de otro colegio | La API rechaza la operación y la interfaz refleja su alcance. |
| Revocación de asignación docente | El acceso se ajusta al alcance vigente del usuario. |
| Promoción anticipada | Se comprueban periodo, consentimiento, acta y autoridad competente. |
| Error durante la aplicación | El expediente conserva un estado consistente y la operación puede recuperarse de forma controlada. |

## Decisiones pendientes antes de implementar

1. Confirmar los tipos de novedad y los soportes mínimos para cada caso.
2. Aprobar la matriz inicial y el procedimiento de registro, revisión y decisión.
3. Definir en el SIEE las equivalencias de escalas, materias y periodos.
4. Resolver cómo valorar periodos no cursados y si existe algún supuesto autorizado de exclusión del cálculo anual.
5. Definir la consolidación de evidencias cuando el movimiento ocurre dentro de un periodo.
6. Precisar el tratamiento de años cerrados y de boletines ya expedidos.
7. Validar las reglas aplicables por nivel educativo y las condiciones de promoción anticipada.
8. Definir constancias, firmantes y datos de verificación documental.
9. Confirmar plazos y destinatarios de seguimiento, novedades y correo.
10. Validar el traslado de antecedentes entre sedes con bases de datos aisladas.

La revisión funcional de estas decisiones precede a la implementación de las etapas. Cada entrega deberá actualizar su estado documental con el alcance efectivamente verificado.
