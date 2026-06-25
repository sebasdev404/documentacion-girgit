---
titulo: Transporte escolar
modulo: bienestar-y-servicios
tipo: proceso
estado: borrador
tags: [transporte, rutas, bienestar, servicio, cobro]
---

# Transporte escolar

## Descripción

Proceso por el cual el colegio presta el servicio de transporte (ruta) a los estudiantes: define rutas y paradas, asigna estudiantes a una ruta, registra el control de abordaje y descenso con notificación al acudiente, gestiona novedades del servicio y cobra el transporte como concepto recurrente integrado a [[../06-monetizacion-y-pagos/pagos-de-pensiones|pagos]]. El servicio es opcional por estudiante y configurable por colegio: algunos lo operan con flota propia y otros con un proveedor tercerizado.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[roles/05-secretaria-academica\|Secretaría Académica]] | Define rutas y paradas, asigna estudiantes, configura el concepto cobrable del transporte y gestiona novedades administrativas. |
| Monitor de ruta | Persona a bordo que registra abordaje y descenso de cada estudiante en su parada; reporta novedades del servicio. |
| Conductor | Opera el vehículo de la ruta; no registra abordaje salvo que el colegio no tenga monitor (configurable). |
| [[roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]] | El estudiante es el sujeto transportado; el acudiente recibe las notificaciones de abordaje/descenso y paga el servicio. |
| [[roles/01-rector-administrador-colegio\|Rector / Administrador del colegio]] | Aprueba la operación del servicio y la política de cobro; visibilidad consolidada. |

> El monitor y el conductor pueden no ser usuarios plenos del SIS. El colegio define si se les crea un acceso acotado (solo la app de ruta) o si la secretaría registra por ellos. Acuerdo coherente con el manejo del acudiente como no-usuario.

## Estructura del servicio: rutas y paradas

- Una **ruta** tiene nombre, sentido (recogida en la mañana / entrega en la tarde, o ambos), vehículo asignado, monitor y conductor, y un cupo máximo.
- Una **parada** pertenece a una ruta y tiene nombre, dirección/referencia, orden dentro del recorrido y hora estimada de paso.
- Un estudiante se asigna a **una ruta y una parada** por sentido. Puede tener parada distinta en la mañana y en la tarde.
- Las rutas se definen por año lectivo; al cerrar el año, las asignaciones no se arrastran automáticamente (se reasignan en la matrícula del año siguiente).

## Flujo principal (día de operación)

1. La secretaría tiene configuradas las rutas, paradas y los estudiantes asignados del año lectivo en curso.
2. Al iniciar el recorrido de recogida, el monitor abre la ruta del día en su dispositivo y ve el listado ordenado de paradas con los estudiantes esperados.
3. En cada parada, el monitor marca el **abordaje** de cada estudiante que sube.
4. El sistema notifica al acudiente que el estudiante **abordó** la ruta, con hora y parada.
5. Al llegar al colegio, el monitor cierra el recorrido; el sistema registra la **llegada** y, si está habilitado, alimenta la marca de presencia para [[../04-procesos-academicos/asistencia|asistencia]].
6. En el recorrido de entrega (tarde), el monitor marca el **descenso** de cada estudiante en su parada.
7. El sistema notifica al acudiente que el estudiante **descendió** en su parada, con hora.
8. Si un estudiante esperado no aborda, el monitor lo marca como **no abordó** y el sistema notifica al acudiente.

## Novedades del servicio

1. El monitor (o la secretaría) registra una novedad asociada a un recorrido o a un estudiante: retraso de ruta, cambio de parada por un día, ausencia anunciada, daño del vehículo, ruta no operada.
2. La novedad puede ser **informativa** (solo notifica) o **operativa** (afecta el cobro o requiere acción de la secretaría).
3. El sistema notifica a los acudientes afectados según el alcance de la novedad (un estudiante, una parada o toda la ruta).
4. Las novedades quedan en el historial del servicio del estudiante y de la ruta para auditoría y atención de reclamos.

## Cobro del transporte

- El transporte es un **concepto cobrable recurrente** dentro de [[../06-monetizacion-y-pagos/pagos-de-pensiones|pagos]], independiente de la pensión.
- El valor puede ser único por colegio o **diferenciado por zona/parada** (paradas más lejanas con mayor valor), configurable por colegio.
- El cobro se genera mensualmente para los estudiantes con asignación de ruta activa, según el cronograma de cobro del colegio.
- Al **retirar** a un estudiante del servicio a mitad de mes aplica la política de prorrateo del colegio, coherente con `RN-PP-121` (prorrateo configurable sin devoluciones automáticas).
- El no pago del transporte **no suspende** el servicio de forma automática: la suspensión por cartera la decide el colegio con su política de cobro (ver [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|políticas de cobro y mora]]).

## Estados y transiciones

### Asignación del estudiante al servicio

```
Sin servicio → Asignado (ruta + parada) → Suspendido (por novedad o cartera)
                                        → Retirado (fin de servicio)
Suspendido → Asignado (reactivación)
```

### Recorrido del día

```
Programado → En curso (monitor abre ruta) → Cerrado (llegada/fin recorrido)
Programado → No operado (novedad de ruta no operada)
```

