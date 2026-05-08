---
titulo: Pagos de pensiones
modulo: monetizacion-y-pagos
tipo: proceso
estado: borrador
tags: [pensiones, pagos, padres]
---

# Pagos de pensiones

## Descripción

Flujo por el que los acudientes pagan al colegio a través de la plataforma usando una [[pasarelas-de-pago|pasarela]] integrada. La plataforma genera el cobro, ofrece múltiples medios de pago, concilia con la pasarela y emite el [[facturacion-y-recibos|comprobante]].

## Actores involucrados

- **Acudiente:** paga.
- **Estudiante:** sujeto del cobro.
- **Colegio:** beneficiario del pago.
- **Pasarela de pago:** procesa la transacción.
- **Plataforma SaaS:** orquesta el flujo y registra la trazabilidad.
- **[[roles/05-secretaria-academica|Secretaría Académica]]** o equivalente financiero del colegio: configura conceptos y supervisa cartera.

## Conceptos cobrables

Un concepto es un ítem facturable. La plataforma soporta como mínimo:

| Concepto | Descripción |
| --- | --- |
| Matrícula | Cobro único al inicio del año lectivo. |
| Pensión | Cobro recurrente (mensual típico). |
| Transporte | Cobro recurrente opcional. |
| Alimentación | Cobro recurrente opcional. |
| Uniformes / textos | Cobro único u ocasional. |
| Salidas pedagógicas | Cobros puntuales por evento. |
| Otros conceptos | Conceptos personalizados que el colegio define. |

Cada concepto se configura por colegio: nombre, tipo, frecuencia, valor, IVA / impuestos aplicables.

## Frecuencia y cronograma de cobro

- El colegio define el cronograma anual de pensiones (10 cuotas, 11 cuotas, etc.).
- Cada cuota tiene fecha de generación, fecha de vencimiento ordinaria y fecha de inicio de mora (ver [[politicas-de-cobro-y-mora]]).
- La generación de cuotas puede ser automática o manual según la configuración.

## Generación de cobros

- El sistema genera la cuota del periodo siguiente en lote, por colegio.
- Cada cuota se asocia a un estudiante y a uno o más conceptos.
- Aplica automáticamente los [[descuentos-y-becas|descuentos y becas]] vigentes.
- Genera la notificación al acudiente con la cuota disponible.

## Métodos de pago aceptados

- Tarjeta crédito / débito.
- PSE / transferencia bancaria.
- Botones de pago de pasarelas locales (Wompi, ePayco, Mercado Pago, etc., según el país).
- Pago en efectivo en puntos físicos cuando la pasarela lo soporta.
- Pago manual registrado por el colegio (según permisos).

## Pago manual y registro de comprobantes

Cuando el acudiente paga por fuera de la plataforma (consignación, ventanilla), el colegio puede registrar el pago manualmente:

- Carga el comprobante.
- Asocia el pago a la cuota correspondiente.
- El sistema concilia y marca la cuota como pagada.
- Queda registro auditable de quién hizo la conciliación manual.

## Conciliación con pasarelas

- La plataforma recibe **webhooks** de la pasarela cuando una transacción cambia de estado.
- Cada cuota referencia el `transactionId` de la pasarela.
- Se ejecuta una **conciliación periódica** (diaria) cruzando los reportes de la pasarela con los pagos registrados, alertando al administrador del colegio cuando hay desajustes.

## Estados de un cobro / pago

```
Pendiente → En proceso (al iniciar pago) → Confirmado
                                       → Rechazado → Pendiente
Pendiente → Vencido (al pasar fecha límite) → En mora
Pagado parcial (acuerdo de pago)
Anulado (por nota crédito o ajuste)
```

## Reglas de negocio

- **RN-PP-001 — Trazabilidad de cada pago:** cada pago queda con `transactionId` de la pasarela, método, fecha, IP del pagador y conceptos cubiertos.
- **RN-PP-002 — Aplicación a los conceptos más antiguos:** un pago parcial se aplica primero a las cuotas más antiguas, salvo que el colegio haya configurado otra prelación.
- **RN-PP-003 — Webhook como fuente de verdad:** el estado del pago se actualiza por webhook de la pasarela, no por la confirmación del navegador del usuario.
- **RN-PP-004 — Doble registro prohibido:** un mismo `transactionId` no puede registrarse dos veces.
- **RN-PP-005 — Conciliación manual auditada:** los pagos registrados manualmente requieren rol con permiso financiero y quedan en auditoría con quién los registró.
- **RN-PP-006 — Comprobante automático:** al confirmarse un pago, el sistema emite el [[facturacion-y-recibos|comprobante]] correspondiente.
- **RN-PP-007 — Anulación con motivo:** anular un pago requiere motivo y queda en la auditoría; no borra histórico.

## Notas y pendientes

- Definir si la plataforma soporta cobros compartidos entre dos acudientes (split de pensión).
- Validar el flujo de devolución parcial cuando un estudiante se retira a mitad de mes.
