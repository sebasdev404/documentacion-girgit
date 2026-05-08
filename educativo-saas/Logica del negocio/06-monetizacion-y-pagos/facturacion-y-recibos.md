---
titulo: Facturación y recibos
modulo: monetizacion-y-pagos
tipo: proceso
estado: borrador
tags: [facturacion, recibos]
---

# Facturación y recibos

## Descripción

La plataforma emite los documentos soporte de cada [[pagos-de-pensiones|pago]] confirmado. Para Colombia, el flujo apunta a integración con **facturación electrónica DIAN** vía proveedor tecnológico autorizado.

## Documentos emitidos

| Documento | Cuándo se emite | Destinatario |
| --- | --- | --- |
| Recibo de caja / comprobante de pago | A todo pago confirmado. | Acudiente. |
| Factura electrónica | Cuando el colegio está obligado a facturar y el cliente lo solicita. | Acudiente / empresa pagadora. |
| Cuenta de cobro | Documento previo al pago para emisión hacia empresas. | Empresa o acudiente con esa modalidad. |
| Nota crédito | Al anular o ajustar un documento previo. | Acudiente. |
| Nota débito | Al ajustar al alza un documento previo. | Acudiente. |

## Datos requeridos del pagador y del colegio

- Datos del colegio: NIT / RUT, razón social, dirección fiscal, régimen tributario.
- Datos del pagador: nombre o razón social, identificación, dirección, correo, teléfono.
- Detalle del cobro: conceptos, periodo, valores, impuestos.

Los datos del pagador se capturan durante la matrícula y se reutilizan en cada documento.

## Flujo de emisión

1. Pago confirmado por la pasarela.
2. Sistema genera el documento (recibo / factura) con los datos almacenados.
3. Si aplica facturación electrónica: envía al proveedor tecnológico DIAN.
4. Recibe respuesta (CUFE / acuse) y la asocia al documento.
5. Notifica al pagador con el documento adjunto (PDF / XML).

## Numeración y consecutivos

- El colegio configura sus rangos de numeración autorizados por la DIAN para cada tipo de documento.
- La plataforma respeta el rango y consecutivo, sin duplicados ni saltos no auditados.
- Cada documento queda vinculado a un único pago.

## Notas crédito y anulaciones

- Solo personal con permiso financiero puede emitir notas crédito.
- La nota crédito referencia el documento original y queda en el log.
- La anulación total revierte el estado del cobro a **pendiente** (si todavía se debe) o a **anulado** (si no se debe).

## Integración con DIAN / autoridad fiscal

- En Colombia: integración vía proveedor tecnológico autorizado.
- Soporta envío del XML, recepción del CUFE, almacenamiento de las representaciones gráficas.
- Otros países: el modelo es extensible al esquema fiscal local (México CFDI, Perú SUNAT, etc.) en fases posteriores.

## Reglas de negocio

- **RN-FR-001 — Documento por pago:** todo pago confirmado emite al menos un documento soporte.
- **RN-FR-002 — Numeración consecutiva:** la numeración por tipo de documento es consecutiva, sin saltos.
- **RN-FR-003 — Datos fiscales actualizados:** un cambio en los datos fiscales del pagador no altera documentos ya emitidos; aplica a partir del siguiente documento.
- **RN-FR-004 — Nota crédito referenciada:** una nota crédito siempre referencia el documento original.
- **RN-FR-005 — Inmutabilidad post-emisión:** un documento emitido no se modifica; cualquier ajuste va por nota crédito o nota débito.

## Notas y pendientes

- **[Decisión externa pendiente — Comercial]** Selección del **proveedor tecnológico DIAN** para Colombia. La integración se diseña en abstracto (`FacturadorElectronico` con adaptador por país y por proveedor) para no acoplar la decisión.
- **[Pendiente — producto]** No se ha definido aún el detalle del flujo de **facturación electrónica** (rechazos DIAN, reintentos, corrección manual, notas crédito y débito). Se documenta a profundidad cuando se confirme el proveedor y el segundo país piloto.
