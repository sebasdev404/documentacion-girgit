---
titulo: Alcance y no-alcance
modulo: vision-y-alcance
tipo: referencia
estado: borrador
tags: [alcance, scope]
---

# Alcance y no-alcance

## En el alcance

### Plataforma

- Multi-tenancy con base de datos aislada por colegio + subdominio (o dominio propio configurable).
- Panel de superadministración para creación, suspensión y eliminación de tenants.
- Backups automáticos diarios por tenant y exportación completa bajo demanda.
- Log de auditoría inmutable.

### Académico

- Configuración inicial del colegio: datos institucionales, calendario (A o B), jornadas, bloques, escala valorativa, método de aprobación, modelo pedagógico por nivel.
- Estructura académica: plan de estudios, áreas, materias, grados, grupos, espacios físicos, asignación de docentes, horarios.
- Logros e indicadores por materia y periodo.
- Registro de notas por componente evaluativo según método configurado.
- Asistencia por sesión.
- Justificaciones de inasistencia.
- Boletines por periodo, certificados de notas finales, constancias de estudio, carné estudiantil, paz y salvo, informe disciplinario, consolidado de notas por grupo.
- Nivelaciones, habilitaciones, plan de mejoramiento.
- Consejo académico con registro de decisiones.
- Promoción y reprobación automática al cierre del año.
- Observador del estudiante.

### Matrícula y pagos

- Inscripción de aspirantes con pago de matrícula y generación de PIN.
- Formulario de matrícula configurable con subida de documentos y revisión.
- Creación automática del usuario estudiante al cierre del proceso.
- Configuración de conceptos cobrables (matrícula, pensión, certificados, etc.).
- Cobro de pensiones y otros conceptos a través de pasarelas configuradas por el colegio.
- Cálculo de mora e intereses según política del colegio.
- Paz y salvo automático y manual.

### Comunicación

- Agenda y publicaciones con segmentación por institución, nivel, grado, grupo o materia.
- Comunicados institucionales.
- Notificaciones por portal y correo electrónico ante eventos del sistema.

### Histórico

- Inmutabilidad de años cerrados.
- Regeneración fiel de documentos históricos con configuración vigente al momento de emisión.

## Fuera del alcance

- **Gestión de nómina y recursos humanos del colegio.** No se manejan contratos, liquidaciones ni horas extra del personal docente o administrativo.
- **Inventario y administración de activos físicos del colegio.**
- **Plataforma LMS de contenido educativo:** no se gestionan tareas, materiales de clase, foros ni contenido pedagógico interactivo. La plataforma es de gestión, no de aprendizaje.
- **Mensajería bidireccional tipo chat** entre estudiantes y docentes. La agenda es difusión, no conversación.
- **Transporte escolar** (rutas, conductores, ubicación en tiempo real).
- **Cafetería y alimentación escolar** (pedidos, menús, control nutricional).
- **Reportes oficiales al Ministerio de Educación** (SIMAT, ICFES) automatizados. La secretaría puede exportar datos para subirlos manualmente, pero la plataforma no se conecta directamente.
- **Aplicación móvil nativa** en el lanzamiento. El portal es web responsive.
- **Integración WhatsApp** como canal masivo de notificaciones. Es funcionalidad de plan premium futuro.

## Decisiones de exclusión y razones

| Excluido | Razón |
| --- | --- |
| LMS de contenido | El mercado ya tiene actores fuertes (Classroom, Moodle); el foco es gestión, no aprendizaje. |
| Chat bidireccional | Complejidad operativa alta y problemas de moderación/privacidad con menores de edad. |
| Nómina | Mercado distinto, normativa laboral compleja; no aporta a la propuesta de valor central. |
| App móvil nativa de lanzamiento | Costo de desarrollo y mantenimiento doble; web responsive cubre la mayoría de casos. |
| WhatsApp masivo | Costo por mensaje, restricciones de la API oficial, complejidad de plantillas aprobadas. |

## Posibles ampliaciones futuras

- App móvil nativa para estudiantes y acudientes.
- Integración WhatsApp como canal premium de notificaciones.
- Integración directa con SIMAT y otros reportes oficiales.
- Marketplace de plantillas de boletín diseñadas profesionalmente.
- Módulo de orientación escolar (psicología) con privacidad reforzada.
- Expansión a otros países de Latinoamérica.

## Notas y pendientes

- Validar con colegios piloto qué exclusiones generan más fricción.
