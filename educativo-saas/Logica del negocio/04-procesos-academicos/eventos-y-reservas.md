---
titulo: Eventos y reservas
modulo: procesos-academicos
tipo: proceso
estado: borrador
tags: [eventos, reservas, salidas-pedagogicas, espacios, proceso]
---

# Eventos y reservas

## Descripción

Proceso por el cual el colegio agenda eventos institucionales, programa salidas pedagógicas con autorización firmada del acudiente, reserva espacios físicos evitando doble ocupación, abre cupos y registra la confirmación de asistencia. Un evento puede tener cobro opcional asociado.

Este módulo es la **capa operativa** del evento (autorizaciones, reservas, cupos, cobro). La agenda visual y los tipos de evento viven en [[calendario-escolar|Calendario escolar]]; aquí se gestiona el ciclo de vida completo de cada evento que requiere logística, autorización o cobro.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Administrador]] | Crea y publica eventos institucionales; aprueba salidas pedagógicas y cobros. |
| [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico\|Coordinador Académico]] | Programa salidas pedagógicas y eventos académicos; reserva espacios. |
| [[../02-usuarios-roles-y-permisos/roles/06-docente\|Docente]] | Propone salidas, reserva espacios para actividades de su materia y registra asistencia el día del evento. |
| [[../02-usuarios-roles-y-permisos/roles/07-director-de-grupo\|Director de Grupo]] | Hace seguimiento a las autorizaciones pendientes de su grupo. |
| [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | El estudiante se inscribe o es inscrito; el acudiente autoriza la salida y paga el cobro si aplica. |

## Tipos de evento gestionados

| Tipo | Requiere autorización del acudiente | Requiere reserva de espacio | Permite cobro |
| --- | --- | --- | --- |
| Evento institucional (izadas, semana cultural) | No (salvo configuración del colegio) | Frecuente (auditorio, coliseo) | Opcional |
| Salida pedagógica (excursión, visita técnica) | Sí, siempre | No aplica (es fuera del colegio) | Opcional |
| Reunión / consejo / jornada | No | Sí | No |
| Actividad interna con cupo (taller, torneo) | Configurable | Sí | Opcional |

## Flujo principal

1. El organizador (administrador, coordinador o docente con permiso) crea el evento e indica tipo, alcance (institución, grado, grupo o materia) y fechas.
2. Si el evento ocupa un espacio físico, el sistema verifica disponibilidad contra otras reservas y entradas de [[horarios|horario]]; si hay choque, bloquea la reserva (ver [[espacios-fisicos|Espacios físicos]]).
3. El organizador define cupo máximo (opcional) y, si aplica, el valor del cobro y la fecha límite de pago.
4. El evento se publica y queda en estado **abierto**; el sistema notifica a los destinatarios del alcance (ver [[../05-comunicacion/notificaciones|Notificaciones]]).
5. Si es salida pedagógica, a cada estudiante del alcance se le genera una **solicitud de autorización** dirigida al acudiente.
6. El acudiente abre la autorización en el portal, la lee y la firma electrónicamente (ver firma electrónica `RN-VA-004`); si hay cobro, realiza el pago.
7. El sistema registra la confirmación: estudiante autorizado, autorización firmada y pago conciliado (si aplica) cuentan el cupo.
8. El día del evento, el docente o responsable registra la asistencia real de los inscritos confirmados.

## Flujos alternativos

- **Cupo lleno:** al alcanzarse el cupo máximo, las nuevas inscripciones entran en **lista de espera** y se promueven en orden si se libera un puesto.
- **Acudiente no autoriza:** si la autorización no se firma antes de la fecha límite, el estudiante queda **no autorizado** y no puede participar; el cupo se libera.
- **Cobro no pagado:** si hay cobro y el acudiente no paga antes de la fecha límite, la inscripción se marca **pendiente de pago** y no confirma cupo hasta conciliar.
- **Cancelación del evento:** el organizador cancela; el sistema notifica a los inscritos y, si hubo cobro, marca los pagos para reembolso o nota crédito (ver [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]]).
- **Doble ocupación detectada:** si dos eventos solicitan el mismo espacio en el mismo rango horario, solo el primero confirma; el segundo recibe alerta y debe elegir otro espacio u horario.

## Estados y transiciones

### Evento

```
Borrador → Abierto → Cerrado (cupo lleno o pasó fecha límite) → Realizado
                  → Cancelado
```

### Inscripción del estudiante

```
Inscrito → Pendiente de autorización → Autorizado → Confirmado (cupo) → Asistió
                                     → No autorizado (vence plazo)     → No asistió
        → Lista de espera → Inscrito (si se libera cupo)
```

### Autorización del acudiente

```
Generada → Pendiente → Firmada
                     → Rechazada / Vencida
```

## Configurabilidad por colegio

