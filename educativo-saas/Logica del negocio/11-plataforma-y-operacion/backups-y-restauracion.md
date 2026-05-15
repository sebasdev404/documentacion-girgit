---
titulo: Backups y restauración
modulo: 11-plataforma-y-operacion
tipo: proceso
estado: borrador
tags: [backup, restore, disaster-recovery, operacion]
---

# Backups y restauración

## Descripción

Estrategia de respaldo, retención y restauración de los datos de la plataforma, diseñada para soportar fallos operativos, errores humanos y recuperación de desastres.

## Estrategia de backups

| Tipo | Frecuencia | Retención | Ubicación |
| --- | --- | --- | --- |
| Backup completo | Semanal. | 12 semanas. | Bucket / almacenamiento secundario en otra región. |
| Backup incremental | Diario. | 30 días. | Bucket / almacenamiento secundario. |
| Snapshot de base de datos | Cada hora (configurable). | 7 días. | Almacenamiento del proveedor cloud. |
| WAL / log de transacciones | Continuo. | 7 días. | Almacenamiento del proveedor cloud. |
| Backup de archivos (storage del tenant) | Diario incremental + semanal completo. | 30 / 90 días. | Bucket secundario en otra región. |

Los rangos exactos pueden ajustarse por plan o por colegio.

## Aislamiento por tenant

- Cada tenant (colegio) tiene su propia BD y su propio bucket de archivos (ver [[../03-multi-tenancy/aislamiento-de-datos|Aislamiento de datos]]).
- Los backups respetan el aislamiento: una restauración de un tenant no afecta a los demás.

## Restauración

| Tipo de restauración | Quién la dispara | Objetivo |
| --- | --- | --- |
| Point-in-time del tenant | Equipo de operación (con aprobación del cliente). | Volver a un instante específico. |
| Restauración de un registro borrado (soft-delete) | Administrador del colegio. | Recuperar un registro eliminado que esté en estado lógico borrado. |
| Restauración masiva del tenant | Equipo de operación. | Recuperar todo el tenant tras un incidente. |
| Restauración de un archivo | Administrador del colegio. | Recuperar un archivo eliminado. |
| Recuperación de desastres (DR) | Equipo de operación. | Restablecer la plataforma completa en otra región. |

## Métricas objetivo

| Métrica | Objetivo |
| --- | --- |
| RPO (Recovery Point Objective) | ≤ 1 hora. |
| RTO (Recovery Time Objective) | ≤ 4 horas para incidentes acotados; ≤ 24 horas para DR completo. |

## Borrado lógico vs físico

- Las eliminaciones desde la aplicación son **lógicas** (soft delete) por defecto.
- El borrado físico se ejecuta tras la ventana de retención configurada.
- Esto permite recuperar registros eliminados accidentalmente sin necesidad de restaurar un backup.

## Pruebas periódicas

- Restauración de prueba cada **trimestre** sobre un entorno aislado.
- Validación de integridad: hashes y conteos de registros.
- Reporte interno con resultados y tiempos.

## Acceso a backups

- Solo el equipo de operación de la plataforma tiene acceso al sistema de backups.
- Toda restauración productiva queda registrada en el [[log-de-auditoria|log de auditoría]] y, cuando aplica, requiere aprobación documentada del cliente.
- Los backups están cifrados en reposo.

## Reglas de negocio

- **RN-BR-001 — Aislamiento de backup:** un backup pertenece a un único tenant; no se mezcla con otros.
- **RN-BR-002 — Cifrado en reposo:** todos los backups están cifrados.
- **RN-BR-003 — Restauración auditada:** toda restauración productiva queda en el log, con quién la solicitó, autorizó y ejecutó.
- **RN-BR-004 — RPO / RTO comprometido:** la plataforma cumple los RPO / RTO publicados; cualquier desviación se reporta.
- **RN-BR-005 — Soft delete por defecto:** las eliminaciones desde la app son lógicas, recuperables dentro de la ventana de retención.

## Notas y pendientes

- **[Decisión tomada]** **Almacenamiento secundario de backups**: queda como **decisión de infraestructura pendiente**. Hipótesis inicial: la plataforma opera sobre **VPS Linux** y los respaldos se almacenan en almacenamiento secundario **dentro del mismo proveedor o región**, dejando abierta la incorporación de un **proveedor o región adicional** en fases futuras según crecimiento y requerimientos de resiliencia.
- **[Decisión tomada]** **Pruebas de restauración** se realizan **trimestralmente** con registro interno; el **reporte resumido** queda **disponible al cliente bajo solicitud**. Regla: **RN-BR-260 — Pruebas trimestrales de restauración con reporte bajo solicitud**.
