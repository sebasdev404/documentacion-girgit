---
titulo: Biblioteca
modulo: bienestar-y-servicios
tipo: proceso
estado: borrador
tags: [biblioteca, prestamos, multas, proceso]
---

# Biblioteca

## Descripción

Proceso por el cual el colegio gestiona su colección bibliográfica: cataloga material, controla ejemplares físicos, presta y recibe en devolución a estudiantes y docentes, gestiona reservas y vencimientos, y aplica multas configurables por mora que pueden integrarse a la cartera del estudiante.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| Bibliotecario / Personal de apoyo | Cataloga material, registra préstamos y devoluciones, gestiona reservas y aplica multas. Ver [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo\|Personal de Apoyo]]. |
| [[../02-usuarios-roles-y-permisos/roles/06-docente\|Docente]] | Solicita préstamos y reservas; puede tener cupo y plazos diferenciados. |
| [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | El estudiante toma material en préstamo; el acudiente ve multas reflejadas en la cartera. |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Rector / Administrador]] | Configura plazos, multas, cupos y la política de bloqueo por morosidad. |

## Conceptos del modelo

| Concepto | Descripción |
| --- | --- |
| Material (título) | Obra catalogada (libro, revista, audiovisual, material didáctico). Tiene autor, ISBN, categoría/CDU, ubicación. |
| Ejemplar | Copia física e individual de un material. Tiene código de barras propio y un estado (disponible, prestado, reservado, en reparación, dado de baja, extraviado). |
| Préstamo | Vínculo entre un ejemplar y un usuario, con fecha de salida y fecha de vencimiento. |
| Reserva | Solicitud de un usuario sobre un material cuyos ejemplares están todos prestados; se atiende por orden de cola. |
| Multa | Cargo generado por devolución tardía, pérdida o daño del ejemplar. |

## Flujo principal de préstamo

1. El usuario solicita un material en el mostrador o desde el portal (según configuración del colegio).
2. El sistema valida cupo disponible, ausencia de bloqueo por morosidad y disponibilidad de al menos un ejemplar.
3. El bibliotecario (o el portal en autoservicio) registra el préstamo asociando un ejemplar concreto.
4. El sistema calcula la **fecha de vencimiento** = fecha de salida + plazo configurado para el tipo de usuario y tipo de material.
5. El ejemplar pasa a estado `Prestado` y se descuenta del disponible del material.
6. El sistema notifica al usuario la fecha de vencimiento y programa recordatorios.

## Flujo de devolución

1. El usuario entrega el ejemplar; el bibliotecario lo identifica por su código de barras.
2. El sistema marca la devolución y verifica la fecha contra el vencimiento.
3. Si hay retraso, genera una **multa** según la política configurada (valor por día o tarifa fija).
4. Si el ejemplar regresa dañado o no regresa (extravío declarado), aplica la multa de daño/reposición.
5. El ejemplar vuelve a `Disponible`; si tenía reservas en cola, pasa a `Reservado` para el siguiente y se le notifica.

## Flujo de reservas

1. Si todos los ejemplares de un material están prestados, el usuario puede reservarlo.
2. La reserva entra en una **cola por orden de llegada**.
3. Al devolverse un ejemplar, el primero de la cola recibe notificación y dispone de una ventana configurable (ej. 48 horas) para retirarlo.
4. Si no lo retira en la ventana, la reserva caduca y pasa al siguiente de la cola.

## Multas y cartera

- El colegio define el **valor de la multa por mora** (por día de retraso) y los topes máximos.
- Define el **valor de reposición** por pérdida y el cargo por daño.
- Según configuración, la multa puede liquidarse **solo dentro de la biblioteca** (pago en mostrador / paz y salvo interno) o **integrarse a la cartera del estudiante** como un concepto cobrable adicional. Ver [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora\|Políticas de cobro y mora]].
- Cuando se integra a cartera, la multa aparece como concepto en el estado de cuenta del acudiente y puede afectar la emisión del [[../06-monetizacion-y-pagos/paz-y-salvo\|paz y salvo]].

## Bloqueo por morosidad

- El colegio activa o desactiva el **bloqueo de préstamo a usuarios morosos** (configurable por tenant).
- Cuando está activo, un usuario con préstamos vencidos o multas pendientes por encima del umbral configurado **no puede tomar nuevos préstamos** hasta regularizar.
- El umbral (días de mora y/o monto de multa) es configurable por colegio.

## Estados y transiciones

### Ejemplar

```
Disponible → Prestado → Disponible
Disponible → Reservado → Prestado
Prestado → En reparación → Disponible
Prestado → Extraviado (declarado) → Dado de baja
```

### Préstamo

```
Activo → Devuelto a tiempo
Activo → Vencido → Devuelto con multa
Activo → Extraviado (genera multa de reposición)
```

### Reserva

```
En cola → Notificada (turno) → Convertida en préstamo
                             → Caducada (no retiró en la ventana)
```

## Configurabilidad por colegio

