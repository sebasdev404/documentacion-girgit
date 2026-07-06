---
tags:
  - arquitectura
  - rol/director-de-grupo
  - feature-map
aliases:
  - Feature Map ROL-08
---

# Feature Map — Director de Grupo

Mapa de features del complemento agrupadas. La estructura del arbol clasifica (sin colores ni emojis).

> Solo se mapean las features que el complemento **suma** sobre el grupo dirigido. Las features de Docente (notas/asistencia/observador de sus materias) viven en [[../06 - Docente/07 - Feature Map|Feature Map Docente]].

```
DIRECTOR DE GRUPO (ROL-08) — complemento sobre el grupo dirigido
│
├── PRIMARIAS
│   │
│   ├── Consolidado del grupo
│   │   ├── Ver consolidado completo del grupo (todas las materias) (RF-18)
│   │   ├── Consolidado por periodo / acumulado del ano
│   │   └── Descargar consolidado en PDF
│   │
│   ├── Boletines del grupo
│   │   ├── Generar boletines del grupo dirigido (RF-38)
│   │   ├── Agregar observacion general por estudiante (RF-40)
│   │   ├── Aprobar / firmar boletines (configurable) (RF-39)
│   │   └── Descargar boletin en PDF
│   │
│   ├── Observador del grupo
│   │   ├── Registrar anotacion en el observador del grupo (RF-25)
│   │   ├── Adjuntar evidencia
│   │   └── Solicitar confirmacion del acudiente
│   │
│   └── Convivencia (Ley 1620)
│       ├── Reportar situacion de convivencia del grupo
│       ├── Aplicar medidas pedagogicas tipo I en el aula (RN-CVE-003)
│       ├── Marcar presunto delito -> escala al Rector (RN-CVE-004)
│       └── Seguimiento de acuerdos y compromisos
│
└── SECUNDARIAS
    │
    ├── Acompanamiento del grupo
    │   ├── Inicio "Mi grupo dirigido" (tarjetas resumen)
    │   ├── Consultar asistencia completa del grupo (RF-23)
    │   └── Selector de grupo (si dirige varios)
    │
    ├── Alertas y bienestar
    │   └── Visibilidad de remisiones a orientacion (lo que le corresponde)
    │
    └── Relacion con acudientes
        ├── Citar formalmente a acudientes (configurable)
        ├── Comunicacion con acudientes via portal (configurable)
        └── Plantillas de comunicado (boletines, citacion, felicitacion)
```

## Clasificacion

- **Primarias:** modulos core que justifican la existencia del complemento (consolidado, boletines, observador y convivencia del grupo dirigido).
- **Secundarias:** capacidades transversales de acompanamiento, alertas y relacion con acudientes.

## Relacionado

- [[00 - Arquitectura Director de Grupo|Wireframe]]
- [[05 - Requerimientos]]
- [[../06 - Docente/07 - Feature Map|Feature Map Docente (rol base)]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
