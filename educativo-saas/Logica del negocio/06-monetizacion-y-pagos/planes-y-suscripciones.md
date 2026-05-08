---
titulo: Planes y suscripciones
modulo: monetizacion-y-pagos
tipo: referencia
estado: borrador
tags: [planes, suscripciones]
---

# Planes y suscripciones

## Planes ofrecidos

| Plan | Público objetivo | Funcionalidades clave |
| --- | --- | --- |
| Esencial | Colegios pequeños (< 300 estudiantes). | Académico, asistencia, comunicación básica, pagos de pensión con 1 pasarela, almacenamiento limitado. |
| Estándar | Colegios medianos (300–800 estudiantes). | Todo lo anterior + boletines personalizables, reportes financieros, multi-sede, múltiples pasarelas. |
| Premium | Colegios grandes (800+ estudiantes) o con necesidades avanzadas. | Todo lo anterior + WhatsApp, BI avanzado, integraciones DIAN / facturación electrónica, almacenamiento ampliado, soporte priorizado. |

Las funcionalidades exactas de cada plan se mantienen en una matriz separada que el equipo de producto puede actualizar.

## Ciclos de facturación

- **Mensual:** cobro al inicio del periodo de servicio.
- **Anual prepago:** descuento aplicable. Cobro único al inicio del año de servicio.
- **Anual escolar prepago:** alineado al año lectivo del colegio (en lugar del año calendario).

El ciclo de facturación del colegio (B2B) es independiente del ciclo de cobro de pensiones a los padres.

## Periodo de prueba (trial)

- Trial estandar: 30 días.
- Durante el trial el colegio puede cargar datos, configurar y operar.
- Al expirar el trial, el colegio entra en estado **suspensión suave**: lectura permitida, escritura bloqueada en módulos no esenciales, hasta confirmar la suscripción.
- Los datos cargados durante el trial se preservan al activar la suscripción.

## Upgrades y downgrades

- **Upgrade:** efecto inmediato. El sistema cobra la diferencia prorrateada por los días restantes del ciclo.
- **Downgrade:** efecto al final del ciclo actual. Hasta entonces el colegio conserva las funcionalidades del plan superior.
- Si el downgrade implica perder datos (ej. menos sedes que las activas), el sistema bloquea el cambio hasta que el colegio resuelva el conflicto.

## Cancelación y reembolsos

- El colegio puede solicitar la cancelación en cualquier momento.
- La cancelación se hace efectiva al final del ciclo de facturación vigente.
- No hay reembolso por periodos no consumidos en planes mensuales. En planes anuales prepagos, el reembolso queda sujeto a la política comercial vigente.
- Tras la cancelación, el tenant pasa por las fases definidas en [[../03-multi-tenancy/modelo-de-tenants|Modelo de tenants]] hasta su eliminación definitiva (incluye exportación y retención).

## Estados de la suscripción

```
Trial → Activa → Suspendida (mora) → Activa
              → Cancelada solicitada → Finalizada
```

| Estado | Comportamiento |
| --- | --- |
| Trial | Acceso completo, fecha límite. |
| Activa | Acceso completo. |
| Suspendida | Lectura permitida, escritura bloqueada en módulos no esenciales. Acceso a la información académica preservado. |
| Cancelada solicitada | Sigue activa hasta el fin de ciclo. |
| Finalizada | Tenant pasa a fase de retención previa a eliminación. |

## Reglas de negocio

- **RN-PS-001 — Suspensión no destruye datos:** la suspensión por mora no elimina datos.
- **RN-PS-002 — Académico siempre accesible:** incluso en suspensión, el módulo académico esencial (consulta de notas, asistencia, observador) sigue accesible para no afectar al estudiante.
- **RN-PS-003 — Downgrade respeta integridad:** un downgrade que implique pérdida de datos se bloquea hasta resolver el conflicto.
- **RN-PS-004 — Trial preserva datos:** los datos cargados en trial se conservan al activar la suscripción.
- **RN-PS-005 — Reactivación posible:** un colegio suspendido puede reactivarse al ponerse al día con su pago.

## Notas y pendientes

- Definir días de gracia entre el vencimiento de un cobro al colegio y la entrada en estado suspendida.
- Definir el procedimiento de "reactivación con cargos pendientes".
