---
titulo: "CU-001: Onboardear nuevo colegio"
modulo: 03-multi-tenancy
tipo: caso-de-uso
estado: borrador
tags: [caso-de-uso, onboarding, tenant, superadmin]
---

# CU-001: Onboardear nuevo colegio

## Identificación

- **ID:** CU-001
- **Nombre:** Onboardear nuevo colegio
- **Módulo:** Multi-tenancy + Usuarios y roles
- **Prioridad:** alta
- **Versión:** 0.1

## Actores

- **Primario:** [[../02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma|Superadministrador de Plataforma]].
- **Secundarios:** [[../02-usuarios-roles-y-permisos/roles/01-rector-administrador-colegio|Rector / Administrador del Colegio]] (recibe la cuenta).

## Descripción

Creación y aprovisionamiento de un nuevo tenant (colegio) en la plataforma, con su base de datos, bucket, configuración inicial y usuario administrador.

## Precondiciones

- El colegio firmó el contrato comercial.
- El superadmin tiene los datos básicos: nombre, NIT, contacto, plan contratado, calendario (A o B).

## Postcondiciones (éxito)

- Tenant en estado **Trial** o **Activo** según contrato.
- Base de datos y bucket aprovisionados.
- Cuenta del rector / administrador creada con invitación enviada.
- Configuración mínima cargada (calendario, niveles, sedes si aplica).
- Evento registrado en el [[../11-plataforma-y-operacion/log-de-auditoria|log]].

## Flujo principal (camino feliz)

1. Superadmin entra al panel global.
2. Crea un nuevo tenant: nombre, identificación fiscal, plan, calendario, país, zona horaria.
3. El sistema valida unicidad del subdominio y aprovisiona DB y bucket.
4. Sistema crea la cuenta inicial del rector con email de contacto.
5. Sistema envía invitación por correo al rector (incluye URL del subdominio del colegio).
6. Sistema marca el tenant como **Trial** con fecha límite.
7. Rector acepta la invitación y completa onboarding (ver CU-onboarding-usuario).
8. Sistema registra el alta en el log.

## Flujos alternativos

### A1. Plan anual prepago

- Tenant inicia directamente en estado **Activo** tras confirmación del primer pago.

### A2. Migración desde otro sistema

- Tras crear el tenant, el equipo de operación carga datos históricos vía proceso especializado.

## Excepciones / errores

| ID | Condición | Comportamiento esperado |
| --- | --- | --- |
| EX-1 | Subdominio duplicado. | Sistema rechaza la creación con mensaje claro. |
| EX-2 | Email del rector ya pertenece a otro tenant. | Sistema valida; si el modelo permite multi-tenant para el usuario, se vincula; si no, se solicita otro correo. |
| EX-3 | Falla del aprovisionamiento (DB / bucket). | Sistema reintenta y, si falla, deja el tenant en estado **Provisionando con error** y alerta a operación. |

## Reglas de negocio aplicables

- RG-001 (aislamiento), RG-007 (permisos), RG-016 (acceso del superadmin auditado).
- RN-PS-002 (acceso académico siempre disponible) aplica una vez activo.

## Datos de entrada / salida

- **Entrada:** datos del colegio, plan, calendario, zona horaria, país, contacto.
- **Salida:** subdominio, credenciales de la cuenta inicial, fecha de fin de trial.

## Criterios de aceptación

- [ ] El tenant se crea en menos de 5 minutos en condiciones normales.
- [ ] La invitación al rector llega al email registrado.
- [ ] El subdominio queda accesible al finalizar el aprovisionamiento.
- [ ] El log de auditoría registra el alta con el actor superadmin.

## Notas y pendientes

- Definir si el superadmin puede personalizar el branding al crear el tenant o si lo hace el rector después.
