---
titulo: Tienda escolar y otros cobros
modulo: bienestar-y-servicios
tipo: proceso
estado: borrador
tags: [tienda, cobros, pagos, proceso]
---

# Tienda escolar y otros cobros

## Descripción

Proceso por el cual el colegio cobra al acudiente conceptos que están **fuera de la pensión** (uniformes, libros y textos, salidas pedagógicas, eventos, certificados, derechos varios). Estos cobros se generan de forma puntual o masiva, se cargan a la **cartera única del estudiante** y se pagan por la misma [[../06-monetizacion-y-pagos/pasarelas-de-pago|pasarela]] que las pensiones.

## Objetivo del proceso

Permitir al colegio facturar y recaudar conceptos ocasionales sin abrir un canal de pago paralelo: todo cobro queda en el mismo estado de cuenta del estudiante, con su trazabilidad, conciliación y comprobante.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica\|Secretaría Académica]] | Crea conceptos cobrables, genera cobros puntuales o masivos y concilia. |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Aprueba conceptos de alto valor y supervisa la cartera consolidada. |
| [[../02-usuarios-roles-y-permisos/roles/06-docente\|Docente]] / Coordinación | Solicita el cobro de una salida pedagógica o evento de su grupo. |
| [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | Visualiza el cargo en el estado de cuenta y paga. |

## Conceptos cobrables fuera de pensión

| Concepto | Naturaleza | Notas |
| --- | --- | --- |
| Uniformes y dotación | Puntual, por catálogo o talla. | El colegio puede manejar inventario o solo el cobro. |
| Libros y textos | Puntual, inicio de año. | Asociable a un grado o área. |
| Salidas pedagógicas | Puntual, por evento. | Suele requerir autorización firmada del acudiente antes de habilitar el cobro. |
| Eventos institucionales | Puntual o masivo. | Grados, izadas de bandera, jornadas culturales. |
| Certificados y constancias | Puntual, a demanda. | Certificado de estudio, paz y salvo con costo, duplicado de carné. |
| Derechos varios | Puntual. | Habilitaciones, nivelaciones, recuperación de material. |
| Otros conceptos | Configurable. | Conceptos personalizados que el colegio define. |

Cada concepto se configura por colegio: nombre, valor base, IVA / impuestos aplicables, si admite cantidad (ej. número de uniformes), grado o grupo al que aplica y si exige autorización previa del acudiente.

## Flujo principal

1. La Secretaría (o el rol con permiso financiero) **crea o selecciona el concepto** cobrable desde el catálogo del colegio.
2. Define el **alcance del cobro**: individual, por grupo, por grado o masivo a toda la institución.
3. El sistema genera un **cargo por cada estudiante** del alcance y lo asocia a su cartera única.
4. Si el concepto exige autorización (ej. salida pedagógica), el cargo queda en estado **pendiente de autorización** hasta que el acudiente la firma.
5. El sistema **notifica al acudiente** el nuevo cargo con su fecha de vencimiento.
6. El acudiente paga por pasarela o el colegio registra un pago manual; el cargo se marca como pagado y se emite el [[../06-monetizacion-y-pagos/facturacion-y-recibos|comprobante]].

## Cobros puntuales vs. masivos

- **Puntual:** un cargo a un solo estudiante (ej. un duplicado de carné, una habilitación).
- **Masivo:** generación en lote a un grupo, grado o toda la institución (ej. salida pedagógica de octavo, libros de primaria). El lote queda identificado para poder anular o ajustar el conjunto.
- En ambos casos el cargo **se suma a la cartera del estudiante**; nunca se cobra por un canal separado.

## Estados y transiciones

### Cargo de otro concepto

```
Borrador → Pendiente de autorización (si aplica) → Pendiente de pago → Pagado
                                                  → Pendiente de pago → Vencido → En mora
Pendiente de pago / Vencido → Anulado (con motivo)
```

- Un cargo solo entra a **Pendiente de pago** cuando, de exigirse, ya tiene la autorización del acudiente.
- El paso a **Vencido / En mora** sigue las mismas fechas y [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|políticas de cobro y mora]] que las pensiones.

## Configurabilidad por colegio

- Catálogo de conceptos propio por tenant; ningún concepto es obligatorio.
- Por concepto: valor, impuestos, si admite cantidad, grado/grupo aplicable y exigencia de autorización.
- Política de mora aplicable a cada concepto (puede diferir de la de pensiones o reusarla).
- Si un certificado o paz y salvo tiene costo o es gratuito.
- Si los conceptos fuera de pensión bloquean o no el [[../06-monetizacion-y-pagos/paz-y-salvo|paz y salvo]] integral.

