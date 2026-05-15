---
titulo: Visión del producto
modulo: vision-y-alcance
tipo: referencia
estado: borrador
tags: [vision, estrategia]
---

# Visión del producto

## Problema que resuelve

Los colegios en Colombia gestionan procesos académicos, disciplinarios, de matrícula, comunicación con padres y cobros con herramientas dispersas: hojas de cálculo, sistemas heredados sin soporte, plataformas genéricas no diseñadas para el contexto educativo local, y trámites manuales en papel. El resultado es duplicación de trabajo, pérdida de información histórica, dificultad para generar boletines y certificados consistentes a lo largo de los años, y comunicación lenta o inexistente con los acudientes.

## Visión a largo plazo

Ser la plataforma SaaS de referencia para la gestión académica de colegios en Latinoamérica, con multi-tenancy real, configuración fina por colegio, y un modelo de datos que respeta tanto el Calendario A como el Calendario B sin forzar a la institución a cambiar su forma de trabajar.

## Misión

Darle a cada colegio una plataforma propia (subdominio, datos aislados, configuración propia) sobre una base SaaS compartida, donde gestionar su año lectivo completo: desde la matrícula con pago en línea hasta el cierre del año con promoción automática, pasando por notas, asistencia, observador, boletines, comunicación y pagos.

## Diferenciadores clave

- **Aislamiento real por tenant:** base de datos exclusiva por colegio + subdominio propio. No es un simple `tenant_id` sobre una tabla compartida.
- **Soporte nativo de Calendario A y Calendario B:** el sistema entiende el formato "AAAA-AAAA" del Calendario B y no lo trata como dos años distintos.
- **Configuración profunda por colegio:** escala valorativa (numérica o por imágenes), método de aprobación, modelo pedagógico por nivel, jornadas y bloques horarios, conceptos cobrables, plantillas de boletín.
- **Inmutabilidad del histórico:** los años cerrados no se pueden modificar, ni siquiera por el administrador del colegio. Los boletines y certificados se regeneran con la configuración vigente al momento de su emisión original.
- **Pagos pasan directo al colegio:** la plataforma no retiene dinero de pensiones; actúa como intermediario tecnológico contra las cuentas y pasarelas que el colegio configura.
- **Auditoría completa e inviolable** sobre toda acción sensible.

## Métricas de éxito

- Número de tenants (colegios) activos.
- Tasa de retención anual de tenants.
- Tiempo promedio desde alta del tenant hasta operación normal (configuración inicial completa).
- Porcentaje de colegios con cobro de pensión activo a través de la plataforma.
- Volumen de boletines y certificados emitidos por año lectivo.
- Reducción de incidencias de soporte por errores manuales (notas, asistencia, paz y salvo).

## Notas y pendientes

- Definir mercado inicial geográfico exacto (ver [[mercado-objetivo|Mercado objetivo]]).
- Validar el modelo de cobro al colegio (ver [[../06-monetizacion-y-pagos/modelo-de-negocio|Modelo de negocio]]).
