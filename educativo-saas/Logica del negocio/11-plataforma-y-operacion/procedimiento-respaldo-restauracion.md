---
titulo: Procedimiento de respaldo y restauración
tipo: operacion
estado: pendiente-despliegue
tags: [backup, restore, evidencia]
---

# Procedimiento y evidencia de respaldo/restauración

## Estado al 29 de septiembre de 2026

**No existe todavía evidencia de un sistema automático de respaldos en producción.** La entrega contiene un simulacro reproducible con dos bases temporales PostgreSQL, registros y un archivo sintéticos. No se han respaldado ni restaurado los datos reales de Inmaculada.

| Comprobación local | Resultado |
|---|---|
| `pg_dump` en formato custom y `pg_restore` transaccional | Correcto con PostgreSQL 18 de este equipo |
| Cifrado autenticado de la copia de prueba | Correcto; clave efímera en memoria, sin salida de secretos |
| Rechazo de una copia alterada | Correcto |
| Registros y hash del archivo al restaurar | 2 registros idénticos; SHA-256 coincide |
| Limpieza | Ambas bases temporales y los archivos del simulacro eliminados |
| Duración de esta prueba mínima | 1,93 segundos; **no es una medición de RTO del producto** |

Evidencia: [simulacro ejecutable](../../../../colegio-saas-backend/tests/Support/backup-restore-drill.php). Desde el backend en este equipo:

```powershell
php tests/Support/backup-restore-drill.php --run '--pg-bin=C:\Program Files\PostgreSQL\18\bin'
```

Requiere conexión central PostgreSQL y privilegio para crear bases de prueba; obtiene la contraseña de la configuración del servidor, no de argumentos. Los nombres se generan con el prefijo `restore_probe_`; el script no recibe un nombre de base a restaurar o eliminar. Usar la versión de herramientas compatible con el servidor. La clave de cifrado de esta prueba es desechable: no es el sistema de custodia productivo.

## Trabajo P0 antes de operar con datos reales

| Trabajo | Responsable de ejecución | Evidencia de cierre |
|---|---|---|
| Inventario de bases, archivos y metadatos centrales necesarios para recuperar un colegio y sus sedes | Operación + backend | Manifiesto por tenant; correspondencia entre archivos, sus referencias y colegio; no mezclar datos de otro tenant |
| Copia consistente BD/archivos | Backend + operación | Trabajo repetible, versión de esquema, instante de corte, hashes y conteos; evitar copia de archivos durante escrituras sin coordinación |
| Copia cifrada diaria y retención | Operación | Historial de ejecuciones, eliminación por política y prueba de recuperación con una copia retenida |
| Almacenamiento secundario y custodia de claves | Operación | Accesos mínimos, clave separada de las copias y de las credenciales del VPS; prueba de recuperación de clave; destino contratado y comprobado |
| PITR/WAL o snapshots horarios | Operación | Recuperación al instante solicitado; imprescindible para sostener el objetivo RPO ≤1 h, que una copia diaria no satisface |
| Supervisión | Operación | Alertas por fallo, copia ausente, antigüedad, espacio y verificación fallida; responsable y canal comprobados |
| Restore completo de tenant de prueba | Backend + operación | Base nueva, archivos, logo, acceso, permisos, conteos, muestras y aislamiento correctos con volumen representativo |
| Ensayo trimestral | Operación | Acta con tiempos, incidencias y evidencia; resumen disponible al cliente bajo solicitud |

## Restauración productiva: secuencia obligatoria

1. Registrar solicitud, tenant exacto, motivo, instante, solicitante, autorización del cliente cuando corresponda y ejecutor. Determinar impacto en la base central y sedes.
2. Seleccionar copia y claves autorizadas. Verificar cifrado, integridad, versión y pertenencia antes de usarla.
3. Restaurar primero en **base y almacenamiento nuevos y aislados**. No sobrescribir el colegio activo. Bloquear salida de correos, pagos y tareas automáticas en ese entorno.
4. Comparar conteos, relaciones, archivos y muestras; revisar datos recientes ausentes desde el punto de recuperación. Probar login, RBAC y acceso entre tenants.
5. Obtener aceptación del resultado concreto. Fijar ventana, mantenimiento, respaldo previo al cambio y plan de reversión con responsables.
6. Realizar el cambio controlado de conexión/almacenamiento; revocar sesiones restauradas y regenerar cachés. Validar acceso y datos.
7. Auditar resultado, duración, pérdida de datos medida y desviaciones frente al RPO/RTO. Conservar evidencia y copia previa según retención.

**Pendientes de infraestructura:** proveedor/destino secundario, claves, política de retención ejecutable, WAL/snapshots, programación y alertas. La otra región/proveedor sigue como objetivo; la hipótesis de almacenamiento secundario en el mismo proveedor no permite afirmar recuperación ante pérdida regional. No hay fecha de cumplimiento hasta desplegar y medir.

Referencias: [[backups-y-restauracion]], [[../../Arquitectura/_Globales/11 - Matriz de Verificacion|AC-20 y prioridades]].
