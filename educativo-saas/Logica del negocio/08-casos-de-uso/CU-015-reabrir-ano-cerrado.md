---
titulo: "CU-015: Reabrir año cerrado por excepción"
modulo: 11-plataforma-y-operacion
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, reapertura, rector, excepcion]
---

# CU-015: Reabrir año cerrado por excepción

## Identificación

- **ID:** CU-015
- **Nombre:** Reabrir año cerrado por excepción
- **Módulo:** Plataforma y operación / Procesos académicos
- **Prioridad:** media
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rector / Administrador del Colegio]].
- **Secundarios:** [[../04-procesos-academicos/consejo-academico|Consejo Académico]] (acta), Superadmin (apoyo técnico si aplica).

## Descripción

Reapertura excepcional y acotada de un año lectivo cerrado para corregir un proceso puntual (calificación, observación, matrícula) sustentada por motivo y acta.

## Precondiciones

- Año en estado **Cerrado**.
- Existe acta del consejo académico cuando la corrección es académica.
- Soporte adjunto del motivo.

## Postcondiciones (éxito)

- Año en estado **Reabierto** acotado al recurso afectado.
- Tras aplicar la corrección, año vuelve a **Cerrado**.

## Flujo principal

1. Rector entra a \"Reapertura excepcional\".
2. Selecciona el recurso a modificar (estudiante, asignatura, periodo, observación).
3. Llena motivo y adjunta acta / soporte.
4. Sistema confirma con doble validación.
5. Sistema desbloquea solo el recurso seleccionado.
6. Rector / coordinación aplica la corrección.
7. Sistema regenera documentos afectados (boletín, paz y salvo).
8. Rector cierra de nuevo el año.
9. Sistema registra todo el ciclo en el log.

## Flujos alternativos

### A1. Reapertura masiva (no permitida por defecto)

- El sistema no permite reabrir todo un año al tiempo. Cada caso requiere su propio motivo.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Falta acta o motivo. | Sistema bloquea. |
| EX-2 | Año demasiado antiguo (> ventana de reapertura). | Sistema bloquea o requiere autorización del superadmin. |

## Reglas de negocio aplicables

- RN-HA-003 (reapertura motivada), RN-ET-001..004, RG-002, RG-005.

## Criterios de aceptación

- [ ] La reapertura solo afecta al recurso seleccionado.
- [ ] Al cerrar de nuevo, los documentos quedan reemitidos con el cambio.
- [ ] El log refleja: reapertura, modificación, cierre con todos los actores y motivos.

## Notas y pendientes

- Definir la \"ventana máxima de reapertura\" (sugerido: 5 años desde el cierre).
