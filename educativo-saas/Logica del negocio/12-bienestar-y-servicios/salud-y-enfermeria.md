---
titulo: Salud y Enfermería
modulo: bienestar-y-servicios
tipo: proceso
estado: borrador
tags: [salud, enfermeria, bienestar, proceso]
---

# Salud y Enfermería

## Descripción

Servicio de enfermería escolar que centraliza la ficha médica de cada estudiante, registra las atenciones en la enfermería del colegio, controla el suministro de medicamentos autorizado por el acudiente, lleva el control de vacunas y gestiona remisiones a centros médicos. Cada evento de salud relevante notifica automáticamente al acudiente y, cuando corresponde, alimenta el observador del estudiante.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo\|Personal de Apoyo]] (ROL-12) | Registra atenciones, suministra medicamentos autorizados, actualiza la ficha médica y genera remisiones. |
| [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Acudiente]] | Diligencia y mantiene la ficha médica, autoriza el suministro de medicamentos y recibe las notificaciones de salud. |
| [[../02-usuarios-roles-y-permisos/roles/03-coordinador-convivencia\|Coordinador de Convivencia]] | Recibe notificación ante eventos de salud graves de los estudiantes a su cargo. |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Rector]] | Configura el servicio y tiene visibilidad consolidada de los eventos de salud del colegio. |
| [[../02-usuarios-roles-y-permisos/roles/06-docente\|Docente]] / [[../02-usuarios-roles-y-permisos/roles/07-director-de-grupo\|Director de Grupo]] | Reportan al estudiante a enfermería y consultan únicamente alertas de salud marcadas como visibles para docencia (alergias, condiciones críticas). |

## Ficha médica del estudiante

Expediente de salud asociado al estudiante. Lo diligencia el acudiente durante la matrícula y lo mantiene actualizado. Campos principales:

| Campo | Detalle |
| --- | --- |
| EPS / aseguradora | Entidad y número de afiliación (EPS, medicina prepagada o póliza). |
| Tipo de sangre | Grupo y factor RH (ej. O+). |
| Alergias | Alimentarias, medicamentosas y ambientales, con nivel de severidad. |
| Condiciones crónicas | Asma, epilepsia, diabetes, etc., con protocolo de manejo. |
| Medicamentos autorizados | Lista de medicamentos que el acudiente autoriza suministrar en el colegio, con dosis y horario. |
| Contactos de emergencia | Al menos dos contactos con parentesco, teléfono y orden de prioridad. |
| Restricciones | Actividades físicas o alimentarias restringidas. |

La ficha es un dato sensible: su acceso se limita a Personal de Apoyo, enfermería y los roles con permiso explícito. Las alergias y condiciones críticas se exponen como **alerta de salud** a docentes solo cuando el acudiente lo autoriza.

## Flujo principal: atención en enfermería

1. El estudiante llega a la enfermería remitido por un docente o por iniciativa propia.
2. El Personal de Apoyo identifica al estudiante y el sistema carga su ficha médica con las alertas activas (alergias, condiciones crónicas).
3. Registra el motivo de consulta, los signos observados y la atención brindada.
4. Si requiere suministrar un medicamento, verifica que esté en la lista de **medicamentos autorizados** por el acudiente (ver flujo de autorización).
5. Decide la disposición: regreso a clase, reposo en enfermería, llamado al acudiente o remisión a centro médico.
6. Guarda la atención. El sistema dispara la **notificación automática al acudiente** según la severidad del evento.
7. Si el evento es relevante para el seguimiento integral, se genera una entrada en el observador del estudiante con la visibilidad correspondiente.

## Autorización de suministro de medicamentos

1. El acudiente registra en la ficha médica el medicamento, dosis, vía, horario y vigencia de la autorización, adjuntando la fórmula médica cuando aplica.
2. La autorización queda en estado **vigente** hasta su fecha de vencimiento o hasta que el acudiente la revoque.
3. El Personal de Apoyo solo puede suministrar medicamentos con una autorización **vigente**; cada suministro queda registrado (medicamento, dosis, hora, responsable).
4. Sin autorización vigente, el sistema bloquea el registro de suministro y obliga a contactar al acudiente.

## Control de vacunas

- El acudiente carga el esquema de vacunación del estudiante (vacuna, dosis, fecha) y adjunta el carné cuando el colegio lo exige.
- El colegio define un esquema esperado por edad/grado; el sistema marca el estado del estudiante como **al día**, **pendiente** o **sin información**.
- El Personal de Apoyo y secretaría pueden emitir recordatorios a los acudientes con esquema pendiente.

## Remisión a centro médico

1. Ante un evento que excede la capacidad de la enfermería, el Personal de Apoyo genera una **remisión**.
2. Registra el centro de destino, el medio de traslado y el acompañante.
3. La remisión notifica de inmediato al acudiente y al Coordinador de Convivencia, y marca la atención como **remitida**.
4. Al cierre, se registra el desenlace reportado por el acudiente o el centro médico.

## Estados y transiciones

### Atención en enfermería

```
Abierta → En observación → Cerrada
                         → Remitida → Cerrada
```

### Autorización de medicamento