- Activar o desactivar el módulo de eventos con cobro (un colegio puede usar solo agenda sin cobros).
- Definir si los eventos institucionales internos requieren autorización del acudiente o solo las salidas fuera del colegio.
- Días de anticipación mínima para publicar una salida pedagógica (ej. mínimo 5 días hábiles antes).
- Plazo por defecto para firmar la autorización y para pagar el cobro.
- Medios de pago habilitados para eventos (reusa las pasarelas configuradas en [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]]).
- Política de lista de espera y de reembolso por cancelación.

## Integraciones con otros módulos

- **[[calendario-escolar|Calendario escolar]]:** todo evento publicado aparece en la agenda institucional con su alcance y recordatorios.
- **[[espacios-fisicos|Espacios físicos]]:** la reserva de aula/auditorio reusa la detección de doble ocupación (`RN-EF-002`).
- **Firma electrónica (`RN-VA-004`):** la autorización del acudiente se firma electrónicamente con trazabilidad legal.
- **[[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos]] y [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación]]:** el cobro del evento es un concepto cobrable distinto de la pensión.
- **[[../05-comunicacion/notificaciones|Notificaciones]]:** convocatoria, recordatorios de firma/pago y avisos de cancelación.
- **[[observador-del-estudiante|Observador del estudiante]]:** una novedad relevante durante el evento puede dejar registro en el observador.

## Reglas de negocio

- **RN-EV-001 — Salida exige autorización firmada:** ningún estudiante puede participar en una salida pedagógica sin la autorización del acudiente firmada electrónicamente (`RN-VA-004`) antes de la fecha límite.
- **RN-EV-002 — Reserva sin doble ocupación:** un evento no puede reservar un espacio físico que ya esté ocupado por otra reserva o por una entrada de horario en el mismo rango; el sistema bloquea el choque reutilizando `RN-EF-002`.
- **RN-EV-003 — Cupo confirmado solo con autorización y pago:** un puesto del cupo se cuenta como confirmado únicamente cuando la autorización está firmada y, si hay cobro, el pago está conciliado.
- **RN-EV-004 — Lista de espera por orden de inscripción:** al llenarse el cupo, las nuevas inscripciones entran en lista de espera y se promueven en estricto orden de llegada cuando se libera un puesto.
- **RN-EV-005 — Cobro de evento independiente de la pensión:** el valor de un evento es un concepto cobrable separado; su impago no afecta el estado de pensión ni el paz y salvo académico, salvo configuración explícita del colegio.
- **RN-EV-006 — Anticipación mínima de salidas:** una salida pedagógica solo puede publicarse respetando los días de anticipación mínima configurados por el colegio para dar tiempo a firmar y pagar.
- **RN-EV-007 — Cancelación notificada y con reversa de cobro:** al cancelar un evento con cobro, el sistema notifica a los inscritos y marca los pagos recibidos para reembolso o nota crédito.
- **RN-EV-008 — Asistencia real auditable:** el registro de asistencia al evento queda en el log con responsable, fecha y hora; las ediciones conservan valor anterior y nuevo.
- **RN-EV-009 — Aislamiento por tenant:** eventos, reservas, autorizaciones y cobros pertenecen exclusivamente al colegio (tenant) que los creó y nunca son visibles entre tenants.

## Notas y pendientes

- **[Decisión tomada]** La autorización de salida usa la **firma electrónica** del módulo de valor agregado (`RN-VA-004`) y no firma en papel; el documento firmado se conserva como soporte legal junto al consentimiento de tratamiento de datos del menor (Habeas Data, Ley 1581).
- **[Decisión tomada]** El cobro de eventos es **opcional y configurable por colegio** (`RN-EV-005`): un colegio puede usar el módulo solo para agenda y autorizaciones sin habilitar cobros.
- **[Pendiente — producto]** Definir si la lista de espera promueve automáticamente o requiere confirmación manual del organizador antes de reabrir el cupo (`RN-EV-004`).
- **[Pendiente — producto]** Política de reembolso por cancelación: reembolso total, nota crédito aplicable a otro concepto, o sin reembolso pasada cierta fecha. Validar con colegios piloto.
- **[Funcionalidad futura]** Checklist de seguridad de la salida (cantidad de acompañantes por número de estudiantes, datos del transporte, contacto de emergencia) como requisito para publicar.

## Documentos relacionados

- [[calendario-escolar|Calendario escolar]] — agenda institucional y tipos de evento.
- [[espacios-fisicos|Espacios físicos]] — reserva de aulas y detección de doble ocupación.
- [[horarios|Horarios]] — fuente de ocupación regular de los espacios.
- [[observador-del-estudiante|Observador del estudiante]] — registro de novedades durante el evento.
- [[../05-comunicacion/notificaciones|Notificaciones]] — convocatoria y recordatorios.
- [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]] — cobro y reversa del evento.
- [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]] — medios de pago habilitados.
- [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente|Estudiante y acudiente]] — quién autoriza y paga.
