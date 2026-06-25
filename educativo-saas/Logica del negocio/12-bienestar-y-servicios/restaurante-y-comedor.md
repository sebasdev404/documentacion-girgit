---
titulo: Restaurante y comedor escolar
modulo: bienestar-y-servicios
tipo: proceso
estado: borrador
tags: [restaurante, comedor, alimentacion, cobros, proceso]
---

# Restaurante y comedor escolar

## Descripción

Servicio de alimentación escolar (refrigerios y almuerzos) por el cual el colegio define planes alimentarios y menús, controla el consumo diario de cada estudiante y cobra el servicio al acudiente, ya sea por **tiquete** o por **plan mensual** integrado a la cartera única. Las restricciones y alergias alimentarias se heredan de la ficha médica del estudiante, de modo que el menú servido respete cada condición.

## Objetivo del proceso

Permitir que el colegio opere su comedor (propio o concesionado) sin un canal de cobro paralelo y sin papeles: el plan o el tiquete quedan en el mismo estado de cuenta del estudiante, el consumo se controla por estudiante y día, y el menú considera automáticamente las restricciones de salud registradas por el acudiente.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica\|Secretaría Académica]] | Configura planes alimentarios, gestiona inscripciones, genera los cargos y concilia. |
| [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo\|Personal de Apoyo]] (ROL-12) | Opera el comedor: registra el consumo, valida restricciones y atiende incidencias del servicio. |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Activa el servicio, aprueba la operación (propia o concesionada) y supervisa la cartera del comedor. |
| [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | Inscribe al estudiante en un plan o compra tiquetes, declara restricciones y paga. |

## Modalidades de cobro del servicio

| Modalidad | Cómo funciona | A quién conviene |
| --- | --- | --- |
| Tiquete (consumo suelto) | El acudiente compra tiquetes prepagados o cargos por día; cada consumo descuenta un tiquete. | Familias que usan el servicio de forma ocasional. |
| Plan mensual | Inscripción a un plan con cupo de consumos por mes (ej. almuerzo todos los días hábiles); se factura como cargo recurrente a la cartera. | Familias que usan el servicio de forma permanente. |
| Plan por componentes | Combina refrigerio y/o almuerzo en un solo plan configurable por colegio. | Colegios con jornada extendida. |

Cada plan se configura por colegio: nombre, valor, periodicidad de facturación, componentes incluidos (refrigerio, almuerzo), días aplicables y política de mora aplicable.

## Planes alimentarios y menús

- El colegio define uno o varios **planes alimentarios** (qué incluye, valor, días de servicio) y un **menú ciclado** (ej. ciclo de 4 semanas) con la minuta de cada día.
- Cada plato del menú declara sus **componentes y posibles alérgenos** (lácteos, gluten, maní, frutos secos, etc.) para poder cruzarlos con las restricciones del estudiante.
- El colegio puede ofrecer **menús alternativos** (vegetariano, sin gluten, sin lácteos) para cubrir restricciones declaradas.
- El menú del periodo se publica al acudiente como información del servicio.

## Restricciones y alergias (cruce con la ficha médica)

1. Las alergias y restricciones alimentarias **no se capturan en este módulo**: se leen de la ficha médica del estudiante ([[salud-y-enfermeria\|Salud y Enfermería]], `RN-SA`), que diligencia el acudiente.
2. Al inscribir o servir, el sistema cruza las **restricciones vigentes** del estudiante contra los alérgenos del plato del día.
3. Si el plato del día contradice una restricción, el sistema **marca una alerta de incompatibilidad** y propone el menú alternativo disponible o bloquea el servicio de ese plato según la severidad.
4. Una alergia de severidad **alta** (anafilaxia) bloquea el servicio del plato incompatible y exige confirmar el menú alternativo antes de registrar el consumo.

## Flujo principal: inscripción y cobro

1. La Secretaría (o el rol con permiso financiero) **publica los planes** del periodo y abre la inscripción.
2. El acudiente **inscribe al estudiante** en un plan mensual o compra tiquetes; confirma que las restricciones de la ficha médica están actualizadas.
3. El sistema genera el **cargo** correspondiente (mensual recurrente o por tiquetes) y lo asocia a la **cartera única** del estudiante.
4. El sistema notifica al acudiente el nuevo cargo con su fecha de vencimiento.
5. El acudiente paga por pasarela o el colegio registra un pago manual; el cargo se marca como pagado y se emite el [[../06-monetizacion-y-pagos/facturacion-y-recibos\|comprobante]].
6. El plan queda **activo** y habilita el consumo del estudiante durante su vigencia.

## Flujo de consumo en el comedor

1. El estudiante se presenta al comedor; el Personal de Apoyo lo identifica (carné/QR o lista del grupo).
2. El sistema verifica que tenga **plan activo** o **saldo de tiquetes** disponible.
3. El sistema muestra las **restricciones vigentes** del estudiante y el plato/menú alternativo aplicable.
4. Se registra el consumo: descuenta un tiquete o marca el consumo del día contra el cupo del plan.
5. Si no hay plan activo ni saldo, el sistema **deja el consumo en estado pendiente** y notifica al acudiente para regularizar (según la política del colegio: bloquear, fiar o generar cargo automático).

## Estados y transiciones

### Inscripción a plan

```
Borrador → Pendiente de pago → Activo → Vencido (fin de periodo) → Renovado / Cerrado
Pendiente de pago / Activo → Cancelado (con motivo)
```

### Tiquete

```
Comprado (saldo disponible) → Consumido
Comprado → Expirado (si el colegio define vigencia)
```

### Consumo del día

```
Habilitado → Servido
Habilitado → Bloqueado (restricción incompatible / sin saldo)
```

## Configurabilidad por colegio

- Activación del módulo de restaurante/comedor (no todos los colegios lo ofrecen) y si la operación es **propia o concesionada**.
- Catálogo de planes alimentarios: componentes, valor, periodicidad y días de servicio.
- Menú ciclado y declaración de alérgenos por plato; disponibilidad de menús alternativos.
- Modalidad de cobro habilitada: tiquete, plan mensual o ambas.
- Política para consumo sin saldo: bloquear, permitir "fiado" o generar cargo automático a la cartera.
- Vigencia de los tiquetes y política de mora aplicable al servicio.
- Severidad de alergia que bloquea el servicio del plato incompatible.

## Integraciones con otros módulos

- **[[salud-y-enfermeria\|Salud y Enfermería]] (`RN-SA`):** fuente única de las alergias y restricciones alimentarias; este módulo solo las **lee**, nunca las captura.
- **[[../06-monetizacion-y-pagos/pagos-de-pensiones\|Pagos]] / cartera única:** los cargos del comedor van al mismo estado de cuenta del estudiante y respetan la prelación de pago (`RN-PP-002`).
- **[[../06-monetizacion-y-pagos/pasarelas-de-pago\|Pasarela de pago]]:** misma integración y conciliación por webhook que las pensiones.
- **[[../06-monetizacion-y-pagos/facturacion-y-recibos\|Facturación y recibos]]:** todo cargo pagado emite comprobante o factura electrónica DIAN.
- **[[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora\|Políticas de cobro y mora]]:** fechas, recargos e intereses del plan mensual.
- **[[../05-comunicacion/notificaciones\|Notificaciones]]:** publicación del menú, avisos de cargo y alertas de consumo sin saldo al acudiente.
- **[[../04-procesos-academicos/espacios-fisicos\|Espacios físicos]]:** el comedor se modela como espacio para aforo y turnos de servicio.

## Reglas de negocio

- **RN-RE-001 — Cargo del comedor a la cartera única:** todo cobro del servicio de alimentación (plan o tiquete) se carga a la **cartera única del estudiante**; no existe un canal de cobro paralelo. Hereda la deuda única por estudiante de `RN-PP-120` (sin split entre hermanos ni entre acudientes).
- **RN-RE-002 — Restricciones leídas de la ficha médica:** las alergias y restricciones alimentarias se obtienen de la ficha médica (`RN-SA`); el comedor nunca las captura ni edita, solo las consulta como dato vigente.
- **RN-RE-003 — Bloqueo por alergia severa:** un plato cuyos alérgenos contradicen una restricción de severidad alta del estudiante se **bloquea**; el consumo solo se registra tras confirmar el menú alternativo compatible.
- **RN-RE-004 — Consumo solo con plan activo o saldo:** un consumo solo se sirve si el estudiante tiene plan **activo** o **saldo de tiquetes**; sin él, el sistema deja el consumo pendiente y aplica la política de "sin saldo" configurada por el colegio.
- **RN-RE-005 — Planes y menús configurables por colegio:** los planes, valores, componentes, menú ciclado y alérgenos por plato se definen por tenant; ningún plan ni menú viene impuesto por la plataforma.
- **RN-RE-006 — Plan mensual como cargo recurrente:** el plan mensual genera un cargo recurrente a la cartera por periodo; su mora sigue las mismas `RN-PP` / políticas de cobro que las pensiones, salvo política propia del comedor.
- **RN-RE-007 — Tiquete prepagado y trazable:** cada tiquete comprado descuenta exactamente un consumo y deja registro de fecha, hora y responsable del registro; no se puede consumir el mismo tiquete dos veces.
- **RN-RE-008 — Control de consumo inmutable:** cada registro de consumo es inmutable (estudiante, plato/menú, fecha, hora, responsable); las correcciones se hacen por anotación, no borrando el original.
- **RN-RE-009 — Cancelación con motivo y sin devolución automática:** cancelar un plan pagado exige motivo y queda en auditoría; el sistema deja **saldo a favor** en la cartera y la devolución de dinero se gestiona offline (coherente con `RN-PP-121`).
- **RN-RE-010 — Servicio activable y aislado por tenant:** el módulo de comedor se activa por colegio; la operación, los planes, los menús y el consumo son exclusivos del tenant y no se comparten entre colegios.

## Notas y pendientes

- **[Decisión tomada]** Las alergias y restricciones **no se duplican** en el comedor: se leen de la ficha médica (`RN-SA`) como fuente única. Regla: `RN-RE-002`.
- **[Decisión tomada]** Los cobros del comedor **no se separan** en una cartera aparte: van a la misma deuda única del estudiante, sin split. Regla: `RN-RE-001`, derivada de `RN-PP-120`.
- **[Decisión tomada]** El sistema **no ejecuta devoluciones de dinero** al cancelar un plan pagado: deja **saldo a favor** y la devolución se gestiona offline (alineado con `RN-PP-121`). Regla: `RN-RE-009`.
- **[Pendiente — producto]** Definir la política por defecto para **consumo sin saldo**: bloquear, permitir "fiado" con cargo automático o requerir autorización del acudiente; hoy `RN-RE-004` la deja configurable por colegio.
- **[Pendiente — producto]** Resolver si la operación **concesionada** (operador externo) requiere un rol o acceso propio en la plataforma o si todo pasa por Personal de Apoyo.
- **[Pendiente — producto]** Definir si el carné/QR de consumo se integra con el control de acceso (`RN-VA-005`) o es un identificador independiente del comedor.

## Documentos relacionados

- [[salud-y-enfermeria|Salud y Enfermería]] — fuente de alergias y restricciones alimentarias (`RN-SA`).
- [[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos de pensiones]] — cartera única y prelación de pago.
- [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]] — medios de pago y conciliación.
- [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]] — comprobantes y factura electrónica DIAN.
- [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|Políticas de cobro y mora]] — fechas, recargos e intereses aplicables.
- [[tienda-y-otros-cobros|Tienda escolar y otros cobros]] — modelo de cobros fuera de pensión sobre la cartera única.
- [[../05-comunicacion/notificaciones|Notificaciones]] — publicación de menú y avisos de cargo.
- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]] — el comedor como espacio con aforo y turnos.
- [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo|Rol: Personal de Apoyo (ROL-12)]] — operación del comedor.
