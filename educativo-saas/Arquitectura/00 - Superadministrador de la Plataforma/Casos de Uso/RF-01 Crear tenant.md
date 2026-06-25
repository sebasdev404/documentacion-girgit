---
tags:
  - arquitectura
  - rol/superadmin
  - caso-de-uso
aliases:
  - CU RF-01
---

# ID: RF-01
**Nombre:** Crear tenant

**Historia:**
Un colegio nuevo contrata la plataforma. El Superadministrador de la Plataforma da de alta el tenant para que el colegio empiece a configurarse. Es el punto de entrada de todo el ciclo de vida del colegio en el SaaS y debe dejar al rector listo para operar con credenciales propias y aislamiento total frente a otros tenants.

**Criterios de aceptacion:**
Al crear el tenant, el sistema provisiona automaticamente una base de datos exclusiva, un subdominio `<slug>.<dominio>` y un usuario administrador (rector) con contrasena temporal autogenerada (`RN-OB-001`, `RN-OB-002`, `RN-AU-001`). El correo institucional recibe la URL y las credenciales. El tenant queda en estado `Configurando` hasta que el rector complete la configuracion minima obligatoria, momento en que pasa a `Activo`. Ningun dato es visible para otros tenants (`RR-01`) y la creacion queda registrada en el log de auditoria (`RR-03`).

**Documentacion:**
- PRD: PRD-02 Superadministrador de la Plataforma
- Flow: Alta de tenant y provisioning
- Prototipo: (link de Figma)

**Flujo:**
`Solicitud de alta (colegio contratado)` -> MANUAL -> `Superadmin registra datos del colegio y plan` -> AUTOMATICO -> `Provisioning de BD exclusiva + subdominio + usuario rector con contrasena temporal` -> AUTOMATICO -> `Correo al rector con URL y credenciales; tenant en estado Configurando` -> MANUAL -> `Rector completa configuracion minima` -> AUTOMATICO -> `Tenant pasa a Activo`
