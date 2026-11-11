---
titulo: Planes y suscripciones
modulo: monetizacion-y-pagos
tipo: referencia
estado: vigente-local
tags: [planes, suscripciones, contratos]
---

# Planes y contratos comerciales

Decisiones del 5 de noviembre de 2026. Solo se comercializan Estándar y Premium. Los planes históricos se archivan; sus registros no se eliminan. No se ofrecen cuentas ni portal propio de acudientes.

## Tarifas y capacidad

| Regla | Estándar | Premium |
| --- | --- | --- |
| Precio base por estudiante al mes | COP 1.500 | COP 2.500 |
| Mínimo de estudiantes contratados | 30 | 30 |
| Sedes incluidas (contando la principal) | 1 | 3 |
| Precio inicial por sede adicional al mes | COP 15.000 | COP 15.000 desde la cuarta |
| Almacenamiento inicial de archivos, compartido entre sedes | 2 GB | 5 GB |
| Roles principales y roles adicionales | Sin suplemento por rol | Sin suplemento por rol |

Las tarifas de sede, las tarifas de complementos y los demás límites son editables por el superadministrador. El importe por sede de COP 15.000 es un valor inicial de configuración, no un costo de infraestructura medido ni una rentabilidad garantizada.

El colegio contrata una capacidad de estudiantes para el conjunto de sus sedes. Un colegio con 15 estudiantes puede contratar 30 cupos y paga ese mínimo. Las cantidades no se multiplican por el número de sedes. Cada sede adicional tiene un cargo fijo mensual, no una tarifa por estudiante adicional.

Total mensual = estudiantes contratados × (tarifa base + complementos por estudiante) + sedes facturables × tarifa de sede.

Se cobra cada mes durante los 12 meses mientras la suscripción esté activa. La referencia anual es 12 mensualidades; no constituye una compra anual ni un pago anticipado obligatorio. El cambio de capacidad lo realiza por ahora únicamente el superadministrador.

## Herramientas actuales

Ambos planes incluyen núcleo institucional, gestión académica, SIEE, indicadores, notas, observaciones, nivelaciones, promoción, admisiones/matrículas, eventos/comunicación básica y emisión de boletines.

Estándar permite escoger diseños predefinidos y ajustar color y tamaño del texto. Premium permite además diseño libre, Aula y apariencia de Aula, asistencia, preinformes, múltiples sedes y soporte prioritario. Las autorizaciones dentro del colegio siguen dependiendo de la matriz, el rol y la asignación docente.

## Complementos del colegio

Un contrato Estándar puede agregar herramientas sin modificar el plan global ni los contratos de otros colegios. Los valores iniciales por estudiante y mes son: asistencia COP 200, preinformes COP 200, diseño libre de boletines COP 300, Aula COP 300 y soporte prioritario COP 100. Aula incluye su configuración de apariencia. No se cobra de nuevo una herramienta ya incluida en el plan.

Los complementos son un catálogo cerrado, validado en backend. No se admiten claves arbitrarias ni importes calculados por el navegador. El simulador y el guardado usan el mismo cálculo del servidor. Si una combinación se acerca a Premium, la interfaz recomienda compararlo; no cambia el plan automáticamente.

## Funciones proyectadas

Pagos, reportes financieros, integración/exportación SIMAT, facturación DIAN, WhatsApp, firma electrónica, carné QR, generador automático de horarios, BI y SSO se presentan como próximas funciones. Su presencia en el catálogo no significa disponibilidad. Pagos y reportes financieros se proyectan para ambos planes; su activación exige implementación y verificación. Los costos externos de pasarela y mensajería deben especificarse antes de comercializarlos. No se afirma que exista conexión automática con SIMAT.

## Contratos, permisos y conservación

El contrato se guarda con el colegio principal y se hereda por sus sedes. Conserva cantidades, complementos y desglose calculado al configurar. Cambiar un contrato no modifica el plan de los otros colegios. Reducir capacidad no puede dejar sedes o estudiantes activos fuera del contrato. Los datos académicos, las plantillas y los archivos se conservan aunque una herramienta deje de estar habilitada.

La configuración comercial y sus cambios se auditan. El cupo de archivos es compartido entre el colegio y sus sedes. Las cuotas no son espacio físico reservado ni incluyen una promesa de almacenamiento ilimitado.

## Alcance implementado

Catálogo, simulación, persistencia del contrato, creación/edición de colegios, capacidades efectivas, controles de acceso, sedes, cuotas y selección de diseños predefinidos se implementan localmente. Esta reestructuración no procesa cobros reales, no configura una pasarela B2B y no publica una página comercial. La contratación automática por el cliente queda para una fase posterior.

La inicialización de contratos existentes se realiza con `plans:initialize-contracts` (revisión) y `plans:initialize-contracts --apply` (persistencia); respeta los contratos ya configurados y no envía correos ni genera cargos. Las migraciones centrales y de tenant deben aplicarse por separado en cada entorno. La validación local no equivale a despliegue en VPS.

La integración comercial se comprueba contra PostgreSQL con `php scripts/test-commercial-postgres.php`. El ejecutor crea bases desechables para central y tenants, rechaza nombres fuera del entorno de prueba y las elimina al terminar; no utiliza la base operativa de ningún colegio. La suite rápida histórica mantiene su configuración de pruebas separada del motor PostgreSQL del SaaS.
