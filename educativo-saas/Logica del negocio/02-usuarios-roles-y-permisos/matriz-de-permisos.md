---
titulo: Matriz de permisos
modulo: usuarios-roles-y-permisos
tipo: referencia
estado: borrador
tags: [permisos, autorizacion, matriz]
---

# Matriz de permisos

Tabla rol × acción. Para cada acción del sistema, se indica qué roles pueden ejecutarla.

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
| Citar formalmente a acudientes | — | ✅ | ⚠️ | ⚠️ | ⚠️ | ❌ | ❌ | ⚠️❌ | ❌ |
| Definir sanciones formales | — | ✅ | ❌ | ⚠️ | ⚠️ | ❌ | ❌ | ❌ | ❌ |
| Generar reportes de convivencia | — | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Ver observador disciplinario propio / del estudiante | — | ✅ | ❌ | ✅ | ✅ | ❌ | — | ✅ | ⚠️❌ |

## Matrícula y secretaría

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

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Generar boletín del grupo dirigido | — | ✅ | ✅ | ❌ | ✅ | ❌ | ❌ | ✅ | ❌ |
| Aprobar / firmar boletines | — | ✅ | ⚠️ | ❌ | ⚠️ | ❌ | ❌ | ⚠️ | ❌ |
| Agregar observación general en boletín | — | ✅ | ❌ | ❌ | ❌ | ❌ | ❌ | ✅ | ❌ |
| Consultar boletines propios / del estudiante asociado | — | ✅ | ✅ | ❌ | ✅ | ✅ | — | — | ✅ |
| Descargar boletín en PDF | — | ✅ | ✅ | ❌ | ✅ | ✅ | ❌ | ✅ | ⚠️ |

## Comunicaciones y portal

| Acción | SA | R | CA | CC | CK | SE | DO | DG | EA |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Enviar comunicados al colegio entero | — | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ❌ | ❌ | ❌ |
| Comunicarse con acudientes vía portal | — | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ❌ |
| Recibir notificaciones por correo | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ |
| Acceder al portal | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️✅ |

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
