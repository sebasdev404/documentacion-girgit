---
titulo: Glosario
modulo: vision-y-alcance
tipo: referencia
estado: borrador
tags: [glosario, terminologia]
---

# Glosario

Definiciones de términos del dominio. Usar este glosario como fuente única de verdad para nombrar entidades en el código y en la documentación.

## Términos

| Término | Definición | Notas |
| --- | --- | --- |
| Tenant | Colegio dentro de la plataforma. Cada tenant tiene base de datos aislada y subdominio propio. | Equivale a "colegio" en el dominio del usuario final. |
| Superadministrador | Único actor de la plataforma con visibilidad cross-tenant. Crea, suspende, elimina tenants y restaura backups. | No pertenece a ningún colegio. |
| Administrador del colegio | Usuario del tenant con mayor nivel de permisos. Típicamente el rector. | Configurable: el colegio puede renombrar el rol. |
| Año lectivo | Ciclo académico anual del colegio. En Calendario A es un año calendario; en Calendario B cruza dos años calendario. | Identificación: "2026" para A, "2025-2026" para B. |
| Calendario A | Calendario académico que va de febrero a noviembre dentro de un mismo año calendario. | Estándar en colegios oficiales y muchos privados. |
| Calendario B | Calendario académico que va de septiembre a junio cruzando dos años calendario. | Solo colegios privados. |
| Periodo académico | Subdivisión del año lectivo (bimestre, trimestre, etc.). El número y duración los define el colegio. | Generalmente 4. |
| Jornada | Bloque horario diario en que el colegio opera (Mañana, Tarde, Única, etc.). | Cada jornada tiene su propia hora de inicio y fin. |
| Bloque horario | Espacio dentro de una jornada donde se dicta una clase. | Configurable en duración. |
| Grado | Nivel educativo (ej. Grado 9, Transición). | |
| Grupo | Sección dentro de un grado (ej. 9A, 9B). | Si el colegio no maneja secciones, el grupo coincide con el grado. |
| Director de grupo | Complemento de rol que un docente puede tener sobre un grupo específico. | Otorga permisos adicionales sobre ese grupo. |
| Plan de estudios | Conjunto de materias por grado y año lectivo, con su intensidad horaria y área. | |
| Área del conocimiento | Agrupación de materias relacionadas. Sirve para promediar por área. | |
| Asignación docente | Combinación materia × grupo × año lectivo asignada a un docente. | Determina los permisos de registro de notas/asistencia. |
| Componente evaluativo | Cada parte que compone la nota de un periodo (ej. quiz, examen, taller). | Aplica si el método de aprobación es por porcentajes ponderados. |
| Escala valorativa | Forma en que se califica al estudiante. Puede ser numérica (rango configurable) o por imágenes. | Puede variar por nivel educativo. |
| Método de aprobación | Regla con la que el sistema determina si un estudiante aprueba una materia. | Promedio simple, porcentajes ponderados o sumatoria dividida. |
| Logro / indicador de desempeño | Objetivo de aprendizaje esperado por materia y periodo. | El docente marca por estudiante si lo alcanzó. |
| Boletín | Documento PDF con las notas, logros, observaciones e inasistencias del estudiante en un periodo o al cierre del año. | Versionado por plantilla y configuración. |
| Nivelación | Proceso de recuperación de una materia perdida al cierre de un periodo. | |
| Habilitación | Proceso de recuperación de una materia perdida al cierre del año lectivo. | |
| Plan de mejoramiento | Compromisos y actividades de refuerzo asociadas a una nivelación o habilitación. | |
| Consejo académico | Reunión que decide el resultado final de estudiantes en situación límite. | Su decisión puede sobreescribir el cálculo automático. |
| Promoción | Avance de un estudiante al grado siguiente al cierre del año lectivo. | |
| Observador del estudiante | Documento acumulativo anual con anotaciones disciplinarias y de convivencia. | Solo lectura para el estudiante. |
| Matrícula | Proceso de inscripción de un aspirante a un grado de un año lectivo. | Inicia con un pago y genera un PIN. |
| PIN de matrícula | Código único asociado a un pago de matrícula que da acceso al formulario de inscripción. | Tiene vigencia configurable por el colegio. |
| Aspirante | Persona en proceso de matrícula que aún no es estudiante del colegio. | No tiene usuario en el sistema hasta el cierre del proceso. |
| Acudiente | Padre, madre o tutor responsable del estudiante. | Tipo de usuario distinto al estudiante; puede compartir rol. |
| Pensión | Cobro recurrente (mensual u otra periodicidad) que el estudiante paga al colegio durante el año lectivo. | |
| Concepto cobrable | Cualquier valor que el colegio cobra a través de la plataforma (matrícula, pensión, certificado, constancia, carné, otros). | |
| Paz y salvo | Estado del estudiante respecto a sus obligaciones de pago y entrega de documentos. | Puede bloquear documentos según configuración del colegio. |
| Agenda / publicación | Contenido (texto, imagen, video, archivo) publicado por la institución hacia un alcance específico. | Comunicación unidireccional. |
| Alcance de publicación | Audiencia a la que se dirige una publicación: institución, nivel, grado, grupo o materia. | |
| Cuota de almacenamiento | Espacio máximo asignado al tenant según su plan. | Aplica a logos, fotos, documentos, PDFs y multimedia. |
| Histórico | Datos de años lectivos cerrados. Inmutables para todos los usuarios del tenant. | |
| Backup por tenant | Copia de seguridad diaria de la base de datos de un colegio. | Restauración solo por superadministrador. |
| Log de auditoría | Registro inmutable de toda acción sensible en el sistema. | Solo lectura, ni siquiera el administrador puede modificarlo. |

## Siglas y abreviaturas

| Sigla | Significado |
| --- | --- |
| SaaS | Software as a Service |
| MEN | Ministerio de Educación Nacional (Colombia) |
| NIT | Número de Identificación Tributaria |
| DIAN | Dirección de Impuestos y Aduanas Nacionales (Colombia) |
| SIMAT | Sistema Integrado de Matrícula del MEN |
| MFA | Multi-Factor Authentication |
| SSO | Single Sign-On |
| PDF | Portable Document Format |
| PIN | Personal Identification Number — código de matrícula |
| KPI | Key Performance Indicator |
| MRR | Monthly Recurring Revenue |
| LTV | Lifetime Value |
| CAC | Customer Acquisition Cost |

## Notas y pendientes

- Mantener el glosario sincronizado: cuando se agregue un concepto nuevo en cualquier módulo, registrarlo aquí.
