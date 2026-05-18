---
tags:
  - arquitectura
  - rol/superadmin
  - validaciones
aliases:
  - Validaciones ROL-01
---

# Validaciones — Superadministrador de la Plataforma

Casos de validacion y comportamiento del sistema.

## Crear tenant

| Caso | Comportamiento del Sistema |
|---|---|
| Nombre vacio o < 3 caracteres | Bloquea envio; muestra "El nombre del colegio es obligatorio (min 3 caracteres)" |
| NIT con formato invalido | Bloquea envio; muestra "NIT invalido" |
| NIT ya existente en plataforma | Bloquea envio; muestra "Ya existe un colegio con este NIT" |
| Subdominio con caracteres no permitidos | Bloquea envio; muestra "Solo letras, numeros y guion" |
| Subdominio ya en uso o reservado | Bloquea envio; muestra "Subdominio no disponible" |
| Correo del Rector invalido | Bloquea envio; muestra "Correo invalido" |
| Cuota de almacenamiento <= 0 o sobre el plan | Bloquea envio; muestra "Cuota fuera del rango del plan seleccionado" |
| Falla el provisioning del schema | Revierte la creacion (transaccional); no deja tenant a medias; registra error en log; muestra "No se pudo provisionar el tenant, reintente" |

## Cambiar calendario A/B

| Caso | Comportamiento del Sistema |
|---|---|
| Nuevo calendario igual al actual | Bloquea envio; muestra "El tenant ya usa ese calendario" |
| Checkbox de confirmacion sin marcar | Bloquea envio; resalta el checkbox |
| Motivo < 10 caracteres | Bloquea envio; muestra "Indique un motivo (min 10 caracteres)" |
| Tenant con periodo academico en curso | Advierte: "Hay un periodo activo; el cambio recalcula su estructura. Confirme." (no bloquea, pero exige doble confirmacion) |

## Eliminar / suspender tenant

| Caso | Comportamiento del Sistema |
|---|---|
| Eliminar sin motivo | Bloquea; exige motivo (queda en log como evento critico) |
| Eliminar sin confirmacion fuerte | Bloquea; pide escribir el nombre del tenant para confirmar |
| Suspender un tenant ya suspendido | Bloquea; muestra "El tenant ya esta suspendido" |

## Impersonacion (RN-RT-402)

| Caso | Comportamiento del Sistema |
|---|---|
| Sin ticket interno | Bloquea; muestra "Debe asociar un ticket de soporte" |
| Justificacion < 20 caracteres | Bloquea; muestra "Justificacion insuficiente" |
| Usuario objetivo inactivo | Bloquea; muestra "No se puede impersonar a un usuario inactivo" |
| Sesion supera la duracion | Expira automaticamente; cierra la sesion; registra fin en log |
| Intento de impersonar desde un rol que no es superadmin | Bloquea en backend; registra intento en log de seguridad |

## Restauracion de backup

| Caso | Comportamiento del Sistema |
|---|---|
| Sin doble confirmacion | Bloquea; exige ambas confirmaciones |
| Punto de restauracion corrupto / inexistente | Bloquea; muestra "Backup no disponible o invalido" |
| Restauracion en curso para el mismo tenant | Bloquea; muestra "Ya hay una restauracion en proceso para este tenant" |

## Transversales

| Caso | Comportamiento del Sistema |
|---|---|
| Sesion sin MFA | Bloquea acceso al panel; MFA es obligatorio para este rol |
| Accion sensible sin conectividad con el log | Bloquea la accion; no se permite operar sin poder auditar (RR-03) |
| Token expirado a mitad de operacion | Cierra sesion; la operacion no se aplica; pide reautenticacion |

## Relacionado

- [[09 - Campos del Formulario]]
- [[11 - Respuestas del Sistema]]
- [[../_Globales/08 - Criterios de Aceptacion|Criterios de Aceptacion]]
