---
tags:
  - arquitectura
  - prd
aliases:
  - PRD-01
  - PRD Plataforma
---

# PRD - Plataforma

| Campo | Valor |
|---|---|
| ID PRD | PRD-01 |
| HU | Plataforma SaaS de Gestion Academica |
| Funcionalidad | Gestion academica integral de un colegio privado |
| Actor Principal | Multiples (ver tabla de actores) |
| Dispositivo | Web responsive (desktop + mobile) |
| Estado | Borrador |
| Version | 0.1 |

---

## Objetivo

Proveer una plataforma SaaS multi-tenant que permita a colegios privados de Colombia gestionar la totalidad de su operacion academica y convivencia escolar: matricula, calendarios, jornadas, planes de estudio, asignacion docente, registro de notas y asistencia, observador disciplinario, boletines, comunicacion con padres, pagos de pensiones, facturacion y reporte oficial al SIMAT.

---

## Alcance

### Incluye

- Multi-tenant: un colegio = un schema independiente.
- Configuracion institucional por colegio (calendario A/B, jornadas, escala valorativa, modelo pedagogico).
- Gestion completa de matricula, asistencia, notas, boletines, disciplina.
- Comunicacion interna y con acudientes.
- Pagos de pensiones y suscripcion del SaaS.
- Reporte SIMAT.
- Portal de consulta para estudiantes y acudientes.
- Auditoria de acciones sensibles.

### Fuera del alcance

- LMS / cursos online / contenido educativo (este SaaS NO es Moodle ni Canvas).
- Lecciones, ejercicios o evaluaciones online.
- Tienda de cursos / marketplace.

---

## Flujo General

```
Superadmin crea tenant
        |
        v
Rector recibe acceso, configura colegio
        |
        v
Coordinadores configuran plan de estudios + grupos + horarios
        |
        v
Secretaria matricula estudiantes y vincula acudientes
        |
        v
Docentes operan dia a dia: notas, asistencia, observaciones
        |
        v
Estudiantes / Acudientes consultan portal
```

---

## Actores

| Actor | Tipo | Responsabilidad principal |
|---|---|---|
| Superadministrador de la Plataforma | Humano (interno SaaS) | Provisionar y mantener tenants |
| Rector / Administrador del Colegio | Humano (directivo) | Configurar y administrar el colegio |
| Coordinador Academico | Humano (directivo) | Estructura academica operativa |
| Coordinador de Convivencia | Humano (directivo) | Seguimiento disciplinario |
| Coordinador Combinado | Humano (directivo) | Ambos coordinaciones unidas |
| Secretaria Academica | Humano (administrativo) | Procesos administrativos |
| Docente | Humano (operativo) | Operacion de aula |
| Director de Grupo | Humano (operativo + complemento) | Acompanamiento de grupo |
| Estudiante / Acudiente | Humano (consulta) | Consulta de datos propios |
| Sistema | Automatizacion | Tareas programadas, notificaciones, calculos |

---

## Restricciones / Reglas aplicables

Las reglas transversales del proyecto estan en [[07 - Reglas de Negocio]]. En particular:

- **RR-01** Aislamiento total entre tenants.
- **RR-02** Verificacion de permisos en frontend y backend.
- **RR-03** Auditoria obligatoria de acciones sensibles.
- **RR-04** Asignacion de roles por el rector.
- **RR-05** Configurabilidad acotada de permisos.
- **RR-06** Acceso al sistema solo por subdominio del colegio.

Origen: `Logica del negocio/02-usuarios-roles-y-permisos/reglas-transversales-de-roles.md`.

---

## Integraciones (RI)

| ID | Integracion | Descripcion |
|---|---|---|
| RI-01 | Pasarelas de pago | Para pago de pensiones y suscripcion |
| RI-02 | SIMAT (MEN Colombia) | Reporte oficial de matricula |
| RI-03 | Correo electronico | Notificaciones a usuarios |
| RI-04 | SMS | Notificaciones criticas opcionales |
| RI-05 | Facturacion electronica DIAN | Emision de facturas y recibos |
| RI-06 | Almacenamiento en la nube | Documentos, archivos, evidencias |
| RI-07 | SSO (opcional) | Login con Google / Microsoft |

---

## Dependencias

Ver [[09 - Dependencias]] para el detalle completo.

Resumen:
- **Internas:** modulos de Logica del Negocio (matricula, notas, asistencia, etc.).
- **Externas:** pasarelas de pago, SIMAT, proveedores de correo/SMS, DIAN, almacenamiento.
- **Catalogos:** escalas valorativas, modelos pedagogicos, calendarios A/B, jornadas.
