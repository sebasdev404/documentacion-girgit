---
titulo: Modelo de negocio
modulo: monetizacion-y-pagos
tipo: referencia
estado: borrador
tags: [modelo-de-negocio, monetizacion]
---

# Modelo de negocio

La plataforma combina **dos flujos de monetización**:

- **B2B (SaaS):** el colegio paga al proveedor por el uso de la plataforma.
- **B2B2C (intermediación financiera):** la plataforma facilita el cobro de pensiones que los padres pagan al colegio. El proveedor cobra una comisión por transacción.

Ambos flujos son independientes pero se facturan a través del mismo tenant.

## Fuentes de ingreso

| Fuente | Descripción | Tipo |
| --- | --- | --- |
| Suscripción del colegio | Cuota periódica que paga el colegio para usar la plataforma. | Recurrente B2B |
| Comisión por pago de pensión | Porcentaje sobre cada pago de pensión procesado por la plataforma. | Por transacción B2B2C |
| Comisión fija por transacción | Valor fijo cobrado al padre o al colegio por uso de la pasarela. | Por transacción |
| Servicios profesionales | Implementación, capacitación, migración de datos. | Una vez |
| Almacenamiento adicional | Cuotas de almacenamiento por encima del incluido en el plan. | Recurrente |
| Funcionalidades premium | Módulos opcionales (WhatsApp, BI avanzado). | Recurrente |

## Estructura de precios de la suscripción

- Precio **por estudiante activo matriculado**, escalonado por bandas (ej. 0–300, 301–800, 801+).
- Mínimo institucional independiente del número de estudiantes.
- Descuento por contratar el plan anual prepago.
- Periodo de prueba gratuito durante el onboarding (ver [[planes-y-suscripciones]]).

## Comisiones B2B2C

- Porcentaje sobre el valor de cada pago de pensión exitoso.
- Quien asume la comisión (colegio o padre) se configura por colegio.
- En adición, la pasarela cobra su comisión propia (ver [[pasarelas-de-pago]]).
- La comisión se descuenta automáticamente del cierre de cada conciliación.

## Costos variables relevantes

- Comisión de la pasarela de pagos.
- Costo de mensajes WhatsApp / SMS premium.
- Costo de almacenamiento de archivos por encima del cupo.
- Costo de envío de correos transaccionales (proveedor SMTP).

## Unidades económicas

- **MRR / ARR:** ingreso mensual y anual recurrente por suscripciones.
- **GMV:** valor total de pagos de pensión procesados por la plataforma.
- **Take rate:** comisión efectiva sobre GMV.
- **CAC:** costo de adquisición por colegio.
- **LTV:** valor del cliente colegio (suscripciones + comisiones a lo largo del ciclo de vida).
- **Churn de colegios:** % de colegios que cancelan su suscripción.
- **Churn de estudiantes:** % de estudiantes que se desmatriculan dentro de un colegio.

## Reglas de negocio

- **RN-MN-001 — Doble flujo separable:** los ingresos por suscripción y por comisiones se reportan por separado al colegio.
- **RN-MN-002 — Comisiones transparentes:** el desglose de comisiones se muestra al pagador antes de confirmar el pago.
- **RN-MN-003 — Quien asume comisión configurable:** cada colegio define si las comisiones de la pasarela las asume el colegio o el padre.

## Notas y pendientes

- Definir las bandas exactas de precios por estudiante para el go-to-market inicial.
- Validar tope máximo de comisión B2B2C aceptado por colegios pilotos.
