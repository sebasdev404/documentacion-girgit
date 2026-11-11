---
titulo: Matriz de permisos
modulo: usuarios-roles-y-permisos
tipo: referencia
estado: borrador
tags: [permisos, autorizacion, matriz]
---

# Matriz de permisos

Tabla rol × acción. Para cada acción del sistema, se indica qué roles pueden ejecutarla.

Los permisos para corregir matrículas confirmadas, reconocer resultados anteriores e incorporar resultados en periodos cerrados se proponen en el [plan de novedades académicas](../04-procesos-academicos/plan-novedades-academicas-y-reconocimiento-de-resultados-2026-11-11.md). Su asignación y sus claves operativas están pendientes de revisión e incorporación al catálogo.

## Convenciones

- ✅ Permitido (estructural — el colegio no lo puede desactivar)
- ⚠️ Configurable (default sugerido entre paréntesis: ⚠️✅ activado por defecto, ⚠️❌ desactivado por defecto)
- ❌ No permitido (nunca, sin importar configuración)
- — No aplica al ámbito del rol

Abreviaturas de columna:
- **SA** = Superadministrador de la Plataforma
- **R** = Rector / Administrador del Colegio
- **CA** = Coordinador Académico
- **CC** = Coordinador de Convivencia
- **CK** = Coordinador combinado (académico + convivencia)
- **SE** = Secretaría Académica
- **DO** = Docente
- **DG** = Director de Grupo (complemento sobre Docente)
- **EA** = Estudiante (cuenta del estudiante; el acudiente la opera de hecho según `RN-TU-410`)

> Para los detalles de cada permiso ver el archivo del rol correspondiente en [[roles/|`roles/`]].

---

## Plataforma (cross-tenant)

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Crear / eliminar tenant | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Asignar plan de licencia al tenant | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Cambiar calendario A ↔ B del tenant | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Definir subdominio del tenant | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Gestionar almacenamiento del tenant | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Acceso cross-tenant para soporte (auditado) | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Acceder a logs globales de plataforma | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |

## Configuración del colegio (tenant)

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Configurar identidad institucional (logo, NIT, MEN) | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Definir períodos lectivos | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Configurar jornadas y bloques horarios | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Configurar modelo pedagógico por nivel | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Configurar escala valorativa | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Configurar método de aprobación y nota mínima | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Crear / editar / desactivar usuarios del tenant | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Asignar roles a usuarios | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Ajustar permisos configurables de los roles | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |

## Plan académico y horarios

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Gestionar plan de estudios (materias por grado) | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Crear / gestionar grupos por grado y año lectivo | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Asignar docentes a materias y grupos | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Designar director de grupo | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Construir / editar horarios de clase | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Consultar horario propio | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

## Notas y consolidados

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Registrar / editar notas en materia y grupo asignado | — | ✅ | ⚠️ | ❌ | ⚠️ | ❌ | ✅ | ✅ | ❌ |
| Editar notas de materias que no dicta | — | ✅ | ⚠️ | ❌ | ⚠️ | ❌ | ❌ | ⚠️❌ | ❌ |
| Editar notas después del cierre de período | — | ✅ | ⚠️ | ❌ | ⚠️ | ❌ | ⚠️❌ | ⚠️❌ | ❌ |
| Ver consolidado completo de notas del grupo | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ✅ | ❌ |
| Ver consolidados de todos los grupos | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Ver notas propias / del estudiante asociado | — | ✅ | ✅ | ❌ | ✅ | ⚠️✅ | — | — | ✅ |
| Coordinar cierre de período académico | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Gestionar nivelaciones / habilitaciones | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ❌ | ❌ |

## Asistencia

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Registrar asistencia en sus clases | — | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ❌ |
| Consultar asistencia del grupo dirigido | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ✅ | ❌ |
| Consultar asistencia propia / del estudiante asociado | — | ✅ | ✅ | ✅ | ✅ | ✅ | — | — | ✅ |

## Convivencia y observador

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Registrar observación académica en su materia | — | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ❌ |
| Registrar anotación en el observador del grupo dirigido | — | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ | ✅ | ❌ |
| Registrar anotaciones en el observador (cualquier estudiante) | — | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Definir tipologías de anotación | — | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Definir sanciones formales | — | ✅ | ❌ | ⚠️ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| Generar reportes de convivencia | — | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Ver observador disciplinario propio / del estudiante | — | ✅ | ❌ | ✅ | ✅ | ❌ | — | ✅ | ⚠️❌ |

## Matrícula y secretaría

### Ingreso estudiantil por enlace — implementado localmente, 2026-10-07

