---
titulo: "CU-002: Matricular un estudiante"
modulo: 04-procesos-academicos
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, matricula, secretaria]
---

# CU-002: Matricular un estudiante

## Identificación

- **ID:** CU-002
- **Nombre:** Matricular un estudiante
- **Módulo:** Procesos académicos
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica|Secretaría Académica]].
- **Secundarios:** Acudiente, Estudiante, [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rector]] (aprobaciones excepcionales).

## Descripción

Confirmación oficial de la matrícula de un estudiante en un grupo de un grado en un año lectivo determinado, tras validar documentos y pagos.

## Precondiciones

- El estudiante existe en el sistema (creado en pre-matrícula o por carga).
- El año lectivo está activo y tiene cupos en el grupo objetivo.
- Si es renovación, el estudiante tiene paz y salvo del año anterior.

## Postcondiciones (éxito)

- Estado del estudiante: **Matrícula confirmada** y **Activa** en el año lectivo.
- Estudiante asignado a un grupo.
- Documentos requeridos almacenados y aprobados.
- Pago de matrícula registrado.
- Notificación enviada al acudiente.

## Flujo principal (camino feliz)

1. Secretaría busca al estudiante o lo crea (con sus acudientes).
2. Selecciona año lectivo, grado y grupo objetivo.
3. Sistema valida cupo del grupo y rango de edad sugerido.
4. Sistema valida paz y salvo del año anterior si aplica.
5. Secretaría sube los documentos requeridos.
6. Sistema valida que estén todos los documentos críticos.
7. Secretaría genera la cuota de matrícula.
8. Acudiente paga (CU-008 o CU-009) o secretaría registra pago previo.
9. Sistema marca matrícula como **confirmada** y emite contrato / soporte.
10. Sistema notifica al acudiente.

## Flujos alternativos

### A1. Estudiante nuevo (no renovación)

- Se omite la validación de paz y salvo del año anterior y se aplica el flujo de admisión.

### A2. Cambio de grupo dentro del mismo grado

- Secretaría usa el flujo de \"Cambio de grupo\", que no genera nueva cuota de matrícula.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Grupo sin cupo. | Sistema bloquea; ofrece otro grupo o lista de espera. |
| EX-2 | Paz y salvo no vigente. | Bloquea la matrícula salvo excepción del rector con motivo. |
| EX-3 | Documentos faltantes. | Permite continuar en estado \"Documentos pendientes\" sin confirmar. |
| EX-4 | Pago no realizado. | Matrícula queda en estado \"Pendiente de pago\". |

## Reglas de negocio aplicables

- RN-MA-NNN del módulo matrículas, RG-005 (inmutabilidad año cerrado), RN-PZ-005 (paz y salvo).

## Datos de entrada / salida

- **Entrada:** datos del estudiante, acudiente, año lectivo, grado, grupo, documentos.
- **Salida:** matrícula confirmada, contrato, cuota generada.

## Criterios de aceptación

- [ ] El sistema impide matricular en grupo sin cupo.
- [ ] El sistema valida paz y salvo y bloquea con mensaje claro si no procede.
- [ ] Al confirmar, el estudiante queda visible en su grupo y el acudiente recibe notificación.

## Notas y pendientes

- Definir si la secretaría puede revertir una matrícula confirmada y bajo qué condiciones.
