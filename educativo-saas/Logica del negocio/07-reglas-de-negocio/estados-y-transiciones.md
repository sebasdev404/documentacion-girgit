---
titulo: Estados y transiciones
modulo: reglas-de-negocio
tipo: regla
estado: borrador
tags: [estados, transiciones, maquinas-de-estado]
---

# Estados y transiciones

Catálogo de máquinas de estado del sistema. Cada entidad clave tiene un conjunto definido de estados y transiciones permitidas.

## Convención

```
Estado origen → Estado destino  (Evento que dispara la transición)
```

## Por entidad

### Usuario

```
Invitado → Activo            (acepta invitación y completa onboarding)
Invitado → Expirado          (no acepta dentro del plazo)
Activo  → Suspendido         (decisión del administrador, o intentos fallidos)
Suspendido → Activo          (reactivación por administrador)
Activo  → Inactivo            (auto-desactivación por inactividad prolongada)
Activo / Suspendido / Inactivo → Archivado  (al cerrar año; no borra histórico)
```

### Tenant (colegio)

```
Provisionando → Trial → Activo → Suspendido (mora) → Activo
                                              → Cancelación solicitada
Cancelación solicitada → Finalizado → En retención → Eliminado
```

### Suscripción

```
Trial → Activa → Suspendida → Activa
              → Cancelada solicitada → Finalizada
```

### Matrícula

```
Borrador → Pre-matrícula → Documentos pendientes → Documentos aprobados → Pago realizado → Matrícula confirmada
                                                                                                          → Anulada (con motivo)
Matrícula confirmada → Activa (durante el año lectivo)
Activa → Retirada (con motivo)
Activa → Egresada (al finalizar grado terminal)
Activa → No promovida (al cierre, si reprueba)
```

### Pago / cuota

```
Pendiente → En proceso → Confirmado
         → En proceso → Rechazado → Pendiente
Pendiente → Vencido → En mora → Pagado parcial (acuerdo)
Confirmado / En mora → Anulado (nota crédito)
```

### Calificación por periodo

```
Borrador (en captura por docente) → Cerrada del periodo → Publicada
Cerrada → Reabierta excepcionalmente → Cerrada nuevamente
Publicada → Recuperación abierta (nivelación) → Recuperación cerrada
```

### Comunicado

```
Borrador → Programado → Enviado
         → Cancelado (antes del envío)
Enviado → Archivado (con motivo, conserva histórico)
```

### Observación disciplinaria

```
Registrada → Notificada al acudiente → Confirmada por acudiente
Registrada → En revisión (apelación) → Mantenida / Modificada / Retirada (con motivo)
```

### Año lectivo

```
Programado → Activo → En proceso de cierre → Cerrado
Cerrado → Reabierto excepcionalmente → Cerrado nuevamente
```

## Eventos que disparan transiciones

| Evento | Transición |
| --- | --- |
| Pago de pensión confirmado por la pasarela | `Pendiente → Confirmado` |
| Vencimiento de fecha límite ordinaria | `Pendiente → Vencido` |
| Inactividad superior a 90 días en cuenta de docente | `Activo → Inactivo` |
| 5 intentos fallidos de login | `Activo → Suspendido` |
| Cierre de periodo académico | `Borrador → Cerrada del periodo` |
| Publicación de boletines del periodo | `Cerrada → Publicada` |
| Falta de pago al día del cobro al colegio | `Activa → Suspendida` (suscripción) |
| Aceptación de invitación por el usuario | `Invitado → Activo` |

## Reglas de transición

- **RN-ET-001 — Auditoría obligatoria:** toda transición queda en el [[../11-plataforma-y-operacion/log-de-auditoria|log]] con actor, motivo (cuando aplica), valor previo y nuevo.
- **RN-ET-002 — No retroactividad:** una transición no se puede aplicar con fecha pasada salvo procesos específicos auditados (corrección académica con acta).
- **RN-ET-003 — Estados terminales:** estados como `Eliminado` o `Egresada` no transicionan de regreso.
- **RN-ET-004 — Permisos por transición:** cada transición requiere un rol con el permiso correspondiente.

## Notas y pendientes

- Validar si conviene formalizar las máquinas de estado en código (con librería de FSM) o solo a nivel lógico.
- Documentar diagramas en formato visual (PlantUML / Mermaid) en una entrega futura.
