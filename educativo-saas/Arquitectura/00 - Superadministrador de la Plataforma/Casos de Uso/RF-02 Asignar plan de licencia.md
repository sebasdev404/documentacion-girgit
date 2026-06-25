---
tags:
  - arquitectura
  - rol/superadmin
  - caso-de-uso
aliases:
  - CU RF-02
---

# ID: RF-02
**Nombre:** Asignar plan de licencia

**Historia:**
El colegio elige (o cambia) su plan comercial y el Superadministrador ajusta la licencia del tenant. El plan determina las cuotas de almacenamiento, los calendarios habilitados, los modulos y features de valor agregado disponibles y los limites de la identidad visual del colegio.

**Criterios de aceptacion:**
El Superadministrador asigna o cambia el plan del tenant. Los **upgrades se aplican de inmediato**; los **downgrades se ejecutan al cierre del ciclo de facturacion** para no romper compromisos vigentes (`RN-MT-241`). El cambio respeta el aislamiento por tenant (`RR-01`), habilita o limita las features de valor agregado segun el plan, y queda registrado en el log de auditoria (`RR-03`). Las cuotas de almacenamiento se recalibran segun el tier (`RN-AC-250`).

**Documentacion:**
- PRD: PRD-02 Superadministrador de la Plataforma
- Flow: Gestion de plan y licencia del tenant
- Prototipo: (link de Figma)

**Flujo:**
`Tenant activo con plan vigente` -> MANUAL -> `Superadmin selecciona nuevo plan` -> AUTOMATICO -> `Si es upgrade: aplica de inmediato; si es downgrade: agenda para el cierre de ciclo` -> AUTOMATICO -> `Recalibra cuotas y features habilitadas; registra en log` -> AUTOMATICO -> `Notifica al rector el cambio de plan`
