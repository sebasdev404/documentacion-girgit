---
titulo: Mercado objetivo
modulo: vision-y-alcance
tipo: referencia
estado: borrador
tags: [mercado, segmentacion]
---

# Mercado objetivo

## Segmentos de colegios

- **Colegios privados** que operan en Calendario A o Calendario B, con cobro de matrícula y pensiones directamente a los acudientes.
- **Colegios públicos / oficiales** que operan en Calendario A, sin cobros recurrentes pero que requieren igualmente gestión académica completa, boletines, observador y comunicación.
- **Colegios mixtos** (privados con convenio o subsidio) que combinan elementos de ambos modelos.

## Geografía

- **Mercado inicial (fase 1):** colegios **privados** de Colombia + colegios **privados** de un segundo país piloto de Latinoamérica (candidatos: Ecuador o Perú).
- **Razones para Colombia:** marco normativo conocido (Ministerio de Educación Nacional, resolución, NIT, integración con DIAN para facturación electrónica), dos calendarios académicos oficiales (A y B), y mercado fragmentado donde los colegios actualmente usan herramientas dispersas.
- **Razones para el segundo país piloto:** validar tempranamente que la arquitectura multi-tenant y el modelo de configuración por colegio sirven en una segunda jurisdicción antes de escalar a más países.
- **Fase 2:** colegios **públicos / oficiales** de Colombia y ampliación a más países de Latinoamérica con calendarios y normativas similares.

## Tamaño de los colegios (rangos de estudiantes)

| Rango | Características | Plan sugerido |
| --- | --- | --- |
| 50–300 estudiantes | Colegios pequeños, con poco personal administrativo | Plan básico |
| 300–800 estudiantes | Colegios medianos, ya con coordinaciones diferenciadas | Plan estándar |
| 800–2000 estudiantes | Colegios grandes con múltiples sedes o jornadas | Plan completo |
| > 2000 estudiantes | Colegios muy grandes o redes de colegios | Plan empresa / personalizado |

## Necesidades comunes del segmento

- Gestión académica del año lectivo completo (notas, asistencia, boletines, promoción).
- Cobro de matrícula y pensión en línea con confirmación automática.
- Comunicación a acudientes con segmentación por grado/grupo.
- Histórico fiable y auditado para certificados y constancias de exalumnos.
- Configuración propia: cada colegio quiere mantener su escala, su modelo pedagógico y su plantilla de boletín.

## Buyer persona

### Persona 1 — Rector / propietario de colegio privado mediano

- Toma decisiones de compra de software.
- Le importa el costo, el aislamiento de datos, la posibilidad de personalizar y la rapidez de implementación.
- Le frustra tener que cambiar de proveedor cada pocos años o quedar atrapado en sistemas viejos sin soporte.

### Persona 2 — Administrador / coordinador encargado de implementación

- Es quien usa el sistema día a día para configurar y operar.
- Le importa la facilidad de uso, los reportes, y que el sistema no le exija cambiar la forma de trabajar del colegio.

## Notas y pendientes

- **[Pendiente — requiere datos de piloto]** Validar segmentación de planes con datos reales de colegios piloto (revisar si los rangos 50–300 / 300–800 / 800–2000 reflejan los puntos de quiebre reales de funcionalidades y precio).
- **[Decisión tomada]** Colegios públicos quedan fuera del lanzamiento (fase 1). Entran en fase 2 una vez validado el modelo con privados.
- **[Decisión pendiente]** Selección final del segundo país piloto (Ecuador vs. Perú): depende de relaciones comerciales, marco normativo de facturación y disponibilidad de pasarelas de pago locales.
