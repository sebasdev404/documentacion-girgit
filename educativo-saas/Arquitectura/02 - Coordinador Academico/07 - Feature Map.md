---
tags:
  - arquitectura
  - rol/coord-academico
  - feature-map
aliases:
  - Feature Map ROL-03
---

# Feature Map — Coordinador Academico

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis).

```
COORDINADOR ACADEMICO (ROL-03)
│
├── PRIMARIAS
│   │
│   ├── Plan de estudios
│   │   ├── Crear materia por grado (RF-11)
│   │   ├── Definir area e intensidad horaria
│   │   ├── Editar materia
│   │   └── Archivar materia
│   │
│   ├── Grupos
│   │   ├── Crear grupo por grado y ano lectivo (RF-12)
│   │   ├── Editar grupo (jornada, nombre)
│   │   └── Archivar grupo
│   │
│   ├── Asignacion docente
│   │   ├── Asignar docente a materia/grupo (RF-13)
│   │   ├── Reasignar docente
│   │   └── Designar director de grupo (RF-14, RR-09)
│   │
│   ├── Horarios
│   │   ├── Crear / editar bloque horario (RF-15)
│   │   ├── Validar cruces (docente / aula / grupo)
│   │   └── Publicar horario
│   │
│   └── Cierre de periodo
│       ├── Validar consolidados por grupo (RF-20)
│       ├── Activar cierre del periodo
│       └── Desactivar / reabrir cierre (segun config.)
│
└── SECUNDARIAS
    │
    ├── Seguimiento academico
    │   ├── Ver consolidado por grupo (RF-18)
    │   ├── Ver consolidado de todos los grupos (RF-19)
    │   └── Detectar estudiantes en riesgo / materias perdidas
    │
    ├── Notas y boletines
    │   ├── Editar notas / editar tras cierre (configurable, RF-17, RR-07)
    │   ├── Generar boletin del grupo (RF-39 relacionado)
    │   └── Aprobar / firmar boletines (configurable, RF-39)
    │
    ├── Nivelaciones
    │   ├── Abrir proceso de nivelacion / habilitacion (RF-21)
    │   └── Registrar resultado
    │
    └── Comunicaciones
        ├── Enviar comunicado academico (configurable)
        └── Mensajear acudientes via portal (configurable, RF-43)
```

## Clasificacion

- **Primarias:** modulos core del sidebar que justifican la existencia del rol (estructura academica operativa: plan, grupos, asignacion, horarios, cierre).
- **Secundarias:** capacidades de seguimiento, notas/boletines, nivelaciones y comunicaciones — varias de ellas configurables por el colegio.

## Relacionado

- [[00 - Arquitectura Coordinador Academico|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
