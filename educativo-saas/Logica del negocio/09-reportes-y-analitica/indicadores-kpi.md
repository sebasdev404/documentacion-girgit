---
titulo: Indicadores KPI
modulo: reportes-y-analitica
tipo: referencia
estado: borrador
tags: [kpi, indicadores, metricas]
---

# Indicadores KPI

## KPIs del SaaS (visión interna)

Visibles solo para el equipo de la plataforma.

| KPI | Descripción | Cálculo | Frecuencia |
| --- | --- | --- | --- |
| MRR | Ingreso mensual recurrente por suscripciones de colegios. | Σ (cuota mensual normalizada de cada tenant activo). | Mensual. |
| ARR | Ingreso anual recurrente. | MRR * 12. | Mensual. |
| GMV | Volumen total de pagos de pensión procesados por la plataforma. | Σ (pagos confirmados B2B2C). | Mensual. |
| Take rate | Comisión efectiva sobre GMV. | (Comisión cobrada / GMV) * 100. | Mensual. |
| Churn de colegios | Colegios que cancelan en el mes. | (Cancelaciones / tenants activos al inicio del mes) * 100. | Mensual. |
| Churn de estudiantes | Estudiantes que se desmatriculan dentro de un colegio. | Por colegio: (retiros / matriculados al inicio del periodo) * 100. | Trimestral. |
| LTV | Valor del cliente colegio durante su ciclo de vida. | (Ingreso medio mensual por colegio * margen) / churn. | Trimestral. |
| CAC | Costo de adquisición por colegio. | (Inversión en marketing y ventas / colegios nuevos del periodo). | Trimestral. |
| Tenants activos | Número de colegios con suscripción activa. | Conteo. | Diario. |
| Tenants en trial | Número de colegios en periodo de prueba. | Conteo. | Diario. |
| Tasa de conversión trial → activo | Trials que pasan a suscripción. | (Trials convertidos / trials iniciados) * 100. | Mensual. |
| Tickets de soporte | Número y SLA. | Por colegio y por mes. | Mensual. |

## KPIs del colegio (visión cliente)

Visibles para el rector y roles autorizados de cada colegio, restringidos a su tenant.

| KPI | Descripción | Cálculo | Frecuencia |
| --- | --- | --- | --- |
| % asistencia | Tasa global de asistencia. | (Sesiones presentes / sesiones totales) * 100. | Diaria. |
| % asistencia por grupo | Tasa por grupo. | Análogo, filtrado. | Diaria. |
| % aprobación por área | Estudiantes que aprueban un área. | (Estudiantes aprobados / total) * 100. | Por periodo y final. |
| % aprobación general | Estudiantes que aprueban el grado. | Análogo. | Final del año. |
| % cartera al día | Estudiantes sin deuda vencida. | (Estudiantes al día / total) * 100. | Diario. |
| Recaudo del mes vs proyección | Cumplimiento del recaudo. | (Recaudado / proyectado) * 100. | Mensual. |
| Tasa de retención de estudiantes | Estudiantes que retornan al siguiente año. | (Reinscritos / matriculados año anterior) * 100. | Anual. |
| Tasa de retención de docentes | Docentes que continuan al siguiente año. | Análogo. | Anual. |
| Carga horaria promedio docente | Horas semanales asignadas. | Promedio. | Por período. |
| Anotaciones disciplinarias | Total y por tipo. | Conteo y distribución. | Mensual. |
| Cumplimiento del plan de estudios | % de logros / temas avanzados vs planeados. | Análogo. | Por periodo. |

## Reglas de negocio

- **RN-KP-001 — Aislamiento de KPIs por tenant:** un colegio solo ve sus propios KPIs operativos.
- **RN-KP-002 — KPIs SaaS solo para plataforma:** los KPIs internos del SaaS no son visibles para los colegios.
- **RN-KP-003 — Cálculo trazable:** cada KPI tiene definición y fórmula publicada para que el cliente pueda auditarlo.
- **RN-KP-004 — Frescura declarada:** cada KPI muestra la fecha y hora del último cálculo.

## Notas y pendientes

- **[Decisión tomada]** **Sin benchmark entre colegios.** Cada colegio visualiza únicamente su propia información, métricas e indicadores. No se contemplan comparaciones entre instituciones, **ni siquiera anónimas**, manteniendo aislamiento total entre tenants. Regla: **RN-KP-300 — Aislamiento estricto: cero benchmark cross-tenant**.
- **[Decisión tomada]** Las **métricas financieras de la plataforma** (MRR, ARR y similares) son de **uso exclusivo interno** del proveedor SaaS. **No se publican** ni se exponen a los tenants. Regla: **RN-KP-301 — MRR/ARR uso interno; sin exposición pública ni a tenants**.
