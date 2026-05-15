---
titulo: "CU-014: Cerrar año lectivo"
modulo: 11-plataforma-y-operacion
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, cierre-de-ano, rector]
---

# CU-014: Cerrar año lectivo

## Identificación

- **ID:** CU-014
- **Nombre:** Cerrar año lectivo
- **Módulo:** Plataforma y operación / Procesos académicos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rector / Administrador del Colegio]].
- **Secundarios:** Coordinación, secretaría, contabilidad.

## Descripción

Cierre formal del año lectivo: tras concluir todos los procesos académicos y financieros, el rector marca el año como **cerrado** y los datos quedan inmutables.

## Precondiciones

- Promoción / reprobación confirmada para todos los estudiantes.
- Boletines finales generados.
- Cartera conciliada del año.
- Observador con observaciones cerradas.

## Postcondiciones (éxito)

- Año en estado **Cerrado**.
- Datos inmutables salvo reapertura formal (CU-015).
- Configuración versionada como configuración del año cerrado.

## Flujo principal

1. Rector entra a \"Cierre de año\".
2. Sistema muestra checklist de validaciones:
   - Notas cerradas y publicadas en todos los grupos.
   - Boletines finales generados.
   - Promoción confirmada.
   - Cartera conciliada.
3. Rector revisa y resuelve pendientes.
4. Rector ejecuta el cierre. Sistema solicita doble confirmación.
5. Sistema marca el año como cerrado, versiona configuración y libera el flujo de matrícula del siguiente año.
6. Sistema registra el cierre en el log con autor y timestamp.

## Flujos alternativos

### A1. Cierre con pendientes documentados

- El rector puede dejar constancia de excepciones (estudiantes cuyo caso queda en revisión) que se resolverán por reapertura.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Validación incompleta. | Sistema bloquea cierre. |
| EX-2 | Conciliación financiera con diferencias. | Sistema advierte y exige confirmación explícita. |

## Reglas de negocio aplicables

- RN-HA-001..006, RG-005, RG-006, RG-002.

## Criterios de aceptación

- [ ] El cierre solo procede al cumplir todas las validaciones.
- [ ] Tras el cierre, los datos del año no se modifican.
- [ ] El log registra el cierre con actor y fecha.

## Notas y pendientes

- Definir si el cierre genera automáticamente certificados de finalización a estudiantes que terminaron el último grado.
