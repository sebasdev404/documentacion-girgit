---
titulo: "CU-010: Emitir paz y salvo"
modulo: 06-monetizacion-y-pagos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, paz-y-salvo, secretaria]
---

# CU-010: Emitir paz y salvo

## Identificación

- **ID:** CU-010
- **Nombre:** Emitir paz y salvo
- **Módulo:** Monetización y pagos / Gestión documental
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** Acudiente / estudiante (solicita); [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica|Secretaría]] (emite o autoriza excepción).
- **Secundarios:** Sistema (validación automática).

## Descripción

Emisión del documento que certifica que un estudiante está al día con sus obligaciones, según los alcances configurados (financiero, documental, material, disciplinario).

## Precondiciones

- Existe el estudiante.
- Los alcances de paz y salvo están configurados.

## Postcondiciones (éxito)

- Paz y salvo PDF emitido y disponible para el solicitante.
- QR de verificación pública.

## Flujo principal

1. Acudiente entra al portal y solicita paz y salvo.
2. Sistema valida automáticamente:
   - Cartera vencida.
   - Documentos faltantes.
   - Materiales no devueltos.
3. Si todo OK → genera el PDF firmado con QR.
4. Si hay pendientes → muestra al solicitante el detalle de lo que debe resolver.
5. Sistema notifica al acudiente y registra emisión en log.

## Flujos alternativos

### A1. Emisión por excepción

- Secretaría / rector puede emitir con pendientes registrando motivo (queda en log).

### A2. Verificación pública

- Un tercero escanea el QR y la página pública confirma la validez del paz y salvo.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Cartera vencida. | Sistema detalla los conceptos pendientes y monto. |
| EX-2 | Documento crítico faltante. | Sistema lista los documentos. |
| EX-3 | Sistema no puede generar PDF. | Reintento; si persiste, alerta a operación. |

## Reglas de negocio aplicables

- RN-PZ-001..006, RG-002, RN-CM-005.

## Criterios de aceptación

- [ ] La emisión normal solo procede si todos los alcances están al día.
- [ ] La excepción registra motivo y autor.
- [ ] El QR permite verificar autenticidad pública.

## Notas y pendientes

- Validar si la emisión automática se dispara al pagar la última cuota.
