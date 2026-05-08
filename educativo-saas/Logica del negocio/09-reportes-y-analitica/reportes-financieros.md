---
titulo: Reportes financieros
modulo: reportes-y-analitica
tipo: referencia
estado: borrador
tags: [reportes, finanzas]
---

# Reportes financieros

## Catálogo

| Reporte | Audiencia | Frecuencia | Datos incluidos |
| --- | --- | --- | --- |
| Cartera (deudores) | Rector, secretaría, contabilidad. | Diario / mensual. | Estudiantes con deuda, monto, días de mora, contacto. |
| Recaudo | Rector, contabilidad. | Diario / mensual. | Pagos confirmados por concepto, sede, método, pasarela. |
| Estado de cuenta por estudiante | Acudiente, secretaría. | Bajo demanda. | Cuotas generadas, pagos, saldo, mora. |
| Conciliación con pasarelas | Contabilidad, rector. | Diaria. | Transacciones reportadas vs registradas, diferencias. |
| Comisiones de pasarela | Rector, contabilidad. | Mensual. | Comisión descontada por pasarela y por mes. |
| Conceptos cobrados | Contabilidad. | Mensual / anual. | Distribución del recaudo por concepto. |
| Becas y descuentos otorgados | Rector, comité. | Trimestral / anual. | Beneficios vigentes, monto total, distribución. |
| Anulaciones y notas crédito | Rector, contabilidad. | Mensual. | Documentos anulados con motivo y autor. |
| Pagos por pasarela | Contabilidad. | Diaria / mensual. | Detalle por pasarela y método. |
| Acuerdos de pago vigentes | Cartera. | Semanal. | Acuerdos activos, cuotas, cumplimiento. |
| Proyección de ingresos | Rector. | Mensual. | Estimación con base en cronograma de pensiones. |

## Filtros y parámetros disponibles

- Sede / nivel / grado / grupo / estudiante.
- Año lectivo / mes / rango de fechas.
- Concepto (matrícula, pensión, transporte, etc.).
- Pasarela / método de pago.
- Estado del cobro (pendiente, confirmado, en mora, anulado).
- Acudiente.

## Formatos de exportación

- PDF y Excel / CSV.
- Reportes para contabilidad (formato compatible con software contable del colegio).

## Reglas de negocio

- **RN-RF-001 — Acceso restringido:** los reportes financieros completos solo son visibles para roles autorizados (rector, contabilidad).
- **RN-RF-002 — Históricos inmutables:** los reportes de meses cerrados no cambian; cualquier ajuste posterior queda como movimiento del periodo en el que se aplica.
- **RN-RF-003 — Auditoría de exportación:** exportar reportes financieros queda en el log con autor y fecha.
- **RN-RF-004 — Conciliación diaria:** el reporte de conciliación se genera automáticamente cada día.

## Notas y pendientes

- Definir formato exacto del export hacia software contable (Siigo, World Office, etc.).
- Validar si la proyección de ingresos considera escenarios con tasa de mora histórica.
