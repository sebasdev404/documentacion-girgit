---
titulo: Pasarelas de pago externas
modulo: integraciones-externas
tipo: referencia
estado: borrador
tags: [integraciones, pagos]
---

# Pasarelas de pago externas

## Pasarelas integradas

El detalle operativo (métodos, comisiones) se mantiene en [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]] del módulo monetización. Esta página describe la **integración técnica**.

| Pasarela | País | Métodos típicos | Notas |
| --- | --- | --- | --- |
| Wompi | Colombia | Tarjetas, PSE, Nequi, efectivo. | API + webhook. |
| ePayco | Colombia | Tarjetas, PSE, efectivo. | API + webhook. |
| Mercado Pago | LatAm | Tarjetas, billetera. | API + webhook. |
| Stripe | Global | Tarjetas internacionales. | API + webhook. |

La lista exacta es decisión comercial.

## Credenciales y configuración por tenant

- Cada colegio carga sus credenciales de pasarela.
- Se almacenan **cifradas en reposo** y nunca se devuelven al cliente en claro.
- Solo roles con permiso financiero pueden ver una versión enmascarada y rotar credenciales.

## Flujo de cobro

1. La plataforma genera la cuota y un identificador interno.
2. Llama al endpoint de checkout de la pasarela con el monto, identificador y URL de retorno.
3. La pasarela procesa el pago.
4. La plataforma recibe el resultado por:
   - **Webhook** (fuente de verdad).
   - **Redirección del navegador** (UX, pero no se confirma el cobro hasta el webhook).

## Webhooks que consumimos

- `transaction.updated`: cambio de estado de la transacción.
- `refund.created`, `refund.completed`: reembolsos.
- Validación: firma HMAC con secret por colegio.
- Idempotencia: misma `transactionId` no se procesa dos veces.

## Modelos de datos del intercambio

- Petición: monto, moneda, conceptos, identificador interno, URL de retorno, datos del pagador.
- Respuesta: estado, `transactionId` de la pasarela, método, fecha, URL del recibo de la pasarela.
- Webhook: estado nuevo, `transactionId`, monto, fecha, razón del rechazo si aplica.

## Manejo de errores

| Tipo | Acción |
| --- | --- |
| Error transitorio (timeout, 5xx) | Reintento con backoff exponencial, límite máximo. |
| Error de validación | Reportar al colegio y al pagador con mensaje claro. |
| Webhook con firma inválida | Descartar y registrar en el log. |
| Pasarela caída prolongadamente | Bloquear nuevos pagos por esa pasarela y notificar al administrador. |

## Reglas de negocio

- **RN-PE-001 — Webhook firmado:** todo webhook entrante valida firma criptográfica.
- **RN-PE-002 — Idempotencia:** un mismo `transactionId` no genera dos registros.
- **RN-PE-003 — Credenciales cifradas:** las credenciales se almacenan cifradas y se acceden auditadamente.
- **RN-PE-004 — Conciliación diaria:** la conciliación automática corre al menos una vez al día.
- **RN-PE-005 — Multi-pasarela permitida:** un colegio puede tener varias pasarelas activas a la vez.

## Notas y pendientes

- Definir matriz de pruebas de integración para cada pasarela en sandbox.
- Documentar el flujo cuando una transacción queda en estado intermedio durante días (política de timeout).
