---
titulo: Configuración por colegio
modulo: multi-tenancy
tipo: referencia
estado: borrador
tags: [multi-tenancy, configuracion]
---

# Configuración por colegio

Parámetros que cada colegio puede personalizar dentro de su tenant. La configuración inicial es **obligatoria** antes de operar el sistema; sin completarla el tenant queda en estado `Configurando` y la mayoría de módulos no están disponibles.

Responsable principal: el [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Administrador del Colegio]] (típicamente el rector).

## Configuración inicial obligatoria

La configuración inicial cubre los siguientes bloques. Mientras alguno esté incompleto, el tenant no puede operar normalmente.

### 1. Datos institucionales

| Parámetro | Tipo | Obligatorio | Notas |
| --- | --- | --- | --- |
| Nombre completo del colegio | Texto | Sí | Aparece en documentos generados. |
| Logo institucional | Archivo (imagen) | Sí | Sujeto a cuota de almacenamiento y validaciones de tamaño. |
| NIT | Texto | Sí | Para facturación electrónica. |
| Número de resolución MEN | Texto | Sí | |
| Dirección física | Texto | Sí | |
| Teléfono | Texto | Sí | |
| Correo institucional | Email | Sí | Destinatario de notificaciones críticas. |

### 2. Calendario académico

El colegio selecciona uno de los dos calendarios soportados:

- **Calendario A:** febrero a noviembre dentro de un mismo año calendario. Identificación del año lectivo: "2026".
- **Calendario B:** septiembre a junio cruzando dos años calendario. Identificación del año lectivo: "2025-2026". Nunca como un año simple.

Luego define:

- Fechas exactas de inicio y cierre del año lectivo.
- Número de periodos académicos (configurable, típicamente 4).
- Fechas exactas de inicio y cierre de cada periodo.
- Si maneja un quinto periodo, define cómo se calcula (sumatoria de los anteriores u otro método).

Detalle en [[../04-procesos-academicos/periodos-academicos|Períodos académicos]].

### 3. Jornadas y bloques horarios

Para cada jornada (Mañana / Tarde / Única / nombre personalizado):

- Hora de inicio y hora de fin.
- Número de bloques de clase.
- Duración de cada bloque.
- Tiempos de descanso o recreo entre bloques.

Esta configuración es la base sobre la que se construyen los horarios.

### 4. Escala valorativa

El colegio define cómo califica:

- **Numérica:** rango configurable (ej. 1.0–5.0, 0–10, 1–10) con la cantidad de decimales que el colegio decida.
- **Por imágenes (caritas):** usado en preescolar. El colegio define cuántos niveles tiene la escala, sube una imagen para cada nivel y asigna un valor numérico interno a cada nivel para cálculos.

La escala valorativa **puede variar por nivel educativo** dentro del mismo colegio (ej. preescolar usa imágenes mientras bachillerato usa numérica).

### 5. Método de aprobación

El colegio define:

- **Cómo se calcula la nota final del periodo:**
  - Promedio simple de las notas registradas.
  - Porcentajes ponderados por componente evaluativo (cada componente con su peso).
  - Sumatoria de notas dividida entre la cantidad de notas registradas.
- **Nota mínima de aprobación** (ej. 3.0 sobre 5.0).
- **Ámbito de evaluación de aprobación:** materia por materia / por área / por promedio general.

### 6. Modelo pedagógico por nivel educativo

Para cada nivel (Preescolar, Primaria, Secundaria, Media):

- Docente único que permanece todo el día **vs.** rotación de docentes por materia.
- Estudiantes en salón fijo **vs.** desplazamiento a aulas especializadas.
- Existencia de Director de Grupo y permisos del director sobre su grupo.

### 7. Configuración de pagos

- Cuentas bancarias o pasarelas habilitadas para recibir dinero.
- Conceptos cobrables (matrícula, pensión, certificados, constancias, carné, otros personalizados).
- Valor, obligatoriedad, recargos e intereses por mora de cada concepto.

Detalle en [[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos de pensiones]] y [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|Políticas de cobro y mora]].

### 8. Configuración del proceso de matrícula

- Campos obligatorios y opcionales del formulario de inscripción.
- Documentos digitales requeridos por nivel educativo.
- Días de vigencia del PIN tras el pago de matrícula.
- Cupos disponibles por grado.

Detalle en [[../04-procesos-academicos/matriculas|Matrículas]].

### 9. Configuración de publicaciones

- Roles con permiso de publicar.
- Alcances permitidos por rol.

Detalle en [[../05-comunicacion/agenda-y-publicaciones|Agenda y publicaciones]].

## Parámetros configurables (resumen)

| Parámetro | Tipo | Default | Quien lo edita |
| --- | --- | --- | --- |
| Datos institucionales | Texto / archivo | — | Administrador |
| Tipo de calendario | A o B | — | Administrador |
| Número de periodos | Entero | 4 | Administrador |
| Escala valorativa | Numérica o por imágenes | — | Administrador |
| Método de aprobación | Enum | — | Administrador |
| Nota mínima de aprobación | Decimal | — | Administrador |
| Modelo pedagógico por nivel | Configuración | — | Administrador |
| Plantilla de boletín | Selección + personalización | Plantilla base | Administrador |
| Conceptos cobrables | Lista | — | Administrador / Secretaría |
| Documentos requeridos en matrícula | Lista | — | Administrador |
| Vigencia del PIN de matrícula | Entero (días) | 15 | Administrador |
| Cupos por grado | Entero | — | Administrador / Coordinación |
| Permisos de publicación por rol | Configuración | Defaults del sistema | Administrador |
| Eventos notificables (activar/desactivar) | Booleano por evento | Defaults del sistema | Administrador |
| Bloqueo de documentos por paz y salvo | Configuración | Ninguno | Administrador |

## Branding (logo, colores, dominio)

- Logo institucional (sujeto a cuota).
- Colores institucionales aplicados a la plataforma del colegio.
- Dominio propio opcional, sujeto a verificación DNS.

## Idioma y localización

- Idioma por defecto: español (Colombia).
- Zona horaria configurable.
- Formato de fechas y moneda según localización.

## Calendario y zona horaria

- La zona horaria del tenant define cómo se interpretan las marcas de tiempo en asistencia, pagos, publicaciones y log de auditoría.
- Una vez fijada en la configuración inicial, cambiar la zona horaria requiere intervención del superadministrador.

## Reglas de negocio

- **RN-CC-001 — Configuración inicial obligatoria:** el tenant no es operable hasta que la configuración inicial mínima esté completa.
- **RN-CC-002 — Calendario inmutable durante el año lectivo:** el tipo de calendario (A o B) no se puede cambiar mientras haya un año lectivo activo o cerrado. Cambios solo posibles antes de iniciar el primer año lectivo.
- **RN-CC-003 — Escala por nivel:** cada nivel educativo puede tener su propia escala valorativa configurada.
- **RN-CC-004 — Cambios de configuración auditados:** cualquier cambio en la configuración del colegio queda registrado en el log de auditoría con valor anterior y nuevo.
- **RN-CC-005 — No se modifica configuración histórica:** la configuración vigente al momento de la emisión de un documento (boletín, certificado) se preserva. Cambios posteriores no afectan la regeneración del documento histórico.

## Notas y pendientes

- Definir lista exacta de eventos notificables y sus defaults.
- Definir si el colegio puede tener múltiples logos (uno para portal, uno para boletines).