```
Vigente → Vencida
        → Revocada
```

### Estado de vacunación

```
Sin información → Pendiente → Al día
```

## Notificación automática al acudiente

- Todo evento de salud genera una notificación al acudiente a través del módulo de notificaciones (push, correo, WhatsApp según configuración).
- El colegio configura el **umbral de severidad** que dispara notificación inmediata vs. resumen al final de la jornada.
- Los eventos graves (remisión, suministro de medicamento de emergencia, accidente) **siempre** notifican de inmediato e incluyen a un segundo contacto de emergencia si el primero no confirma lectura.

## Configurabilidad por colegio

- Activación del módulo de salud/enfermería (no todos los colegios cuentan con enfermería).
- Campos obligatorios de la ficha médica y exigencia del carné de vacunas.
- Esquema de vacunación esperado por grado.
- Umbral de severidad para notificación inmediata y canales habilitados.
- Qué alertas de salud son visibles para docentes y cuáles permanecen restringidas a enfermería.
- Plantillas de remisión y de consentimiento de suministro de medicamentos.

## Integraciones con otros módulos

- **Observador del estudiante:** los eventos de salud relevantes generan anotaciones con la visibilidad de [[../04-procesos-academicos/observador-del-estudiante\|Observador del estudiante]] (RN-OB-081); por defecto se crean con visibilidad **interna**.
- **Notificaciones:** las alertas al acudiente se emiten vía [[../05-comunicacion/notificaciones\|Notificaciones]].
- **Matrículas:** la ficha médica se inicializa en el proceso de [[../04-procesos-academicos/matriculas\|Matrículas]].
- **Espacios físicos:** la enfermería se modela como un espacio en [[../04-procesos-academicos/espacios-fisicos\|Espacios físicos]] para el reposo del estudiante.
- **Habeas Data:** el tratamiento de datos de salud del menor se rige por los consentimientos del módulo de cumplimiento (Ley 1581).

## Reglas de negocio

- **RN-SA-001 — Ficha médica diligenciada por el acudiente:** la ficha médica es responsabilidad del acudiente, quien la diligencia en matrícula y la mantiene actualizada; el colegio no inventa datos clínicos.
- **RN-SA-002 — Dato sensible con acceso restringido:** la ficha médica es información sensible; solo Personal de Apoyo, enfermería y roles con permiso explícito acceden al detalle clínico, nunca el cuerpo docente completo.
- **RN-SA-003 — Suministro solo con autorización vigente:** no se suministra ningún medicamento sin una autorización vigente del acudiente; sin ella el sistema bloquea el registro y exige contactar al acudiente.
- **RN-SA-004 — Toda atención queda registrada:** cada atención en enfermería genera un registro inmutable con motivo, responsable, fecha/hora y disposición; las correcciones se hacen por anotación, no borrando el original.
- **RN-SA-005 — Notificación automática al acudiente:** todo evento de salud notifica al acudiente; los eventos graves notifican de inmediato y escalan al segundo contacto de emergencia si no hay confirmación de lectura.
- **RN-SA-006 — Remisión escala a convivencia:** una remisión a centro médico notifica simultáneamente al acudiente y al Coordinador de Convivencia, y no puede cerrarse sin registrar el desenlace.
- **RN-SA-007 — Alertas de salud visibles a docentes solo con autorización:** las alergias y condiciones críticas se muestran como alerta a docentes únicamente si el acudiente autoriza esa visibilidad; el resto del detalle clínico permanece restringido.
- **RN-SA-008 — Aporte al observador con visibilidad RN-OB-081:** los eventos de salud que el Personal de Apoyo lleve al observador se crean con los tres niveles de visibilidad de RN-OB-081, por defecto **interna**.
- **RN-SA-009 — Vacunas como control informativo:** el estado de vacunación es informativo y de seguimiento; el colegio decide si la falta de carné condiciona o no la matrícula, según su reglamento.

## Notas y pendientes

- **[Decisión tomada]** Los eventos de salud llevados al observador usan la visibilidad de **RN-OB-081** y se crean por defecto en nivel **interna**, dado el carácter sensible del dato.
- **[Decisión tomada]** El suministro de medicamentos requiere autorización **vigente** del acudiente registrada en la ficha; sin ella el sistema bloquea el registro (RN-SA-003).
- **[Pendiente — producto]** Definir si el colegio puede exigir el carné de vacunas como requisito **bloqueante** de matrícula o solo como recordatorio (hoy RN-SA-009 lo deja informativo).
- **[Pendiente — producto]** Validar con un colegio piloto la matriz de severidad que dispara notificación inmediata vs. resumen de jornada.
- **[Pendiente — producto]** Definir retención y anonimización del histórico clínico tras el egreso del estudiante, alineado con Habeas Data (Ley 1581).

## Documentos relacionados

- [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo|Rol: Personal de Apoyo (ROL-12)]]
- [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente|Rol: Estudiante y Acudiente]]
- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]]
- [[../05-comunicacion/notificaciones|Notificaciones]]
- [[../04-procesos-academicos/matriculas|Matrículas]]
- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]]
- [[bienestar-y-orientacion|Bienestar y orientación escolar]]