Capacidad de plan `academico`. Consulta (`ingreso.ver`) es adicionalmente obligatoria para revisar, decidir, cambiar grado y asignar. Rector estructural; delegaciones configurables inicialmente OFF. El portal público usa enlace privado/desafío HttpOnly + PIN de cuatro dígitos del solicitante, no un rol de estudiante/acudiente. No se crean cuentas de acudiente.

| Permiso / acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `ingreso.configurar`: política institucional de matrículas, convocatorias y requisitos | — | ✅ | ❌ | ❌ | ❌ | ⚠️❌ | ❌ | ❌ | ❌ |
| `ingreso.ver`: solicitudes y archivos privados | — | ✅ | ⚠️❌ | ❌ | ⚠️❌ | ⚠️❌ | ❌ | ❌ | ❌ |
| `ingreso.revisar`: aprobar/rechazar documentos | — | ✅ | ❌ | ❌ | ❌ | ⚠️❌ | ❌ | ❌ | ❌ |
| `ingreso.decidir`: aprobar/rechazar/espera/correcciones | — | ✅ | ❌ | ❌ | ❌ | ⚠️❌ | ❌ | ❌ | ❌ |
| `ingreso.cambiar_grado`: proponer/aprobar otro grado con motivo | — | ✅ | ❌ | ❌ | ❌ | ⚠️❌ | ❌ | ❌ | ❌ |
| `ingreso.asignar`: grupos y matrícula académica | — | ✅ | ⚠️❌ | ❌ | ⚠️❌ | ⚠️❌ | ❌ | ❌ | ❌ |

**Política aceptada el 14 de octubre de 2026:** `ingreso.configurar` habilita **Ajustes institucionales > Configuración de matrículas** y su acceso directo desde **Matrículas por enlace**, con los mismos controles de permiso y plan. Incluye rangos permanentes por grado, aviso institucional versionado y resolución de valores heredados en el mismo formulario. Secretaría puede recibir la delegación; no se exige rol rector adicional. Fuente canónica: [[../04-procesos-academicos/matriculas|Matrículas por enlace]], RN-MA-018 a RN-MA-021.

**Salida institucional (15 de octubre de 2026):** `estudiantes.egreso.gestionar` autoriza listar candidatos estudiantes y marcar manualmente el egreso. Por defecto lo usa solo el superadministrador suplantando al colegio; rector, secretaría y coordinaciones académicas pueden recibirlo mediante las celdas configurables de la matriz, inicialmente apagadas. No habilita borrar el usuario ni cambiar el resultado académico. La cuenta egresada pierde acceso y conserva su historial. La renovación del siguiente año, usando el mismo usuario y el grado destino, es un proceso separado aún pendiente.

**Correo institucional:** `config.correo` es estructural del rector y denegado para los demás roles del tenant. Además de ese permiso se verifica el rol rector explícitamente; delegarlo no habilita acceso. Permite primera configuración y solicitar cambios, **no editar libremente una conexión guardada**. Editar/desconectar exige aprobación del superadministrador central, de un uso y 24 horas, ligada a rector/colegio/acción/versión. No existe permiso delegable para aprobar. La suplantación no permite aprobar ni evita este bloqueo. No es acceso a buzones o documentos; incluido en configuración básica sin gate adicional.

### Matriz académica/documental histórica

La tabla siguiente mezcla funciones existentes y futuras de secretaría. No concede los permisos nuevos de ingreso ni implica implementación de acudientes, SIMAT o certificados en esta entrega. La matrícula académica manual conserva su permiso anterior.

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Registrar / editar estudiantes y datos de acudiente operativo | — | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| Asignar estudiante a grupo (matrícula) | — | ✅ | ⚠️ | ❌ | ⚠️ | ✅ | ❌ | ❌ | ❌ |
| Cambiar grupo de un estudiante después de matriculado | — | ✅ | ⚠️ | ❌ | ⚠️ | ⚠️ | ❌ | ❌ | ❌ |
| Cargar y validar documentos de matrícula | — | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| Generar constancias de estudio | — | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| Generar certificados de notas | — | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| Generar paz y salvos | — | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| Reportar a SIMAT | — | ✅ | ❌ | ❌ | ❌ | ✅ | ❌ | ❌ | ❌ |
| Bloquear documentos por pendientes | — | ✅ | ❌ | ❌ | ❌ | ⚠️✅ | ❌ | ❌ | ❌ |

## Boletines

