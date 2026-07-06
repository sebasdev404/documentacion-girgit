---
tags:
  - arquitectura
  - rol/coordinador-de-convivencia
  - feature-map
aliases:
  - Feature Map ROL-04
  - Coord. Convivencia Feature Map
---

# Feature Map — Coordinador de Convivencia

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis).

```
COORDINADOR DE CONVIVENCIA (ROL-04)
│
├── PRIMARIAS
│   │
│   ├── Observador del estudiante
│   │   ├── Registrar anotacion en cualquier estudiante (RF-26)
│   │   ├── Elegir tipo y nivel de visibilidad (RN-OB-081)
│   │   ├── Editar anotacion propia dentro del periodo
│   │   ├── Anular anotacion con justificacion (RN-OE-003)
│   │   ├── Cerrar / archivar anotacion
│   │   └── Solicitar confirmacion al acudiente
│   │
│   ├── Casos de convivencia (Ley 1620)
│   │   ├── Recibir y clasificar tipo I/II/III (RN-CVE-002)
│   │   ├── Reclasificar con justificacion
│   │   ├── Instanciar protocolo y ejecutar actuaciones (RN-CVE-003)
│   │   ├── Activar atencion en salud prioritaria (RN-CVE-005)
│   │   ├── Escalar tipo III al Rector (RN-CVE-004)
│   │   ├── Registrar acuerdos y compromisos
│   │   └── Seguimiento y cierre del caso
│   │
│   ├── Tipologias y catalogos
│   │   ├── Definir tipologias de anotacion (RF-27)
│   │   ├── Categorias custom del colegio (RN-OB-080)
│   │   └── Catalogo de medidas restaurativas/pedagogicas
│   │
│   └── Comite Escolar de Convivencia
│       ├── Secretaria tecnica del comite
│       ├── Registrar integrantes por ano (RN-CVE-001)
│       ├── Convocar sesion
│       └── Preparar acta para firma del Rector (RN-CVE-006)
│
└── SECUNDARIAS
    │
    ├── Citaciones
    │   └── Citar formalmente a acudientes (RF-28, configurable)
    │
    ├── Reportes y analisis
    │   ├── Reporte de convivencia por estudiante / grupo / tipo (RF-29)
    │   ├── Informe disciplinario consolidado multi-ano (PDF)
    │   └── Dashboard de convivencia
    │
    ├── Articulacion
    │   ├── Recibir remisiones de Bienestar / Orientacion (config)
    │   └── Coordinar con directores de grupo
    │
    └── Comunicacion
        ├── Comunicados de convivencia (configurable)
        └── Mensajes a acudientes via portal (configurable)
```

## Clasificacion

- **Primarias:** modulos core del sidebar que justifican la existencia del rol (gestion del observador, operacion de la Ley 1620, tipologias y comite de convivencia).
- **Secundarias:** capacidades transversales de citaciones, reportes/analisis, articulacion con otras areas y comunicacion. Varias son configurables por el colegio (RR-05).

## Relacionado

- [[00 - Arquitectura Coordinador de Convivencia|Wireframe]]
- [[05 - Requerimientos]]
- [[04 - Permisos Detallados]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
