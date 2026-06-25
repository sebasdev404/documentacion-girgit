---
titulo: Inventario y activos
modulo: bienestar-y-servicios
tipo: proceso
estado: borrador
tags: [inventario, activos, dotacion, mantenimiento, prestamo]
---

# Inventario y activos

## Descripción

Proceso por el cual el colegio registra y controla sus bienes físicos (equipos, mobiliario y dotación), los asigna a espacios físicos, los presta a docentes para uso pedagógico y gestiona su mantenimiento y baja. Cada activo tiene una ficha con su estado y su ubicación, y todo movimiento queda en historial.

## Objetivo del proceso

Tener un inventario único y confiable por colegio (tenant) que permita saber qué bienes existen, dónde están, en qué estado se encuentran y quién los tiene prestados, soportando la responsabilidad patrimonial de la institución.

## Actores involucrados

| Actor | Rol en el proceso |
| --- | --- |
| [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio\|Administrador del Colegio]] | Aprueba bajas, define categorías y políticas de préstamo. |
| [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica\|Secretaría Académica]] | Registra activos, gestiona asignaciones, préstamos y mantenimientos (rol operativo por defecto). |
| [[../02-usuarios-roles-y-permisos/roles/06-docente\|Docente]] | Solicita y recibe en préstamo recursos para sus clases; responde por su devolución. |
| [[../02-usuarios-roles-y-permisos/roles/02-coordinador-academico\|Coordinador Académico]] | Consulta disponibilidad de recursos al planear actividades. |

> El rol operativo responsable del inventario es **configurable por colegio**: por defecto recae en Secretaría Académica, pero un colegio puede asignarlo a otro rol con el permiso `inventario.gestionar`.

## Tipos de activo

| Categoría | Ejemplos | Identificación |
| --- | --- | --- |
| Equipo | Videobeam, portátil, tablet, impresora, microscopio. | Placa de inventario + serial del fabricante. |
| Mobiliario | Pupitre, silla, tablero, escritorio, estante. | Placa de inventario. |
| Dotación | Material de laboratorio, instrumentos, kits deportivos, libros de dotación institucional. | Placa o registro por lote (consumibles). |

Cada colegio puede crear categorías y subcategorías propias; el catálogo de categorías es configurable por tenant.

## Ficha del activo

- Placa de inventario (consecutivo único por colegio).
- Nombre y categoría.
- Serial / referencia del fabricante (si aplica).
- Fecha de adquisición, proveedor y valor de compra (opcional).
- Espacio físico asignado (cruza con [[../04-procesos-academicos/espacios-fisicos\|Espacios físicos]], `RN-EF`).
- Estado actual (operativo / en reparación / dado de baja).
- Responsable actual (espacio o docente en préstamo).

## Flujo principal (alta y asignación)

1. El responsable de inventario registra el activo y el sistema le asigna una **placa consecutiva** única dentro del colegio.
2. Selecciona categoría y completa la ficha.
3. Asigna el activo a un **espacio físico** existente del tenant (aula, laboratorio, sala, depósito).
4. El activo queda en estado **operativo** y disponible.
5. Cualquier cambio posterior (reubicación, préstamo, reparación, baja) genera un registro en el **historial del activo**.

## Préstamo de recursos a docentes

1. El docente solicita un recurso disponible (ej. videobeam) indicando el periodo de uso.
2. El responsable de inventario valida disponibilidad y aprueba el préstamo.
3. El activo cambia su responsable temporal al docente y queda marcado como **prestado** (sigue siendo `operativo`, pero no disponible para otro préstamo simultáneo).
4. En la devolución, el responsable verifica el estado del bien y cierra el préstamo; el activo vuelve a su espacio físico de origen.
5. Si el bien regresa dañado, se abre un **mantenimiento** y, según el caso, se deja constancia en el observador del docente o se reporta a Administración.

## Mantenimiento

1. Se abre una orden de mantenimiento (preventivo o correctivo) sobre el activo.
2. El activo pasa a estado **en reparación** y deja de estar disponible para préstamo o uso.
3. Se registra responsable de la reparación (interno o proveedor externo), fecha estimada y costo si aplica.
4. Al cerrar la orden: si el bien quedó funcional vuelve a **operativo**; si no, se propone su **baja**.

## Estados y transiciones

```
Operativo → En reparación → Operativo
                          → Dado de baja (requiere aprobación)
Operativo → Dado de baja (requiere aprobación)
```

- **Operativo:** en uso normal; puede asignarse a espacios y prestarse.
- **En reparación:** fuera de servicio temporalmente; no asignable ni prestable.
- **Dado de baja:** retirado del inventario activo por obsolescencia, pérdida, robo o daño irreparable. Estado terminal; el activo conserva su historial pero no aparece en disponibilidad.