### Abordaje de un estudiante en un recorrido

```
Esperado → Abordó → Descendió
Esperado → No abordó
```

## Configurabilidad por colegio

- Operación con **flota propia** o **proveedor tercerizado** (cambia quién administra rutas y vehículos, no el flujo del SIS).
- Quién registra el abordaje: **monitor** (default), conductor, o registro manual por secretaría.
- Valor del transporte: **plano** o **diferenciado por zona/parada**.
- Activar o no la alimentación de **asistencia** a partir de la llegada de la ruta.
- Canales de notificación de abordaje/descenso (portal, push, WhatsApp según plan), dentro del catálogo de [[../05-comunicacion/notificaciones|notificaciones]].
- Política de suspensión del servicio por cartera (manual por defecto).

## Integraciones con otros módulos

- **[[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos]]:** el transporte es un concepto cobrable recurrente que se factura junto al resto de cargos del estudiante.
- **[[../05-comunicacion/notificaciones|Notificaciones]]:** abordaje, descenso, no abordó y novedades de ruta se emiten como eventos notificables al acudiente.
- **[[../04-procesos-academicos/asistencia|Asistencia]]:** opcionalmente, la llegada de la ruta puede alimentar la presencia del estudiante.
- **[[../04-procesos-academicos/espacios-fisicos|Espacios físicos]]:** el vehículo de ruta se modela como un recurso con cupo, análogo a un espacio.

## Datos involucrados

- Ruta (nombre, sentido, vehículo, monitor, conductor, cupo, año lectivo).
- Parada (nombre, dirección/referencia, orden, hora estimada, zona/valor).
- Asignación estudiante → ruta + parada por sentido.
- Registro de abordaje/descenso (estudiante, recorrido, parada, hora, estado, monitor).
- Novedades del servicio.
- Concepto cobrable de transporte y sus cargos mensuales.

## Reglas de negocio

- **RN-TR-001 — Asignación única por sentido:** un estudiante tiene a lo sumo una ruta y una parada por sentido (mañana/tarde); puede diferir entre sentidos pero no duplicarse dentro del mismo.
- **RN-TR-002 — Cupo de ruta no excedible:** no se puede asignar un estudiante a una ruta que ya alcanzó su cupo máximo sin una autorización explícita de la secretaría registrada en auditoría.
- **RN-TR-003 — Notificación de abordaje y descenso:** todo abordaje y descenso registrado genera notificación automática al acudiente con hora y parada, y un "no abordó" también notifica.
- **RN-TR-004 — Cobro recurrente independiente:** el transporte se cobra como concepto recurrente separado de la pensión y solo a estudiantes con asignación de ruta activa en el periodo.
- **RN-TR-005 — Valor diferenciado por zona configurable:** el colegio puede definir un valor plano o un valor por zona/parada; el cargo mensual toma el valor de la parada asignada al estudiante.
- **RN-TR-006 — Mora no suspende automáticamente:** el atraso en el pago del transporte no suspende el servicio de forma automática; la suspensión por cartera es una decisión registrada por un rol con permiso.
- **RN-TR-007 — Prorrateo al retirar del servicio:** al retirar a un estudiante del transporte a mitad de mes, el cargo del mes en curso se prorratea según la política del colegio, sin ejecutar devoluciones automáticas (coherente con `RN-PP-121`).
- **RN-TR-008 — Trazabilidad del registro de ruta:** cada marca de abordaje/descenso queda con quién la registró (monitor o secretaría), hora y dispositivo, en log auditable.
- **RN-TR-009 — Novedad de ruta no operada notifica a toda la ruta:** cuando una ruta se marca como no operada, el sistema notifica a todos los acudientes de esa ruta y registra la novedad para el ajuste de cobro si el colegio lo define.

## Notas y pendientes

- **[Decisión tomada]** El registro de abordaje por defecto lo hace el **monitor**; el colegio puede configurar que lo haga el conductor o que la secretaría lo registre manualmente. Regla: **RN-TR-020 — Responsable del registro de abordaje configurable por colegio**.
- **[Decisión tomada]** El no pago del transporte **no suspende** el servicio automáticamente; la suspensión es manual por la política de cobro del colegio (`RN-TR-006`), coherente con el manejo de cartera de pensiones.
- **[Pendiente — producto]** Definir si la app del monitor debe funcionar **sin conexión** (registro offline con sincronización posterior), dado que muchas rutas pierden señal en trayecto. Evaluar durante el piloto.
- **[Pendiente — producto]** Decidir si el transporte tercerizado requiere un **rol de proveedor externo** con acceso acotado a sus rutas o si se opera solo desde la secretaría del colegio.

## Documentos relacionados

- [[../06-monetizacion-y-pagos/pagos-de-pensiones|Pagos de pensiones]]
- [[../06-monetizacion-y-pagos/politicas-de-cobro-y-mora|Políticas de cobro y mora]]
- [[../05-comunicacion/notificaciones|Notificaciones]]
- [[../04-procesos-academicos/asistencia|Asistencia]]
- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]]
- [[roles/05-secretaria-academica|Rol: Secretaría Académica]]
- [[roles/08-estudiante-y-acudiente|Rol: Estudiante / Acudiente]]
