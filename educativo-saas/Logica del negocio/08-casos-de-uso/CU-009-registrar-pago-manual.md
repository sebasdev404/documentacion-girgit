---
titulo: "CU-009: Registrar pago manual"
modulo: 06-monetizacion-y-pagos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, pago, manual, secretaria]
---

# CU-009: Registrar pago manual

## Identificación

- **ID:** CU-009
- **Nombre:** Registrar pago manual
- **Módulo:** Monetización y pagos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica|Secretaría Académica]] u otro rol con permiso financiero.
- **Secundarios:** Acudiente.

## Descripción

Cuando el acudiente paga por fuera de la plataforma (consignación, ventanilla), el rol financiero registra el pago manualmente, asociándolo a las cuotas correspondientes y subiendo el comprobante.

## Precondiciones

- Existe cuota pendiente.
- El usuario tiene permiso financiero.
- El acudiente envió el comprobante.

## Postcondiciones (éxito)

- Cuota en estado **Confirmado**.
- Soporte almacenado en la carpeta del estudiante.
- Auditoría con autor del registro.

## Flujo principal

1. Secretaría busca al estudiante.
2. Selecciona las cuotas a marcar como pagadas.
3. Llena datos: fecha del pago, método (consignación, transferencia, efectivo), monto, número de soporte.
4. Sube comprobante (PDF / imagen).
5. Confirma. Sistema valida monto y registra el pago.
6. Sistema emite recibo y notifica al acudiente.

## Flujos alternativos

### A1. Conciliación posterior con extracto bancario

- Cuando llega el extracto, secretaría cruza los pagos manuales contra el archivo y marca conciliados.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Monto distinto al cobro. | Sistema permite con confirmación: queda como abono parcial o como pago en exceso para abono futuro. |
| EX-2 | Comprobante infectado. | Sistema rechaza. |
| EX-3 | Pago duplicado (mismo soporte). | Sistema advierte y bloquea. |

## Reglas de negocio aplicables

- RN-PP-005 (auditoría manual), RN-AC-002 (antivirus), RG-002.

## Criterios de aceptación

- [ ] Solo roles con permiso financiero pueden registrar manualmente.
- [ ] El soporte queda asociado al pago en la carpeta del estudiante.
- [ ] El log de auditoría registra quién hizo el registro manual.

## Notas y pendientes

- Validar la regla cuando un pago manual no tiene soporte físico (caso muy excepcional).
