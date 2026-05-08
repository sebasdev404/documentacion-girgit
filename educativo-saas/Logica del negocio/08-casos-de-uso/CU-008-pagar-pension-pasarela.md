---
titulo: "CU-008: Pagar pensión por pasarela"
modulo: 06-monetizacion-y-pagos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, pago, pasarela, acudiente]
---

# CU-008: Pagar pensión por pasarela

## Identificación

- **ID:** CU-008
- **Nombre:** Pagar pensión por pasarela
- **Módulo:** Monetización y pagos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** Acudiente.
- **Secundarios:** Pasarela de pago, sistema financiero del colegio.

## Descripción

El acudiente paga una o varias cuotas pendientes a través de una de las pasarelas integradas, desde el portal.

## Precondiciones

- Existe cuota generada en estado **Pendiente** o **En mora**.
- El colegio tiene al menos una pasarela activa.

## Postcondiciones (éxito)

- Cuota en estado **Confirmado**.
- Recibo / factura emitida.
- Acudiente recibe notificación de pago confirmado.

## Flujo principal

1. Acudiente entra al portal y va a \"Mis pagos\".
2. Selecciona las cuotas a pagar y la pasarela.
3. Sistema muestra desglose: capital, intereses, recargos, comisiones, total.
4. Acudiente confirma e inicia pago. Sistema crea transacción y redirige a la pasarela.
5. Acudiente paga en la pasarela.
6. Pasarela retorna y envía webhook.
7. Sistema valida firma del webhook y confirma la cuota.
8. Sistema emite recibo / factura y notifica al acudiente.

## Flujos alternativos

### A1. Pago parcial (acuerdo)

- Si el colegio permite abonos, el acudiente puede ingresar un monto menor al total.

### A2. Pago de varias cuotas en una transacción

- Sistema agrupa las cuotas seleccionadas en una sola transacción y aplica el pago en orden.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Pago rechazado por la pasarela. | Cuota vuelve a **Pendiente**, acudiente recibe motivo. |
| EX-2 | Webhook duplicado. | Sistema descarta por idempotencia. |
| EX-3 | Webhook con firma inválida. | Sistema descarta y registra alerta. |
| EX-4 | Pasarela caída. | Sistema bloquea el inicio de nuevos pagos por esa pasarela hasta restablecer. |

## Reglas de negocio aplicables

- RN-PP-001..007, RN-PA-001..006, RN-FR-001..002.

## Criterios de aceptación

- [ ] Solo se confirma el pago al recibir webhook validado.
- [ ] El recibo / factura queda disponible automáticamente.
- [ ] Un mismo `transactionId` no se procesa dos veces.

## Notas y pendientes

- Definir tiempo máximo de espera antes de marcar la transacción como expirada.
