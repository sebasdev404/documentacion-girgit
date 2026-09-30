---
tags:
  - arquitectura
  - rol/superadmin
aliases:
  - Arquitectura ROL-01
---

# Arquitectura — Superadministrador de la Plataforma

Wireframe principal del rol. Es el documento mas visual y referenciado del rol ROL-01.

> Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma.md` y la seccion `Logica del negocio/11-plataforma-y-operacion/`.

---

## N0 — Inicio (login de plataforma)

El Superadmin NO entra por el subdominio de ningun colegio (RR-06). Entra por una URL dedicada del panel de plataforma.

```
[ panel.plataforma.com ]
        |
        v
  Login (correo + contraseña; código MFA solo si el usuario lo activó)
        |
        +--- credenciales invalidas --> mensaje generico + registro en log
        |
        v
  Dashboard global de plataforma
```

- MFA opcional para este rol; se configura desde Ajustes de la cuenta.
- Todo intento de login (exito/fallo) queda en el log de auditoria global.

---

## HEADER (presente en toda la app)

```
[ Logo Plataforma ]   [ Buscador global de tenants ]      [ Estado del sistema ]  [ Perfil ]  [ Notificaciones ]
```

- **Perfil del usuario:** datos del superadmin, cerrar sesion, configurar MFA.
- **Buscador:** busca tenants por nombre, NIT, subdominio o estado.
- **Estado del sistema:** semaforo global (verde/amarillo/rojo) de salud de la plataforma.
- **Notificaciones:** incidentes, tenants en mora, fallos de backup, alertas de cuota.

---

## N1 — SIDEBAR (modulos del rol)

```
+---------------------------+
|  Dashboard global         |
|  Tenants                  |
|  Planes y licencias       |
|  Calendario A/B           |
|  Almacenamiento y cuotas  |
|  Backups y restauracion   |
|  Log de auditoria global  |
|  Soporte / Impersonacion  |
|  Salud del sistema        |
+---------------------------+
```

El Superadmin NO tiene acceso a modulos academicos (notas, asistencia, observador, boletines). Esos no aparecen en su sidebar.

---

## Detalle por modulo

### Dashboard global

Vista de entrada. Tarjetas resumen:
- Total de tenants (activos / suspendidos / en mora).
- Tenants creados en el ultimo mes.
- Alertas abiertas (fallos de backup, cuotas al limite, incidentes).
- Consumo agregado de almacenamiento.

> Callout informativo: el dashboard es de solo lectura; las acciones se hacen en cada modulo.

### Tenants

- **Sub-vistas:** lista de tenants / detalle de un tenant.
- **Filtros:** estado (activo/suspendido/mora), plan, fecha de creacion, pais.
- **Detalle:** datos institucionales, plan, subdominio, calendario, cuota, estado de pago de la suscripcion.
- **Acciones:** Crear tenant · Suspender / reactivar tenant · Eliminar tenant · Editar subdominio · Cambiar plan.
- Callout importante: eliminar un tenant es irreversible; exige confirmacion fuerte y motivo (queda en log).

**Como se usa este modulo:** cuando un colegio firma contrato, el superadmin crea el tenant, define subdominio y plan, dispara el provisioning del schema y entrega el acceso al primer Rector. (Ver [[Casos de Uso/RF-01 Crear tenant|CU RF-01]] y CU-001 de Logica del negocio.)

### Planes y licencias

- Catalogo de planes (basico / estandar / premium) y que incluye cada uno.
- Asignar / cambiar el plan de un tenant.
- Ver historico de cambios de plan por tenant.

### Calendario A/B

- Ver que calendario tiene habilitado cada tenant.
- Cambiar Calendario A <-> B de un tenant (unico rol que puede — RR-13).
- Callout warning: el cambio de calendario afecta periodos lectivos; exige confirmacion y motivo.

### Almacenamiento y cuotas

- Cuota asignada y consumo real por tenant.
- Ampliar / reducir cuota.
- Alertas cuando un tenant supera el umbral.
- Fuente: `Logica del negocio/11-plataforma-y-operacion/almacenamiento-y-cuotas.md`.

### Backups y restauracion

- Estado del ultimo backup por tenant.
- Disparar backup manual.
- Solicitar restauracion (con doble confirmacion + motivo).
- Fuente: `Logica del negocio/11-plataforma-y-operacion/backups-y-restauracion.md`.

### Log de auditoria global

- Ver logs de TODOS los tenants (la consulta queda auditada — RN-LA-006).
- Filtros: tenant, actor, rol, accion, recurso, rango de fechas, IP.
- Exportar a CSV/JSON (la exportacion queda en meta-auditoria).
- Fuente: `Logica del negocio/11-plataforma-y-operacion/log-de-auditoria.md`.

### Soporte / Impersonacion

- Iniciar sesion de soporte impersonando a un usuario de un tenant (RN-RT-402).
- Requiere: ticket interno, justificacion, expiracion automatica.
- Banner permanente "Impersonando a X" durante toda la sesion.
- Toda accion queda con doble identificador (superadmin real + usuario impersonado).
- Callout importante: el Rector NO puede impersonar; solo este rol.

### Salud del sistema

- Disponibilidad, latencia, errores.
- Estado de integraciones externas (pasarelas, correo, SMS).
- Incidentes abiertos.

---

## Diferencias clave vs otros roles

| Aspecto | Superadmin (ROL-01) | Rector (ROL-02) |
| --- | --- | --- |
| Ambito | Global, cross-tenant | Un solo tenant |
| Entra por | URL de plataforma | Subdominio del colegio |
| Operacion academica | No participa | Acceso total dentro del tenant |
| Calendario A/B | Lo cambia | Solo elige dentro del habilitado |
| Impersonacion | Si (auditada) | No |
| Logs | Globales (todos los tenants) | Solo de su tenant |

---

## Diagrama ASCII general

```
+------------------------------------------------------------------+
| Logo |  Buscador tenants        | Estado | Perfil | Notif         |
+--------+---------------------------------------------------------+
| SIDEBAR|  CONTENIDO                                               |
|        |                                                          |
| Dashbrd|  [ Dashboard global: tarjetas resumen ]                  |
| Tenants|  [ Lista de tenants + filtros + acciones ]               |
| Planes |                                                          |
| Cal A/B|                                                          |
| Almac. |                                                          |
| Backups|                                                          |
| Logs   |                                                          |
| Soporte|                                                          |
| Salud  |                                                          |
+--------+---------------------------------------------------------+
```

---

## Relacionado

- [[01 - Ficha de Rol]]
- [[04 - Permisos Detallados]]
- [[05 - Requerimientos]]
- [[06 - Resumen Rapido]]
- [[03 - PRD]]
- [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente de verdad: `Logica del negocio/02-usuarios-roles-y-permisos/roles/00-superadministrador-plataforma.md`
