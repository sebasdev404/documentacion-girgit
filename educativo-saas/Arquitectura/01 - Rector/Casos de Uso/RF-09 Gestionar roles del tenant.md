---
tags:
  - arquitectura
  - rol/rector
  - caso-de-uso
aliases:
  - CU RF-09
---

# ID: RF-09
**Nombre:** Gestionar roles del tenant

**Historia:**
Como Rector necesito definir y ajustar los roles internos de mi colegio para que cada miembro del equipo (coordinadores, docentes, secretaria, psicologo, tesoreria) tenga exactamente los accesos que su funcion requiere. Solo yo asigno los roles del tenant (RR-04), y puedo activar o desactivar permisos configurables y renombrarlos, pero nunca crear permisos nuevos ni quitarme los estructurales (RR-05). Esto mantiene el control de quien hace que dentro del colegio sin abrir riesgos de seguridad.

**Criterios de aceptacion:**
El Rector puede ver el catalogo de roles del tenant y, para cada rol, activar o desactivar unicamente los permisos marcados como configurables y renombrar la etiqueta visible del rol. El sistema bloquea cualquier intento de crear un permiso inexistente, de quitar un permiso estructural o de removerse a si mismo permisos clave (RR-05), mostrando un mensaje claro. Toda modificacion de rol o permiso queda registrada en el log de auditoria inmutable del tenant con autor, fecha y valor anterior/nuevo (RR-03, RNF-03). El cambio se valida en frontend y backend (RR-02, RNF-02) y solo afecta al colegio actual, nunca a otro tenant (RR-01). Al guardar, los usuarios con ese rol reciben los nuevos permisos en su proxima sesion o refresco de sesion.

**Documentacion:**
- PRD: PRD-03 Rector
- Flow: Gestion de roles y permisos del tenant
- Prototipo: (link de Figma)

**Flujo:**
`Catalogo de roles del tenant` -> MANUAL -> `Rector abre un rol, activa/desactiva permisos configurables y/o renombra la etiqueta` -> AUTOMATICO -> `Sistema valida en frontend y backend que no haya permisos nuevos ni estructurales quitados (RR-05), persiste el cambio acotado al tenant (RR-01), registra la modificacion en el log de auditoria (RR-03) y propaga los permisos a los usuarios del rol en su proxima sesion`
