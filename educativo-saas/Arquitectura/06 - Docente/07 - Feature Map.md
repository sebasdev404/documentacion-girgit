---
tags:
  - arquitectura
  - rol/docente
  - feature-map
aliases:
  - Feature Map ROL-07
---

# Feature Map — Docente

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis).

```
DOCENTE (ROL-07)
│
├── PRIMARIAS
│   │
│   ├── Notas
│   │   ├── Registrar nota en materia asignada (RF-16)
│   │   ├── Editar nota dentro del periodo abierto (RR-07)
│   │   ├── Recalculo automatico del acumulado del estudiante
│   │   └── Cargar evidencia de evaluacion (configurable)
│   │
│   ├── Asistencia
│   │   ├── Registrar asistencia en clase propia (RF-22)
│   │   ├── Estados Presente / Ausente / Tarde / Excusa
│   │   └── Editar registro del dia
│   │
│   ├── Observador academico
│   │   ├── Registrar observacion academica en su materia (RF-24)
│   │   └── Editar la propia mientras este abierta
│   │
│   └── Mis grupos y estudiantes
│       ├── Ver listado de estudiantes de sus grupos (RR-10)
│       └── Ficha minima del estudiante (su materia)
│
└── SECUNDARIAS
    │
    ├── Consulta
    │   ├── Inicio: mis clases de hoy
    │   └── Mi horario (solo lectura, RF-46)
    │
    ├── Bienestar
    │   ├── Ver alertas de salud autorizadas (RN-SA-007)
    │   └── Remitir estudiante a enfermeria
    │
    ├── Convivencia
    │   ├── Reportar situacion observada en aula (no clasifica)
    │   └── Marcar presunto delito -> escala al Rector (RN-CVE-004)
    │
    └── Comunicacion
        ├── Mensajes con acudientes via portal (configurable, RF-43)
        └── Recibir notificaciones por correo (RF-44)
```

## Clasificacion

- **Primarias:** los modulos core del sidebar que justifican la existencia del rol: notas, asistencia, observador academico y la lista de estudiantes de sus grupos. Es la operacion diaria del aula.
- **Secundarias:** capacidades transversales de consulta (home, horario), bienestar (alertas y remision a enfermeria), reporte de convivencia y comunicacion. Varias dependen de que el colegio active el modulo correspondiente.

## Relacionado

- [[00 - Arquitectura Docente|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
