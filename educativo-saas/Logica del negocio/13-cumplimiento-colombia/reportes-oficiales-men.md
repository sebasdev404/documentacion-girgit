---
titulo: Reportes oficiales al MEN (SIMAT, DANE, Saber)
modulo: cumplimiento-colombia
tipo: proceso
estado: borrador
tags: [cumplimiento, simat, dane, icfes, men, reportes, proceso]
---

# Reportes oficiales al MEN (SIMAT, DANE, Saber)

## Descripción

Proceso por el cual el colegio extrae de su BD de tenant la información de matrícula y planta de estudiantes para reportarla a las entidades oficiales de Colombia: el **SIMAT** (Sistema Integrado de Matrícula del Ministerio de Educación Nacional), el **DANE** (formulario **C-600** de educación formal) y el **ICFES** (datos de inscripción a pruebas **Saber 3°, 5°, 9° y 11°**). El sistema valida los campos obligatorios oficiales, genera los archivos en el formato exigido por cada entidad y deja trazabilidad de cada exportación.

> El sistema **no se integra en línea** con las plataformas oficiales: produce los archivos en el formato exigido para que el colegio los **cargue manualmente** en SIMAT, en el aplicativo del DANE o en PRISMA del ICFES. La responsabilidad legal del reporte sigue siendo del colegio.

## Objetivo del proceso

Garantizar que el colegio cumpla la obligación legal de reportar matrícula y novedades al MEN de forma oportuna, con datos consistentes y en el formato vigente, evitando rechazos por la entidad y minimizando el trabajo manual de digitación. Cubre la **RR-15 (reporte SIMAT obligatorio)**.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica\|Secretaría Académica]] | Genera, valida y descarga los archivos oficiales; ejecuta la carga en las plataformas del MEN. |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Rector / Administrador del Colegio]] | Configura los códigos oficiales del colegio (DANE, ICFES) y aprueba el reporte antes del cargue. |
| [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma\|Superadministrador de la Plataforma]] | Mantiene actualizadas las plantillas de formato cuando el MEN/DANE/ICFES cambian la estructura del archivo. |
| MEN — SIMAT | Recibe la matrícula y las novedades (ingresos, traslados, retiros). |
| DANE | Recibe el formulario C-600 con las estadísticas de matrícula por grado, edad, sexo y zona. |
| ICFES | Recibe la inscripción de estudiantes a las pruebas Saber. |

## Códigos oficiales del colegio (configuración)

Cada tenant guarda en su configuración los identificadores que el MEN exige. Sin ellos no se puede generar ningún reporte.

| Dato | Uso |
| --- | --- |
| Código DANE de la institución (12 dígitos) | Identifica la institución en SIMAT, C-600 y Saber. |
| Código DANE por sede | Una institución multi-sede reporta cada sede por separado. |
| Código ICFES del establecimiento | Inscripción a pruebas Saber. |
| Calendario (A o B) | Define las ventanas oficiales de reporte. |
| NIT y razón social | Encabezado de los archivos oficiales. |

## Reportes que cubre el módulo

| Reporte | Entidad | Formato de salida | Periodicidad |
| --- | --- | --- | --- |
| Matrícula oficial | MEN — SIMAT | Plantilla de cargue masivo (formato fijo de columnas) | Anual al inicio + novedades durante el año |
| Novedades de matrícula | MEN — SIMAT | Archivo de novedades por tipo (ingreso, traslado, retiro) | Permanente (al ocurrir el hecho) |
| Formulario C-600 | DANE | Archivo C-600 con consolidados estadísticos | Anual (corte oficial) |
| Inscripción a Saber | ICFES | Archivo de inscripción por prueba (3°, 5°, 9°, 11°) | Según calendario ICFES |

## Flujo principal — Reporte de matrícula a SIMAT

1. La Secretaría Académica selecciona el **año lectivo** y la **sede** a reportar.
2. El sistema arma el lote con todos los estudiantes con matrícula `Activa` en ese año y sede.
3. El sistema ejecuta la **validación de campos obligatorios oficiales** (ver tabla de validaciones) sobre cada registro.
4. Si hay registros con errores, el sistema muestra el listado de inconsistencias y **no incluye** esos registros en el archivo hasta que se corrijan en la ficha del estudiante.
5. La Secretaría corrige los datos en el módulo de [[../04-procesos-academicos/matriculas\|Matrículas]] y vuelve a validar.
6. Cuando el lote queda sin errores bloqueantes, el sistema genera el **archivo de cargue** en el formato de columnas exigido por SIMAT.
7. El Rector revisa y **aprueba** el reporte.
8. La Secretaría descarga el archivo y lo **carga en la plataforma SIMAT**.
9. La Secretaría registra en el sistema la **constancia del cargue** (fecha, usuario, resultado), que queda en el log de auditoría.

