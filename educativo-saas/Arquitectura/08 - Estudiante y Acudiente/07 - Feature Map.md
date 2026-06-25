---
tags:
  - arquitectura
  - rol/estudiante-y-acudiente
  - rol/estudiante-acudiente
  - feature-map
aliases:
  - Feature Map ROL-09
  - Estudiante y Acudiente Feature Map
---

# Feature Map — Estudiante / Acudiente

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis).

```
ESTUDIANTE / ACUDIENTE (ROL-09)
│
├── PRIMARIAS
│   │
│   ├── Notas
│   │   ├── Consultar notas por materia y periodo (RF-45)
│   │   ├── Ver observaciones academicas del docente
│   │   └── Ver promedio y consolidado del periodo
│   │
│   ├── Horario
│   │   └── Consultar horario semanal del grupo (RF-46)
│   │
│   ├── Asistencia
│   │   ├── Consultar registro de asistencia (RF-23)
│   │   └── Justificar inasistencia (queda pendiente, RN-PE-005)
│   │
│   ├── Boletines
│   │   ├── Consultar boletines por periodo (RF-47)
│   │   ├── Confirmar boletin digitalmente (RN-PE-004)
│   │   └── Descargar boletin en PDF (RF-41, configurable, RN-PE-003)
│   │
│   └── Pagos y estado de cuenta
│       ├── Consultar estado de cuenta e historial
│       ├── Pagar pension y otros conceptos (RN-PP-003)
│       └── Descargar comprobante (RN-PP-006)
│
└── SECUNDARIAS
    │
    ├── Convivencia
    │   ├── Consultar observador (RF-48, configurable, RN-OB-081)
    │   └── Confirmar anotaciones que lo requieran
    │
    ├── Comunicaciones
    │   ├── Leer comunicados y agenda con alcance al estudiante
    │   ├── Mensajeria con docentes/coordinacion (RF-43, configurable, RN-MI-180)
    │   ├── Recibir notificaciones por correo (RF-44, configurable)
    │   └── Ajustar preferencias de notificacion (RN-NO-004)
    │
    ├── Documentos
    │   ├── Cargar documentos requeridos de matricula (RF-32, RN-GD-270)
    │   ├── Solicitar constancia de estudio (RF-34)
    │   ├── Solicitar certificado de notas (RF-35)
    │   └── Solicitar paz y salvo (RF-36, RN-PYS-150)
    │
    ├── Citas
    │   └── Solicitar cita con docente o coordinacion
    │
    └── Cuenta y acceso
        ├── Selector multi-estudiante (RR-14, RN-CP-002)
        ├── Cambio de contrasena (RN-AU-360)
        └── Perfil y datos de contacto (solo lectura academica)
```

## Clasificacion

- **Primarias:** los modulos de consulta y autogestion que justifican el portal — notas, horario, asistencia, boletines y pagos. Son lo que el acudiente abre el dia a dia.
- **Secundarias:** capacidades de soporte y excepcion — convivencia (observador), comunicaciones, documentos, citas y gestion de la propia cuenta. Varias son configurables por el colegio.

## Relacionado

- [[00 - Arquitectura Estudiante y Acudiente|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