## Configurabilidad por colegio

- Catálogo de categorías y subcategorías de activos.
- Formato y prefijo del consecutivo de placa.
- Rol responsable de la gestión de inventario (`inventario.gestionar`).
- Política de préstamo: duración máxima, si requiere aprobación, si el docente puede autoprestarse.
- Si registrar valor de compra y depreciación (algunos colegios solo controlan existencia física).
- Qué roles pueden aprobar una baja.

## Integraciones con otros módulos

- **Espacios físicos (`RN-EF`):** todo activo se asigna a un espacio del tenant; si un espacio se inactiva, sus activos deben reubicarse.
- **Observador del estudiante / docente:** daño o pérdida de un recurso prestado puede generar una anotación de responsabilidad (ver [[../04-procesos-academicos/observador-del-estudiante\|Observador del estudiante]]).
- **Pagos y otros cobros:** la reposición por daño o pérdida atribuible puede convertirse en un cargo (ver [[tienda-y-otros-cobros\|Tienda y otros cobros]]).
- **Log de auditoría:** altas, bajas, préstamos y reubicaciones quedan trazados (ver [[../11-plataforma-y-operacion/log-de-auditoria\|Log de auditoría]]).
- **Gestión documental:** facturas y actas de baja se adjuntan a la ficha del activo (ver [[../11-plataforma-y-operacion/gestion-documental\|Gestión documental]]).

## Reglas de negocio

- **RN-IV-001 — Placa única por tenant:** cada activo recibe una placa de inventario consecutiva y única dentro del colegio; no se reutiliza una placa de un activo dado de baja.
- **RN-IV-002 — Aislamiento multi-tenant:** el inventario es exclusivo del colegio; ningún activo, categoría ni placa es visible o compartible entre tenants.
- **RN-IV-003 — Activo siempre ubicado:** todo activo operativo debe estar asignado a un espacio físico existente del tenant o a un docente en préstamo; no se permiten activos operativos sin ubicación.
- **RN-IV-004 — Préstamo no concurrente:** un activo prestado no puede asignarse a un segundo préstamo hasta que se registre su devolución.
- **RN-IV-005 — En reparación no disponible:** un activo en estado `En reparación` no puede prestarse ni asignarse a una nueva ubicación hasta cerrar la orden de mantenimiento.
- **RN-IV-006 — Baja con aprobación y motivo:** dar de baja un activo requiere aprobación del rol autorizado (configurable, por defecto Administrador) y un motivo (obsolescencia, pérdida, robo, daño irreparable).
- **RN-IV-007 — Baja es estado terminal:** un activo dado de baja no vuelve al inventario operativo; conserva su historial para auditoría pero no figura en disponibilidad.
- **RN-IV-008 — Reubicación al inactivar un espacio:** si un espacio físico se marca inactivo, sus activos operativos deben reubicarse a otro espacio antes de completar la inactivación.
- **RN-IV-009 — Responsable en préstamo:** durante un préstamo, el docente que recibe el recurso queda como responsable registrado del activo hasta su devolución.
- **RN-IV-010 — Trazabilidad de movimientos:** toda alta, baja, reubicación, préstamo, devolución y cambio de estado queda en el historial inmutable del activo y en el log de auditoría con autor, fecha y valor anterior/nuevo.

## Notas y pendientes

- **[Decisión tomada]** El catálogo de categorías de activos y el rol responsable del inventario son **configurables por colegio**; el MVP entrega un catálogo base (Equipo / Mobiliario / Dotación) editable por el tenant.
- **[Decisión tomada — MVP]** El control de **depreciación contable y valor en libros** queda **fuera del MVP**: el inventario controla existencia, ubicación, estado y responsabilidad, no contabilidad de activos fijos.
- **[Pendiente — producto]** Definir si la **reposición por daño/pérdida** se integra automáticamente como cargo en el módulo de otros cobros o si solo deja constancia para gestión manual.
- **[Pendiente — producto]** Evaluar lectura de **código QR / código de barras** en la placa para acelerar inventarios físicos y préstamos desde el celular; candidato a fase posterior.

## Documentos relacionados

- [[../04-procesos-academicos/espacios-fisicos|Espacios físicos]] — asignación de activos a aulas y salas (`RN-EF`).
- [[../04-procesos-academicos/observador-del-estudiante|Observador del estudiante]] — constancia por daño o pérdida de recursos.
- [[tienda-y-otros-cobros|Tienda y otros cobros]] — cargos por reposición de bienes.
- [[../11-plataforma-y-operacion/log-de-auditoria|Log de auditoría]] — trazabilidad de movimientos de activos.
- [[../11-plataforma-y-operacion/gestion-documental|Gestión documental]] — soportes de adquisición y actas de baja.
- [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Administrador del Colegio]] — aprobación de bajas y políticas.
