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
| Estándar | Colegios medianos (300–800 estudiantes). | Todo lo anterior + boletines personalizables, reportes financieros, multi-sede, múltiples pasarelas, Aula por asignatura y colores configurables de su jerarquía. |
| Premium | Colegios grandes (800+ estudiantes) o con necesidades avanzadas. | Todo lo anterior, incluida Aula y su apariencia configurable, + WhatsApp, BI avanzado, integraciones DIAN / facturación electrónica, almacenamiento ampliado, soporte priorizado. |

Las funcionalidades exactas de cada plan se mantienen en una matriz separada que el equipo de producto puede actualizar.

**Implementado localmente el 7 de octubre de 2026:** Aula por asignatura empieza en Estándar y no forma parte de Esencial. La capacidad `aula` controla el acceso al módulo; `aula_colores`, listada inmediatamente después en el catálogo comercial, controla la configuración de los acentos de períodos y preinformes y requiere `aula`. Ambas vienen por defecto en Estándar y Premium, pero la plataforma puede retirarlas por plan personalizado sin eliminar contenido ni calificaciones. Sin `aula_colores` se muestran colores predeterminados y la configuración guardada se conserva para una eventual reactivación. Solo el rector puede modificar esos colores mediante el permiso `aula.apariencia.configurar`. Planillas y notas siguen disponibles en Esencial sin Aula. Véase [[../04-procesos-academicos/plan-aula-virtual-y-ayuda-asistencia-2026-10-06|Plan de Aula por asignatura y ayuda de asistencia]]. Aplicar las migraciones en cada entorno no equivale a haber desplegado o verificado el VPS.

## Ciclos de facturación

### Matrículas por enlace: alcance comercial del corte 2026-10-07

Ingreso estudiantil pertenece a la capacidad existente `academico`, con seis permisos `ingreso.*` en el catálogo/matriz. No se creó un suplemento comercial ni se habilitó pasarela. Al aprobar una solicitud se verifica `max_estudiantes`; los documentos consumen cuota de almacenamiento del tenant. Quitar `academico` bloquea endpoints internos/públicos de solicitud sin borrar expedientes. Los planes que lo incluyen pueden usar el módulo sujeto a permisos; no confundir con `aula` ni `aula_colores`.

La conexión de Gmail por colegio es configuración institucional básica en todos los planes, sin suplemento ni capacidad comercial adicional; requiere `config.correo`, exclusivo del rector. Usa una cuenta aportada por el colegio, sujeta a cuotas/políticas de Google; no implica correo ilimitado ni servicio transaccional contratado por la plataforma. Aplica también a recuperación de contraseña, independiente del módulo de matrículas.

Una conexión guardada queda bloqueada en todos los planes. Cambiarla o desconectarla requiere aprobación directa del superadministrador central: autorización personal, ligada al colegio, la acción y la versión, de un solo uso durante 24 horas. Ningún plan ni permiso delegado elimina este control (RN-CO-001).

El texto «Pagos: próximamente» es informativo: no hay cargo, descuento, factura ni comprobación de pago en la versión actual. El cobro B2B del colegio sigue siendo independiente.

- **Mensual:** cobro al inicio del periodo de servicio.
- **Anual prepago:** descuento aplicable. Cobro único al inicio del año de servicio.
- **Anual escolar prepago:** alineado al año lectivo del colegio (en lugar del año calendario).

El ciclo de facturación del colegio (B2B) es independiente del ciclo de cobro de pensiones a los padres.

## Periodo de prueba (trial)

- Trial estándar: **30 días** (valor confirmado).
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
- **RN-PS-006 — Días de gracia configurables por colegio:** el rector o encargado del colegio configura los días de gracia entre el vencimiento del cobro y la entrada en suspensión. La plataforma propone un valor sugerido pero no lo impone.
- **RN-PS-007 — Trial estándar 30 días:** el trial por defecto al onboarding de un colegio nuevo es de 30 días, salvo acuerdo comercial específico.
- **RN-PS-008 — WhatsApp solo en Premium:** el canal WhatsApp Business como notificación está disponible únicamente en el plan Premium.

## Notas y pendientes

- **[Decisión pendiente]** Procedimiento de "reactivación con cargos pendientes": condiciones bajo las cuales se reactiva un colegio antes de saldar la totalidad de la deuda (acuerdo formal, plan de pagos, decisión del rector).
- **[Decisión pendiente]** Política de reembolso para planes anuales prepagos cancelados antes del fin de ciclo. Por ahora la cláusula queda "sujeta a política comercial vigente".
- **[En discusión]** Cuotas de almacenamiento incluidas por plan. Hipótesis de trabajo: Esencial 20 GB / Estándar 100 GB / Premium 500 GB. Pendiente de validar costos del proveedor.
- **[Decisión pendiente]** Inclusión de facturación electrónica DIAN en planes (Estándar y/o Premium). Aún no se ha discutido el costo del proveedor tecnológico ni si se factura aparte como add-on.
