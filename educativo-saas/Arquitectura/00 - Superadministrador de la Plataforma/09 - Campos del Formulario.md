---
tags:
  - arquitectura
  - rol/superadmin
  - formularios
aliases:
  - Campos Formulario ROL-01
---

# Campos del Formulario — Superadministrador de la Plataforma

Campos de cada formulario que opera el rol.

## A) Formulario "Crear tenant" (RF-01)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Nombre del colegio | Texto | Si | Min 3 caracteres | Razon social / nombre comercial |
| NIT | Texto | Si | Formato NIT colombiano, unico en plataforma | Identificacion tributaria |
| Resolucion MEN | Texto | No | — | Resolucion del Ministerio de Educacion Nacional |
| Subdominio | Texto | Si | Solo a-z 0-9 guion, unico, sin reservadas | Define la URL del colegio |
| Pais | Select | Si | Lista de paises soportados | Determina normativa aplicable |
| Plan de licencia | Select | Si | basico / estandar / premium | Define limites y funciones |
| Calendario academico | Select | Si | A / B | Calendario habilitado inicial |
| Cuota de almacenamiento | Numero | Si | > 0, segun plan | En GB |
| Correo del primer Rector | Email | Si | Formato email valido | Recibe el acceso inicial |
| Nombre del primer Rector | Texto | Si | Min 3 caracteres | Contacto del colegio |

## B) Formulario "Cambiar plan" (RF-02)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tenant | Select | Si | Tenant existente | Colegio a modificar |
| Nuevo plan | Select | Si | Distinto al actual | basico / estandar / premium |
| Fecha de efectividad | Fecha | Si | >= hoy | Cuando aplica el cambio |
| Motivo | Texto largo | Si | Min 10 caracteres | Queda en log |

## C) Formulario "Cambiar calendario A/B" (RF-03)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tenant | Select | Si | Tenant existente | Colegio a modificar |
| Nuevo calendario | Select | Si | Distinto al actual (A o B) | Calendario destino |
| Confirmacion | Checkbox | Si | Debe marcarse | "Entiendo que esto recalcula los periodos" |
| Motivo | Texto largo | Si | Min 10 caracteres | Queda en log (RR-13) |

## D) Formulario "Iniciar impersonacion" (RN-RT-402)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tenant | Select | Si | Tenant existente | Colegio objetivo |
| Usuario a impersonar | Select | Si | Usuario activo del tenant | A quien se impersona |
| Ticket interno | Texto | Si | Formato de ticket valido | Trazabilidad del soporte |
| Justificacion | Texto largo | Si | Min 20 caracteres | Por que se necesita |
| Duracion | Select | Si | Maximo permitido por politica | Expira automaticamente |

## E) Formulario "Solicitar restauracion de backup"

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
| Tenant | Select | Si | Tenant existente | Colegio a restaurar |
| Punto de restauracion | Select | Si | Backup valido disponible | Snapshot a restaurar |
| Confirmacion doble | Checkbox x2 | Si | Ambas marcadas | Accion critica e irreversible |
| Motivo | Texto largo | Si | Min 20 caracteres | Queda en log como evento critico |

## Relacionado

- [[10 - Validaciones]]
- [[08 - Acciones del Usuario]]
