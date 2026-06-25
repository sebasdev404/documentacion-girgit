---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - feature-map
aliases:
  - Feature Map ROL-12
---

# Feature Map — Personal de Apoyo

Mapa de features agrupadas. La estructura del arbol clasifica (sin colores ni emojis). Las features de modulo de servicio solo aplican al **perfil** correspondiente (`RN-TU-004`).

```
PERSONAL DE APOYO (ROL-12)
│
├── PRIMARIAS
│   │
│   ├── Ficha acotada del estudiante  (nucleo comun)
│   │   ├── Buscar por nombre / documento / grupo
│   │   ├── Ver identificacion, grupo y contacto del acudiente (RN-TU-006)
│   │   └── Ver alertas basicas (alertas tempranas RN-VA-101 si el colegio lo activa)
│   │
│   ├── Aportes al observador  (nucleo comun)
│   │   ├── Crear anotacion con visibilidad RN-OB-081
│   │   ├── Visibilidad por defecto interna (RN-TU-005)
│   │   └── Editar aporte propio (sin borrar el original)
│   │
│   ├── Bienestar y orientacion  (perfil Orientador, RN-BW)
│   │   ├── Expediente de bienestar (transversal al ano, RN-BW-001)
│   │   ├── Agendar / reprogramar cita (sin motivo sensible, RN-BW-006)
│   │   ├── Nota de seguimiento (default interna, RN-BW-004)
│   │   ├── Plan de acompanamiento (parte visible + interna, RN-BW-008)
│   │   └── Remision interna / externa (consentimiento, RN-BW-005)
│   │
│   ├── Salud y enfermeria  (perfil Enfermeria, RN-SA)
│   │   ├── Consultar ficha medica (RN-SA-002)
│   │   ├── Registrar atencion inmutable (RN-SA-004)
│   │   ├── Suministrar medicamento con autorizacion vigente (RN-SA-003)
│   │   ├── Control de vacunas (RN-SA-009)
│   │   └── Remision a centro medico (RN-SA-006)
│   │
│   └── Biblioteca  (perfil Bibliotecario, RN-BI)
│       ├── Catalogar material y ejemplares
│       ├── Prestamo sobre ejemplar concreto (RN-BI-001)
│       ├── Devolucion y multa (RN-BI-005)
│       ├── Reservas por cola (RN-BI-008)
│       └── Inventario y conciliacion (RN-BI-010)
│
└── SECUNDARIAS
    │
    ├── Agenda / bandeja
    │   ├── Mis citas / atenciones / prestamos
    │   └── Recordatorios y confirmaciones de lectura
    │
    ├── Remisiones
    │   ├── Remision interna a coordinacion u otro perfil
    │   └── Sin decision sobre el estudiante (RN-TU-010)
    │
    ├── Comunicacion
    │   ├── Notificaciones de cita / remision / vencimiento (RF-44)
    │   └── Mensaje al acudiente via portal si el colegio lo habilita (RF-43)
    │
    └── Trazabilidad
        └── Auditoria de cada consulta y aporte (RN-TU-009, RR-03)
```

## Clasificacion

- **Primarias:** la consulta de la ficha acotada, el aporte al observador y el modulo de servicio del perfil — justifican la existencia del rol.
- **Secundarias:** capacidades transversales de agenda, remision, comunicacion y trazabilidad.

## Relacionado

- [[00 - Arquitectura Personal de Apoyo|Wireframe]]
- [[05 - Requerimientos]]
- [[../_Globales/04 - Por Modulo|Por Modulo]]