## Flujo de novedades (ingresos, traslados, retiros)

Las novedades nacen de hechos que ya ocurren en otros módulos; el sistema las traduce al formato de novedad SIMAT.

| Novedad | Origen en el sistema | Dato clave para SIMAT |
| --- | --- | --- |
| Ingreso (matrícula nueva) | Cierre exitoso del proceso de [[../04-procesos-academicos/matriculas\|Matrículas]]. | Fecha de matrícula, grado, grupo. |
| Traslado de salida | Retiro con motivo "traslado a otra institución". | Fecha y motivo; el estudiante queda disponible para que la otra IE lo "jale" en SIMAT. |
| Traslado de entrada | Matrícula de un estudiante que viene de otra IE. | Documento de identidad; debe existir previamente en SIMAT. |
| Retiro / deserción | Cambio de estado de matrícula a `Retirada`. | Fecha y motivo del retiro. |
| Promoción / repitencia | Resultado de [[../04-procesos-academicos/promocion-y-reprobacion\|Promoción y reprobación]] al cierre del año. | Grado del año siguiente. |

1. El sistema detecta el hecho (ej. retiro registrado en Matrículas).
2. Genera una **novedad pendiente de reporte** con el tipo correspondiente.
3. La novedad se acumula en una bandeja para que la Secretaría la incluya en el siguiente cargue de novedades a SIMAT.
4. Tras el cargue, la novedad pasa a `Reportada` y queda asociada a la constancia del cargue.

## Flujo del formulario C-600 (DANE)

1. La Secretaría selecciona el año y la fecha de corte oficial del DANE.
2. El sistema **consolida** la matrícula activa a esa fecha por: grado, **edad cumplida**, sexo, zona (urbana/rural), jornada y modelo educativo.
3. Calcula además los conteos que pide el C-600 (repitentes, estudiantes con discapacidad reportada, grupos étnicos, etc.) a partir de los campos de la ficha.
4. Genera el archivo C-600 en el formato vigente.
5. La Secretaría descarga y carga el archivo en el aplicativo del DANE.

## Flujo de inscripción a pruebas Saber (ICFES)

1. La Secretaría selecciona la prueba (Saber 3°, 5°, 9° u 11°) y el periodo de inscripción.
2. El sistema arma el listado de estudiantes de los grados objetivo con matrícula activa.
3. Valida que cada estudiante tenga **tipo y número de documento** y **fecha de nacimiento** válidos (campos exigidos por el ICFES).
4. Genera el archivo de inscripción con el **código ICFES del establecimiento**.
5. La Secretaría lo carga en PRISMA y registra la constancia.

## Validación de campos obligatorios oficiales

Antes de generar cualquier archivo, el sistema valida (regla **RN-MO-002**). Campos típicos que bloquean el reporte:

| Campo | Regla |
| --- | --- |
| Tipo de documento | Debe ser un valor del catálogo oficial (RC, TI, CC, CE, PEP, PPT, NES…). |
| Número de documento | Obligatorio y único dentro del tenant. |
| Nombres y apellidos | No vacíos. |
| Fecha de nacimiento | Válida y coherente con el grado (alerta, no siempre bloqueo). |
| Sexo | Valor del catálogo oficial. |
| Grado | Mapeado al código de grado del MEN (-2 a 13, ciclos de adultos). |
| Dirección y municipio (DIVIPOLA) | Municipio del catálogo DANE. |
| EPS / régimen de salud | Requerido en C-600. |

## Estados y transiciones

### Lote de reporte

```
Borrador -> En validación -> Validado -> Aprobado -> Cargado -> Archivado
                  |
            Con errores (vuelve a Borrador tras corrección)
```

### Novedad de matrícula

```
Pendiente de reporte -> Incluida en lote -> Reportada
                                         -> Rechazada (vuelve a Pendiente)
```

## Configurabilidad por colegio

- **Multi-sede:** un tenant con varias sedes genera un archivo por **código DANE de sede**; la consolidación nunca mezcla sedes.
- **Calendario A o B:** define qué ventanas de reporte aplican; el sistema avisa cuando se acerca el corte según el calendario del colegio.
- **Mapeo de grados:** cada colegio confirma el mapeo entre sus grados internos y los **códigos de grado del MEN** (configurable, con valores por defecto).
- **Campos extendidos opcionales:** un colegio puede capturar campos adicionales (grupo étnico, discapacidad, víctima del conflicto) si los reporta; si no los usa, no se exigen.

## Integraciones con otros módulos