| Parámetro | Configurable por colegio |
| --- | --- |
| Plazo de préstamo por tipo de usuario (estudiante / docente) y tipo de material | Sí |
| Cupo máximo de ejemplares simultáneos por usuario | Sí |
| Cantidad de renovaciones permitidas y condiciones | Sí |
| Valor de multa por día de mora, tope y valor de reposición | Sí |
| Integración de multas a la cartera del estudiante | Sí (activable / desactivable) |
| Bloqueo de préstamo por morosidad y su umbral | Sí (activable / desactivable) |
| Ventana de retiro de reservas | Sí |
| Préstamo en autoservicio desde el portal | Sí |

## Inventario de la colección

- La biblioteca conserva el **inventario por ejemplar**: cantidad total, disponibles, prestados, dados de baja y extraviados.
- Permite ejecutar **inventarios periódicos** (conteo físico) que concilian el catálogo contra los ejemplares hallados y registran faltantes.
- Cada baja, reposición o cambio de estado queda en el [[../11-plataforma-y-operacion/log-de-auditoria\|log de auditoría]].

## Datos involucrados

- Material (título, autor, ISBN, categoría/CDU, ubicación).
- Ejemplar (código de barras, estado, material al que pertenece).
- Usuario (estudiante o docente), su cupo y su historial de préstamos.
- Préstamo (ejemplar, usuario, fecha de salida, vencimiento, devolución, renovaciones).
- Reserva (material, usuario, posición en la cola, estado).
- Multa (préstamo asociado, motivo, valor, estado de pago, vínculo a cartera si aplica).

## Reglas de negocio

- **RN-BI-001 — Préstamo sobre ejemplar concreto:** todo préstamo se registra contra un ejemplar identificado por su código de barras, no contra el título genérico, para mantener trazabilidad física.
- **RN-BI-002 — Vencimiento calculado por configuración:** la fecha de vencimiento se calcula como fecha de salida más el plazo configurado por el colegio según tipo de usuario y tipo de material; no se ingresa a mano.
- **RN-BI-003 — Cupo máximo por usuario:** un usuario no puede superar el número máximo de ejemplares simultáneos en préstamo configurado por el colegio.
- **RN-BI-004 — Bloqueo por morosidad configurable:** si el colegio activa el bloqueo, un usuario con préstamos vencidos o multas pendientes sobre el umbral no puede tomar nuevos préstamos hasta regularizar.
- **RN-BI-005 — Multa por mora configurable:** la multa por devolución tardía se liquida según el valor por día y el tope que el colegio define; respeta los topes legales aplicables en Colombia.
- **RN-BI-006 — Integración opcional a cartera:** cuando el colegio lo activa, la multa de biblioteca se incorpora como concepto cobrable en la cartera del estudiante y se refleja en su estado de cuenta.
- **RN-BI-007 — Multa pendiente afecta paz y salvo:** una multa de biblioteca sin pagar puede impedir la emisión del paz y salvo del estudiante cuando la integración a cartera está activa.
- **RN-BI-008 — Reserva por orden de cola:** las reservas se atienden estrictamente por orden de llegada; al devolverse un ejemplar se notifica al primero y la reserva caduca si no retira dentro de la ventana configurada.
- **RN-BI-009 — Ejemplar extraviado genera reposición:** un ejemplar declarado extraviado genera multa de reposición por el valor configurado y se da de baja del inventario disponible.
- **RN-BI-010 — Trazabilidad de movimientos:** préstamos, devoluciones, multas, bajas y conciliaciones de inventario quedan registrados en el log de auditoría con usuario, fecha y valor anterior/nuevo.

## Notas y pendientes

- **[Decisión tomada]** La integración de multas a la cartera del estudiante es **configurable por colegio**: cada tenant decide si las multas de biblioteca se cobran solo en mostrador o se incorporan al estado de cuenta. Regla: **RN-BI-006**.
- **[Decisión tomada]** El bloqueo de préstamo por morosidad es **activable/desactivable por colegio** con umbral propio (días de mora y/o monto). Regla: **RN-BI-004**.
- **[Pendiente — producto]** Definir si el préstamo en autoservicio desde el portal entra en el MVP o se difiere; en el MVP el flujo de mostrador con bibliotecario es el camino principal.
- **[Pendiente — producto]** Validar la importación inicial del catálogo (carga masiva por ISBN / plantilla CSV) frente a captura manual durante el onboarding del colegio.

## Documentos relacionados

- [[../02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo|Personal de Apoyo]] — rol que opera la biblioteca.
- [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente|Estudiante y Acudiente]] — usuario del servicio y vista de multas.
- [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|Políticas de cobro y mora]] — base para la liquidación de multas.
- [[../06-monetizacion-y-pagos/paz-y-salvo|Paz y salvo]] — impacto de multas pendientes.
- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]] — la biblioteca como espacio del colegio.
- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]] — seguimiento de incidencias reiteradas.
- [[../11-plataforma-y-operacion/log-de-auditoria|Log de auditoría]] — registro de movimientos.
- [[../03-multi-tenancy/configuracion-por-colegio|Configuración por colegio]] — parámetros configurables por tenant.
