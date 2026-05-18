---
tags:
  - arquitectura
  - rol/superadmin
  - feature-map
aliases:
  - Feature Map ROL-01
---

# Feature Map — Superadministrador de la Plataforma

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis).

```
SUPERADMINISTRADOR DE LA PLATAFORMA (ROL-01)
│
├── PRIMARIAS
│   │
│   ├── Tenants
│   │   ├── Crear tenant (RF-01)
│   │   ├── Provisioning de schema + semillas
│   │   ├── Suspender / reactivar tenant
│   │   ├── Eliminar tenant (irreversible, con motivo)
│   │   └── Editar subdominio
│   │
│   ├── Planes y licencias
│   │   ├── Asignar plan al tenant (RF-02)
│   │   ├── Cambiar plan
│   │   └── Historico de planes por tenant
│   │
│   ├── Calendario A/B
│   │   └── Cambiar Calendario A <-> B del tenant (RF-03, RR-13)
│   │
│   └── Almacenamiento y cuotas
│       ├── Ver consumo por tenant
│       ├── Ampliar / reducir cuota
│       └── Alertas de umbral
│
└── SECUNDARIAS
    │
    ├── Observabilidad
    │   ├── Dashboard global
    │   ├── Salud del sistema (disponibilidad, latencia, errores)
    │   └── Estado de integraciones externas
    │
    ├── Auditoria
    │   ├── Log de auditoria global (RF-50)
    │   ├── Filtros y busqueda
    │   └── Exportacion CSV/JSON (meta-auditada)
    │
    ├── Operacion
    │   ├── Backups (estado, manual, restauracion)
    │   └── Histórico y tenants cerrados
    │
    └── Soporte
        └── Impersonacion auditada (RN-RT-402)
```

## Clasificacion

- **Primarias:** modulos core del sidebar que justifican la existencia del rol (gestion del ciclo de vida del tenant).
- **Secundarias:** capacidades transversales de observabilidad, auditoria, operacion y soporte.

## Relacionado

- [[00 - Arquitectura Superadministrador de la Plataforma|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
