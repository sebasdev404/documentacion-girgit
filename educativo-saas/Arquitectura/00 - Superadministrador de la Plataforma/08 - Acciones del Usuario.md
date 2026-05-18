---
tags:
  - arquitectura
  - rol/superadmin
  - acciones
aliases:
  - Acciones ROL-01
---

# Acciones del Usuario — Superadministrador de la Plataforma

Tabla accion -> resultado. Cada accion sensible genera entrada en el log de auditoria global (RR-03, RN-LA-002).

| Accion | Resultado |
|---|---|
| Click en "Crear tenant" y completa el formulario | Sistema valida datos · provisiona schema PostgreSQL + semillas · genera subdominio · crea cuenta del primer Rector · envia acceso · registra en log |
| Click en "Suspender tenant" | Sistema pide motivo · cambia estado a Suspendido · bloquea acceso de los usuarios del tenant · notifica al Rector · registra en log |
| Click en "Reactivar tenant" | Sistema cambia estado a Activo · restablece acceso · notifica al Rector · registra en log |
| Click en "Eliminar tenant" | Sistema exige confirmacion fuerte + motivo · preserva logs segun retencion · programa borrado · registra evento critico en log |
| Cambia el plan de un tenant | Sistema aplica nuevo plan · ajusta limites/funciones · registra historico y log |
| Edita el subdominio de un tenant | Sistema valida unicidad · actualiza routing · invalida sesiones activas · registra en log |
| Cambia Calendario A <-> B | Sistema exige doble confirmacion + motivo · recalcula estructura de periodos · notifica al Rector · registra en log |
| Amplia / reduce cuota de almacenamiento | Sistema actualiza limite · recalcula alertas · registra en log |
| Dispara backup manual de un tenant | Sistema encola el backup · muestra progreso · al terminar actualiza estado y registra en log |
| Solicita restauracion de un backup | Sistema exige doble confirmacion + motivo · ejecuta restore en ventana controlada · registra evento critico en log |
| Consulta el log de auditoria global | Sistema muestra resultados filtrados · registra la consulta (meta-auditoria, RN-LA-006) |
| Exporta el log a CSV/JSON | Sistema genera archivo con marca de quien exporto · registra la exportacion en log |
| Inicia sesion de impersonacion | Sistema exige ticket + justificacion · abre sesion con expiracion · muestra banner permanente · registra inicio con doble identificador |
| Ejecuta una accion durante impersonacion | Sistema registra la accion con superadmin real + usuario impersonado (RN-RT-402) |
| Finaliza / expira la sesion de impersonacion | Sistema cierra la sesion · quita banner · registra fin en log |
| Cierra sesion | Sistema invalida token · registra logout en log |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