- [[../04-procesos-academicos/matriculas\|Matrículas]] — fuente de los ingresos, retiros y traslados.
- [[../04-procesos-academicos/promocion-y-reprobacion\|Promoción y reprobación]] — fuente de la novedad de promoción/repitencia al cierre del año.
- [[../03-multi-tenancy/configuracion-por-colegio\|Configuración por colegio]] — guarda los códigos oficiales (DANE, ICFES, calendario).
- [[../11-plataforma-y-operacion/log-de-auditoria\|Log de auditoría]] — registra cada generación y cargue como evento inmutable.
- [[../13-cumplimiento-colombia/habeas-data-y-consentimientos\|Habeas Data y consentimientos]] — el envío de datos del menor a entidades oficiales se ampara en la base legal de cumplimiento de obligación legal.

## Reglas de negocio

- **RN-MO-001 — SIMAT obligatorio (RR-15):** todo colegio activo en la plataforma debe poder generar el archivo de matrícula SIMAT del año en curso; el sistema bloquea el cierre del proceso de matrícula anual si no existe al menos un reporte SIMAT generado y con constancia de cargue.
- **RN-MO-002 — Validación previa bloqueante:** ningún registro con un campo obligatorio oficial vacío o fuera del catálogo entra al archivo; el sistema lista las inconsistencias y exige corregirlas en la ficha del estudiante.
- **RN-MO-003 — Catálogos oficiales versionados:** tipo de documento, grado MEN, sexo y municipio (DIVIPOLA) se validan contra catálogos oficiales versionados que mantiene el Superadministrador; un colegio no puede inventar valores.
- **RN-MO-004 — Novedad por cada hecho:** todo ingreso, traslado o retiro de matrícula genera automáticamente una novedad pendiente de reporte; no se permite cerrar un retiro sin clasificar su motivo (traslado vs deserción).
- **RN-MO-005 — Reporte por sede:** en colegios multi-sede el archivo se segmenta por código DANE de sede; queda prohibido consolidar dos sedes en un mismo archivo oficial.
- **RN-MO-006 — Aprobación del Rector antes del cargue:** el archivo oficial solo se habilita para descarga tras la aprobación explícita del Rector (o Administrador del Colegio); la aprobación queda firmada en el log.
- **RN-MO-007 — Trazabilidad del cargue:** cada generación y cada cargue registran fecha, usuario, sede, conteo de registros y resultado en el log de auditoría inmutable.
- **RN-MO-008 — Edad de corte para C-600:** el C-600 calcula la edad a la **fecha de corte oficial del DANE**, no a la fecha de generación del archivo, para evitar desfases en los consolidados por edad.
- **RN-MO-009 — Aislamiento por tenant:** los datos exportados pertenecen a un único tenant; un colegio nunca ve ni reporta estudiantes de otro, aunque compartan municipio o código DANE de municipio.
- **RN-MO-010 — Formato vigente del MEN:** el sistema genera siempre la versión del formato vigente; si la entidad cambia la estructura, el reporte se bloquea hasta que el Superadministrador publique la plantilla actualizada.

## Notas y pendientes

- **[Decisión tomada]** El alcance del MVP es **generar archivos en el formato oficial para cargue manual**, no integración API en línea con SIMAT/DANE/ICFES. El MEN no expone APIs públicas estables, así que la integración directa queda fuera de alcance.
- **[Decisión tomada]** Los catálogos oficiales (tipos de documento, grados MEN, DIVIPOLA) son **globales de la plataforma** y los versiona el Superadministrador; no son editables por el colegio. Regla: **RN-MO-003**.
- **[Pendiente — producto]** Definir si el sistema debe **importar** el reporte de retorno de SIMAT (archivo de respuesta con errores de cargue) para conciliar automáticamente las novedades rechazadas, o si la conciliación se hace manual en el MVP.
- **[Pendiente — producto]** Confirmar el alcance de los campos de **discapacidad, grupo étnico y población víctima** exigidos por el DANE/SIMAT: si entran como campos obligatorios de la ficha o como módulo configurable por colegio según su población.
- **[Pendiente — producto]** Validar con un colegio piloto de **calendario B** las ventanas de reporte, ya que difieren de las de calendario A.

## Documentos relacionados

- [[../04-procesos-academicos/matriculas|Matrículas]]
- [[../04-procesos-academicos/promocion-y-reprobacion|Promoción y reprobación]]
- [[../13-cumplimiento-colombia/habeas-data-y-consentimientos|Habeas Data y consentimientos]]
- [[../03-multi-tenancy/configuracion-por-colegio|Configuración por colegio]]
- [[../03-multi-tenancy/aislamiento-de-datos|Aislamiento de datos]]
- [[../11-plataforma-y-operacion/log-de-auditoria|Log de auditoría]]
- [[../09-reportes-y-analitica/reportes-academicos|Reportes académicos]]
- [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica|Secretaría Académica]]
- [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rector / Administrador del Colegio]]
