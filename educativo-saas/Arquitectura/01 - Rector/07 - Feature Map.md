---
tags:
  - arquitectura
  - rol/rector
  - feature-map
aliases:
  - Feature Map ROL-02
  - Rector Feature Map
---

# Feature Map — Rector / Administrador del Colegio

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis). Las **Primarias** son lo que solo el Rector hace o lidera (configuracion y gobierno del tenant); las **Secundarias** son la operacion que tambien hacen otros roles pero a la que el Rector accede como supervision/respaldo, mas las utilidades transversales.

```
RECTOR / ADMINISTRADOR DEL COLEGIO (ROL-02)
│
├── PRIMARIAS
│   │
│   ├── Configuracion institucional
│   │   ├── Identidad institucional (RF-04)
│   │   ├── Calendario y periodos (RF-05)
│   │   ├── Jornadas y bloques horarios (RF-06)
│   │   ├── Modelo pedagogico por nivel
│   │   ├── Escala valorativa numerica / por imagenes (RF-07)
│   │   └── Metodo de aprobacion y nota minima (RF-08)
│   │
│   ├── Gobierno de usuarios y roles
│   │   ├── Crear / editar / desactivar usuarios (RF-10)
│   │   ├── Asignar roles (RF-09, RR-04)
│   │   ├── Ajustar permisos configurables (RR-05)
│   │   ├── Elegir esquema de coordinacion (separados vs combinado, RR-12)
│   │   └── Renombrar roles
│   │
│   ├── Actos del Rector
│   │   ├── Aprobar / firmar boletines (RF-39)
│   │   ├── Coordinar cierre de periodo academico (RF-20)
│   │   └── Editar notas post-cierre con justificacion (RF-17, RR-07)
│   │
│   └── Auditoria del tenant
│       └── Consultar y exportar logs del colegio (RF-49, RR-03)
│
└── SECUNDARIAS
    │
    ├── Operacion academica (supervision / respaldo)
    │   ├── Plan de estudios, grupos, asignacion, horarios (RF-11 a RF-15)
    │   ├── Notas y consolidados por grupo y total (RF-18, RF-19)
    │   ├── Asistencia y nivelaciones (RF-21 a RF-23)
    │   └── Boletines (generar, observaciones, PDF) (RF-38, RF-40, RF-41)
    │
    ├── Convivencia
    │   ├── Observador del estudiante (RF-24 a RF-26)
    │   ├── Tipologias y citaciones (RF-27, RF-28)
    │   ├── Ruta de atencion Ley 1620
    │   └── Reportes de convivencia (RF-29)
    │
    ├── Secretaria y matricula
    │   ├── Matricula y admisiones (RF-30 a RF-32)
    │   ├── Documentos oficiales (constancias, certificados, paz y salvo) (RF-34 a RF-36)
    │   └── Reporte SIMAT / MEN (RF-37, RR-15)
    │
    ├── Bienestar y servicios
    │   ├── Salud / enfermeria
    │   ├── Bienestar / orientacion escolar
    │   ├── Biblioteca
    │   ├── Transporte escolar
    │   └── Restaurante / comedor
    │
    ├── Financiero
    │   ├── Pensiones y cartera
    │   ├── Becas y descuentos
    │   └── Paz y salvo financiero
    │
    ├── Comunicaciones
    │   ├── Comunicados al colegio entero (RF-42)
    │   └── Mensajeria con acudientes (RF-43)
    │
    └── Reportes y utilidades
        ├── KPIs academicos, de convivencia y financieros
        ├── Reportes oficiales (MEN)
        └── Exportaciones (PDF / CSV)
```

## Clasificacion

- **Primarias:** lo que justifica la existencia del rol: configurar el colegio, gobernar usuarios/roles, ejecutar los actos que requieren su firma y auditar el tenant. Solo el Rector (o un delegado que el habilite) hace esto.
- **Secundarias:** la operacion academica, de convivencia, de bienestar y financiera, que la ejecutan los roles especializados pero a la que el Rector accede con permiso total como supervision y respaldo; mas las utilidades transversales (reportes, exportaciones).

## Relacionado

- [[00 - Arquitectura Rector|Wireframe]]
- [[05 - Requerimientos]]
- [[04 - Permisos Detallados]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
