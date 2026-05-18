---
tags:
  - arquitectura
  - rol/superadmin
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-01
---

# Respuestas del Sistema — Superadministrador de la Plataforma

Que responde el sistema ante cada evento.

| Evento | Respuesta del Sistema |
|---|---|
| Superadmin crea un tenant | Provisiona schema + semillas · genera subdominio · crea cuenta del Rector · envia correo de acceso al Rector · cambia estado a Activo · registra en log global |
| Provisioning de schema falla | Revierte toda la creacion (transaccional) · notifica al superadmin · registra error tecnico · no deja tenant parcial |
| Superadmin suspende un tenant | Bloquea login de todos los usuarios del tenant · muestra a esos usuarios pantalla "colegio suspendido" · notifica al Rector por correo · registra en log |
| Superadmin reactiva un tenant | Restablece login · notifica al Rector · registra en log |
| Superadmin elimina un tenant | Preserva logs segun retencion (RN-RT-401) · programa borrado diferido · registra evento critico · notifica a direccion interna |
| Superadmin cambia el plan | Aplica limites/funciones del nuevo plan · si baja de plan y excede limites, marca recursos en exceso y notifica al Rector · registra historico y log |
| Superadmin cambia calendario A/B | Recalcula estructura de periodos del tenant · notifica al Rector · registra en log (RR-13) |
| Superadmin amplia/reduce cuota | Actualiza limite efectivo · recalcula alertas · si reduce por debajo del consumo, alerta sin borrar datos · registra en log |
| Backup manual finaliza | Actualiza estado del ultimo backup · notifica si fallo · registra en log |
| Restauracion finaliza | Restaura datos al punto elegido · notifica al superadmin y al Rector · registra evento critico |
| Superadmin consulta el log global | Devuelve resultados filtrados · registra la consulta como meta-auditoria (RN-LA-006) |
| Superadmin exporta el log | Genera archivo con marca de quien y cuando exporto · registra la exportacion |
| Superadmin inicia impersonacion | Abre sesion con expiracion · inyecta banner permanente "Impersonando a X" · registra inicio con doble identificador (RN-RT-402) |
| Accion durante impersonacion | Ejecuta como el usuario impersonado · registra con superadmin real + usuario impersonado · notifica al Rector del tenant (RN-LA-002) |
| Sesion de impersonacion expira | Cierra sesion automaticamente · retira banner · registra fin en log |
| Login fallido del superadmin | Mensaje generico (no revela si el usuario existe) · incrementa contador de intentos · registra en log de seguridad · bloquea tras N intentos |
| Caida de una integracion externa (pasarela/correo/SMS) | Marca la integracion en rojo en "Salud del sistema" · genera alerta · no afecta el aislamiento de los tenants |
| Tenant supera umbral de cuota | Genera alerta en dashboard · notifica al superadmin y al Rector |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/11-plataforma-y-operacion/log-de-auditoria.md`
