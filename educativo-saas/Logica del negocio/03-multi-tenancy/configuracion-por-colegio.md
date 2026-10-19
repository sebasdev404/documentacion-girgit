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
- Define de 1 a 12 períodos reales por año lectivo. Si habilita el período sumatorio, se muestra después de los reales como P(N+1) y se calcula según el método anual del SIEE, sin fechas ni notas propias. Cinco períodos reales se configuran indicando N = 5.

Detalle en [[../04-procesos-academicos/periodos-academicos|Períodos académicos]].

### 3. Jornadas y bloques horarios opcionales

Para cada jornada (Mañana / Tarde / Única / nombre personalizado):

- Hora de inicio y hora de fin.
- Si el colegio desea franjas predefinidas, configura los bloques de clase y los descansos con hora de inicio y fin.
- Si prefiere horarios flexibles, puede programar cada clase con horas propias sin crear bloques.

La jornada y su sede se obtienen del grupo. Todas las clases deben quedar dentro de la jornada; los bloques no son requisito para construir el horario.

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

- **Ajustes institucionales > Configuración de matrículas**, con acceso directo desde **Matrículas por enlace**: un solo rango permanente por colegio y grado estable, reutilizado entre años, y aviso de privacidad institucional versionado. Requiere `ingreso.configurar`, delegable según la matriz, y capacidad de plan `academico`.
- Rango habilitado: mínimo y máximo inclusivos; deshabilitado: sin límite de edad para ese grado. La edad se calcula a la fecha actual en la zona horaria institucional, sin fecha de corte configurable ni copia anual. Las solicitudes enviadas conservan su constancia de nacimiento/grado validados; cambiar cualquiera de esos datos obliga a revalidar.
- El envío acepta una versión concreta del aviso. Si cambia antes de enviar, se detiene el envío y se exige leer y aceptar el texto actualizado.
- Hasta el primer guardado institucional se conservan los valores heredados de las convocatorias. Solo se sugieren valores existentes inequívocos; los conflictos requieren una elección explícita en el mismo formulario, sin deducir rangos ni escoger automáticamente un aviso.
- **Por convocatoria:** campos obligatorios/opcionales, documentos comunes o por grado, grados ofrecidos y cupos opcionales. El año, fechas y habilitación del enlace siguen siendo propios de la convocatoria.
- **Acceso privado sin pago:** enlace privado más PIN de cuatro dígitos, o desafío privado HttpOnly más PIN en el navegador que inició la solicitud. El vencimiento es una fecha fija opcional por convocatoria; sin fecha no caduca por tiempo. Sustituye la antigua vigencia de 15 días tras el pago. No se crean usuarios de acudiente.

Política aceptada y reglas canónicas RN-MA-015 y RN-MA-018 a RN-MA-021 en [[../04-procesos-academicos/matriculas|Matrículas por enlace]]. Esta actualización documental no certifica despliegue ni pruebas de correo real.

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
| Rangos institucionales de edad por grado estable | Habilitado + mínimo/máximo inclusivos | Sin edades predefinidas; deshabilitado = sin límite | `ingreso.configurar` + plan `academico` |
| Aviso institucional de privacidad de matrículas | Texto versionado | Valores heredados hasta el primer guardado institucional | `ingreso.configurar` + plan `academico` |
| Documentos requeridos en matrícula por enlace | Lista por convocatoria, común o por grado | — | `ingreso.configurar` + plan `academico` |
| Vencimiento del enlace privado y PIN de cuatro dígitos | Fecha fija opcional por convocatoria | Sin fecha = sin caducidad por tiempo | `ingreso.configurar` + plan `academico` |
| Cupos de convocatoria por grado | Entero opcional | Sin valor = sin tope propio del enlace | `ingreso.configurar` + plan `academico` |
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

- **[Decisión tomada]** El sistema mantiene un **catálogo base de eventos notificables por módulo** (académico, asistencia, pagos, comunicación, etc.). Cada colegio puede **activar, desactivar o ajustar** qué eventos se notifican y por **qué canales** (correo, push, portal). Regla: **RN-CC-220 — Catálogo base de eventos + matriz canal×evento configurable por colegio**.
- **[Decisión tomada]** **Múltiples recursos de identidad visual por colegio**:
  - Logo principal (header del portal, correos).
  - Logo para documentos oficiales (boletines, certificados, paz y salvo).
  - Isotipo / favicon cuadrado (pestaña del navegador, app).
  Regla: **RN-CC-221 — Identidad visual con tres recursos (principal, oficial, isotipo)**.
