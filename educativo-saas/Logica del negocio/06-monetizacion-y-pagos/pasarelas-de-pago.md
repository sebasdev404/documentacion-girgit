---
titulo: Pasarelas de pago
modulo: monetizacion-y-pagos
tipo: referencia
estado: borrador
tags: [pasarelas, pagos]
---

# Pasarelas de pago

## Pasarelas integradas

El listado exacto se mantiene en la matriz comercial. Como referencia inicial:

| Pasarela | Métodos soportados | País principal |
| --- | --- | --- |
| Wompi | Tarjetas, PSE, Nequi, efectivo. | Colombia. |
| ePayco | Tarjetas, PSE, efectivo. | Colombia. |
| Mercado Pago | Tarjetas, billetera. | LatAm. |
| Stripe | Tarjetas internacionales. | Global / planes corporativos. |

La comisión exacta de cada pasarela se gestiona como parámetro comercial actualizable.

## Selección de pasarela por tenant

- Cada colegio configura una o más pasarelas habilitadas.
- Si hay varias, define la **pasarela primaria** y las **secundarias**.
- En el flujo de pago, el sistema muestra al acudiente las pasarelas disponibles según la configuración del colegio.
- Las credenciales de cada pasarela se almacenan cifradas y son visibles solo a los roles autorizados.

## Webhooks y conciliación

- Cada pasarela envía webhooks al evento de cambio de estado de la transacción.
- La plataforma valida la firma del webhook (HMAC) para evitar suplantación.
- El estado del pago se actualiza solo a partir del webhook autenticado.
- Diariamente se ejecuta una **conciliación automática** cruzando el reporte de la pasarela con los pagos registrados; las diferencias se reportan al colegio.

## Manejo de fallos y reintentos

- Si la pasarela responde error transitorio, la plataforma reintenta con backoff exponencial.
- Si la pasarela queda fuera de servicio prolongadamente, los acudientes pueden seguir viendo sus cuotas pero no pueden iniciar pagos hasta que se restablezca.
- Los webhooks se procesan de forma idempotente: un webhook duplicado no genera doble registro.

## Reembolsos

- Reembolsos solo los inicia el colegio desde la plataforma (con permiso financiero).
- El reembolso se envía a la pasarela y se reconcilia cuando esta confirma.
- Reembolsos parciales: permitidos si la pasarela los soporta.

## Reglas de negocio

- **RN-PA-001 — Webhook firmado:** todo webhook entrante se valida criptográficamente.
- **RN-PA-002 — Idempotencia:** la plataforma no procesa dos veces el mismo `transactionId`.
- **RN-PA-003 — Credenciales cifradas:** las credenciales de pasarela no son visibles en pantalla, solo se ven enmascaradas tras configurarse.
- **RN-PA-004 — Reembolso autorizado:** solo roles con permiso financiero ejecutan reembolsos.
- **RN-PA-005 — Conciliación diaria:** la conciliación automática corre al menos una vez al día.
- **RN-PA-006 — Multi-pasarela transparente:** el cambio de pasarela primaria no afecta los pagos históricos ya conciliados.

## Notas y pendientes

- Definir el SLA esperado de la pasarela y el comportamiento ante caída prolongada.
- Validar comisiones por método (PSE vs tarjeta) según pasarela.
