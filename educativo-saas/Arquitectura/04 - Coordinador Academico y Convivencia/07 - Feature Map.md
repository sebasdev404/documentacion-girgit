---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - rol/coord-combinado
  - feature-map
aliases:
  - Feature Map ROL-05
---

# Feature Map — Coordinador Academico y Convivencia

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis). Une el feature map del Coord. Academico (ROL-03) y del Coord. de Convivencia (ROL-04) en un solo rol (ROL-05).

```
COORDINADOR ACADEMICO Y CONVIVENCIA (ROL-05)
│
├── PRIMARIAS
│   │
│   ├── Plan de estudios
│   │   ├── Crear / editar / archivar materias por grado (RF-11)
│   │   ├── Asignar intensidad horaria semanal
│   │   └── Asignar area del conocimiento
│   │
│   ├── Grupos y asignaciones
│   │   ├── Crear y gestionar grupos por grado y ano (RF-12)
│   │   ├── Asignar docentes a materias x grupo (RF-13, RR-10)
│   │   └── Designar director de grupo (RF-14, RR-09)
│   │
│   ├── Horarios
│   │   ├── Construir malla horaria por grupo / docente / aula (RF-15)
│   │   ├── Detectar y resolver choques
│   │   └── Publicar horario
│   │
│   ├── Consolidados y cierre
│   │   ├── Ver consolidados por grupo (RF-18)
│   │   ├── Ver consolidado de todos los grupos (RF-19)
│   │   ├── Cierre de periodo academico (RF-20)
│   │   └── Editar nota tras cierre con justificacion (RF-17, RR-07)
│   │
│   ├── Observador del estudiante
│   │   ├── Registrar anotacion en cualquier estudiante (RF-26)
│   │   ├── Definir tipologias de anotacion (RF-27)
│   │   ├── Configurar visibilidad por anotacion (RN-OB-081)
│   │   └── Anular / archivar con justificacion (RN-OE-003)
│   │
│   └── Convivencia (Ley 1620)
│       ├── Recibir y clasificar caso tipo I/II/III (RN-CVE-002)
│       ├── Activar protocolo de la Ruta de Atencion Integral
│       ├── Citar formalmente a acudientes (RF-28)
│       ├── Secretaria tecnica del Comite Escolar de Convivencia
│       └── Escalar tipo III al Rector (RN-CVE-004)
│
└── SECUNDARIAS
    │
    ├── Procesos de recuperacion
    │   ├── Seguimiento de nivelaciones del periodo (RF-21)
    │   ├── Seguimiento de habilitaciones del ano
    │   └── Revision de planes de mejoramiento
    │
    ├── Boletines
    │   └── Aprobar / firmar boletines si el colegio lo habilita (RF-39)
    │
    ├── Reportes y analisis
    │   ├── Reportes de convivencia por estudiante / grupo (RF-29)
    │   └── Informe institucional para auditoria / SIUCE
    │
    └── Comunicaciones
        ├── Citaciones y mensajes dirigidos a acudientes (RF-43)
        └── Recibir notificaciones por correo (RF-44)
```

## Clasificacion

- **Primarias:** los modulos core del sidebar que justifican la existencia del rol combinado — la estructura academica operativa (plan, grupos, horarios, consolidados/cierre) y el seguimiento de convivencia (observador + casos Ley 1620).
- **Secundarias:** capacidades de apoyo y transversales — supervision de procesos de recuperacion, aprobacion de boletines (configurable), reportes/analisis y comunicaciones dirigidas.

## Relacionado

- [[00 - Arquitectura Coordinador Academico y Convivencia|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