> En desarrollo local existe emisión individual con PDF privado y publicación separada, pero no firma digital certificada. Aprobar una observación **no** aprueba el boletín. La consulta docente del boletín completo es de solo lectura y exige grupo asignado; no permite emitir ni ver expedientes sin publicar. Las claves operativas siguientes prevalecen sobre cualquier objetivo histórico.

| Clave operativa | R | CA | CK | SE | DO | DG | EA | Estado |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `boletines.politica.gestionar` | ✅ | ⚠️❌ | ⚠️❌ | ❌ | ❌ | ❌ | ❌ | API/UI local |
| `boletines.observaciones.gestionar` | ✅ | ⚠️❌ | ⚠️❌ | ⚠️❌ | ❌ | ❌ | ❌ | API/UI local; la interfaz actual se alcanza desde la vista preliminar autorizada |
| `boletines.observaciones.aprobar` | ✅ | ⚠️❌ | ⚠️❌ | ❌ | ❌ | ❌ | ❌ | Solo aprueba el texto; no emite documento |
| `indicadores.configurar` | ✅ | ⚠️❌ | ⚠️❌ | ⚠️❌ | ❌ | ❌ | ❌ | Elegir alcance anual grado/grupo y habilitar edición docente; sujeto al plan académico |
| `indicadores.base.gestionar` | ✅ | ⚠️❌ | ⚠️❌ | ⚠️❌ | ❌ | ❌ | ❌ | Gestionar todos los indicadores del alcance configurado |
| `indicadores.grupo.ver` | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ❌ | Lectura de indicadores únicamente de la materia y grupo asignados |
| `indicadores.grupo.editar` | ✅ | ⚠️❌ | ⚠️❌ | ❌ | ⚠️❌ | ⚠️❌ | ❌ | Crear y editar en modo grupo, solo para materia y grupo realmente asignados; dirigir el grupo no habilita otras materias. Requiere política anual activa. |
| `boletines.grupo.ver` | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ❌ | Boletín preliminar completo del grupo con asignación docente o dirección vigente; emisión publicada visible, sin diseño ni preparación |
| `boletines.emisiones.ver` | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | Expediente de emisiones, incluidas no publicadas |
| `boletines.emisiones.preparar/aprobar/publicar` | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | Operaciones independientes; no se heredan de los permisos de lectura |

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Preparar, aprobar y publicar boletín | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Consultar boletín completo preliminar autorizado | — | ✅ | ✅ | ❌ | ✅ | ❌ | ✅ | ✅ | ✅ |
| Agregar observación general en boletín | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ |
| Consultar boletines propios / del estudiante asociado | — | ✅ | ✅ | ❌ | ✅ | ✅ | — | — | ✅ |
| Descargar PDF ya publicado del grupo asignado o propio | — | ✅ | ❌ | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |

## Comunicaciones y portal

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Enviar comunicados al colegio entero | — | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ❌ | ❌ | ❌ |
| Recibir notificaciones por correo | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| Acceder al portal | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️✅ |

La app o portal independiente de acudientes no forma parte de los planes ni de esta matriz. Las claves antiguas `mensajes.acudientes` y `convivencia.citar_acudientes` se retiran. Los datos de contacto familiares permanecen en la ficha del estudiante; el acceso familiar a la información se realiza mediante la cuenta del estudiante, sin rol propio.

## Auditoría

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Acceder a logs de auditoría del tenant | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ | ❌ |
| Ver historial de cambios de un registro | — | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ❌ | ❌ | ❌ |

---

## Reglas que aplican a esta matriz

Las reglas transversales (verificación frontend+backend, auditoría, aislamiento por tenant, etc.) están en [[reglas-transversales-de-roles|Reglas transversales de roles]].

## Notas y pendientes

- **[Cubierto]** Sección de Pagos / Cartera: ya documentada en módulo `06-monetizacion-y-pagos` con sus reglas `RN-PP-*`, `RN-PG-*`, `RN-PCM-*`, `RN-PYS-*` y reglas de plan `RN-PS-*`.
- **[Cubierto]** Sección de Comunicaciones: el modelo quedó definido como **estructurado, sin chat libre** (ver `RN-MI-180`); ya no hay decisión pendiente de "1 a 1 / grupal / ambas".
- **[Decisión tomada]** **Director de Grupo**: por defecto **no puede modificar notas de materias que no dicta**. Cada colegio puede activar la capacidad bajo **autorización y responsabilidad administrativa**, manteniendo **auditoría completa** sobre cualquier modificación. Regla: **RN-MP-380 — Director de Grupo: edición cross-materia opt-in con auditoría obligatoria**.