## Integraciones con otros módulos

- **[[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos]] / cartera única:** los cargos comparten el mismo estado de cuenta y la prelación de pago (`RN-PP-002`).
- **[[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarela de pago]]:** misma integración y conciliación por webhook que las pensiones.
- **[[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]]:** todo cargo pagado emite comprobante o factura electrónica DIAN.
- **[[../06-monetizacion-y-pagos/paz-y-salvo|Paz y salvo]]:** los cargos pendientes pueden contar para el alcance financiero / material.
- **[[../04-procesos-academicos/espacios-fisicos|Espacios físicos]] y eventos:** el cobro de eventos puede originarse en la reserva de un espacio o salida.

## Reglas de negocio

- **RN-TI-001 — Cargo a la cartera única:** todo concepto fuera de pensión se carga a la **cartera única del estudiante**; no existe un canal de cobro paralelo. Hereda la deuda única por estudiante de **RN-PP-120** (sin split entre acudientes ni entre hermanos).
- **RN-TI-002 — Catálogo configurable por colegio:** los conceptos cobrables (valor, IVA, grado/grupo aplicable, autorización requerida) se definen por tenant; ningún concepto viene impuesto por la plataforma.
- **RN-TI-003 — Autorización previa para salidas:** un concepto marcado como "requiere autorización" no entra a estado **Pendiente de pago** hasta que el acudiente firma la autorización del estudiante.
- **RN-TI-004 — Cobro masivo trazable por lote:** un cobro masivo genera un cargo individual por estudiante pero conserva el identificador del lote, para permitir anular o ajustar todo el conjunto en una operación auditada.
- **RN-TI-005 — Mismo flujo de pasarela y conciliación:** los pagos de otros cobros usan la misma pasarela, referencian su `transactionId` y se concilian por webhook, igual que las pensiones (`RN-PP-003`).
- **RN-TI-006 — Comprobante por cargo pagado:** al confirmarse el pago de un concepto, el sistema emite el comprobante o la factura electrónica correspondiente (`RN-FR-001`).
- **RN-TI-007 — Anulación con motivo y sin devolución automática:** anular un cargo exige motivo y queda en auditoría; si ya fue pagado, el sistema deja **saldo a favor** en la cartera y la devolución de dinero se gestiona offline (coherente con `RN-PP-121`).
- **RN-TI-008 — Certificados con cobro condicionan la emisión:** cuando un certificado o constancia tiene costo, el documento solo se entrega una vez confirmado el pago del cargo asociado.
- **RN-TI-009 — Prelación con cuotas más antiguas:** un pago parcial sobre la cartera se aplica primero a los cargos más antiguos (pensión u otros conceptos), salvo otra prelación configurada por el colegio (`RN-PP-002`).

## Notas y pendientes

- **[Decisión tomada]** Los cobros fuera de pensión **no se separan en una cartera aparte**: van a la misma deuda única del estudiante, sin split entre hermanos ni entre acudientes. Regla: **RN-TI-001**, derivada de **RN-PP-120**.
- **[Decisión tomada]** El sistema **no ejecuta devoluciones de dinero** al anular un cargo pagado: deja **saldo a favor** y la devolución se gestiona offline entre colegio y acudiente (alineado con **RN-PP-121**).
- **[Pendiente — producto]** Definir si la **tienda de uniformes** maneja inventario y tallas dentro de la plataforma o solo el cobro; depende de si se documenta el módulo `RN-IV` de inventario y activos.
- **[Pendiente — producto]** Resolver si los conceptos fuera de pensión vencidos **bloquean el paz y salvo integral** por defecto o solo cuando el colegio lo activa.

## Documentos relacionados

- [[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos de pensiones]] — cartera única y prelación de pago.
- [[../06-monetizacion-y-pagos/pasarelas-de-pago|Pasarelas de pago]] — medios de pago y conciliación.
- [[../06-monetizacion-y-pagos/facturacion-y-recibos|Facturación y recibos]] — comprobantes y factura electrónica DIAN.
- [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|Políticas de cobro y mora]] — fechas, recargos e intereses aplicables.
- [[../06-monetizacion-y-pagos/paz-y-salvo|Paz y salvo]] — alcance financiero y material.
- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]] — origen de cobros por eventos y salidas.
- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]] — autorizaciones y seguimiento del acudiente.
