---
tags:
  - arquitectura
  - rol/secretaria-academica
  - feature-map
aliases:
  - Feature Map ROL-06
  - Secretaria Feature Map
---

# Feature Map — Secretaria Academica

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis).

```
SECRETARIA ACADEMICA (ROL-06)
│
├── PRIMARIAS
│   │
│   ├── Estudiantes
│   │   ├── Crear estudiante (RF-30)
│   │   ├── Editar estudiante
│   │   ├── Editar datos de acudiente operativo (RR-11)
│   │   └── Adjuntar consentimiento de habeas data (RN-HD-001)
│   │
│   ├── Matricula
│   │   ├── Asignar estudiante a grupo (RF-31)
│   │   ├── Cambiar grupo post-matricula (configurable)
│   │   └── Marcar matricula completada
│   │
│   ├── Documentos de matricula
│   │   ├── Cargar documento (RF-32)
│   │   ├── Marcar recibido / pendiente
│   │   └── Definir documentos requeridos por grado
│   │
│   ├── Documentos oficiales
│   │   ├── Generar constancia de estudio (RF-34)
│   │   ├── Generar certificado de notas (RF-35, solo lectura del consolidado)
│   │   ├── Emitir paz y salvo (RF-36)
│   │   └── Bloqueo de emision por pendientes (RF-33, RR-08)
│   │
│   └── SIMAT / Reportes MEN
│       ├── Generar archivo SIMAT (RF-37, RR-15)
│       ├── Validar antes de exportar (RN-MO-004)
│       └── Marcar reporte como enviado
│
└── SECUNDARIAS
    │
    ├── Cumplimiento
    │   ├── Habeas Data / consentimientos (RN-HD-001..006)
    │   └── Revocatoria de autorizaciones
    │
    ├── Comunicaciones (configurables)
    │   ├── Mensajes con acudientes via portal
    │   └── Comunicados administrativos al colegio
    │
    ├── Trazabilidad
    │   ├── Consecutivos de documentos (RN-GD-001)
    │   └── Historial de cambios de un registro (configurable, RR-03)
    │
    └── Utilidades
        ├── Buscador de estudiantes
        ├── Descargar / reimprimir PDF
        └── Tarjetas de resumen en Inicio
```

## Clasificacion

- **Primarias:** modulos core del sidebar que justifican la existencia del rol (matricula, documentos de matricula, documentos oficiales y reporte SIMAT).
- **Secundarias:** capacidades transversales de cumplimiento, comunicaciones configurables, trazabilidad y utilidades.

## Relacionado

- [[00 - Arquitectura Secretaria Academica|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
