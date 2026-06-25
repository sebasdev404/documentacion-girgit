---
tags:
  - arquitectura
  - rol/secretaria-academica
  - caso-de-uso
aliases:
  - CU RF-35
---

# ID: RF-35
**Nombre:** Certificados de notas

**Historia:**
Como secretaria academica necesito emitir certificados de notas para los estudiantes que los solicitan (traslado a otro colegio, tramites o constancia de desempeno). Hoy transcribo las calificaciones a mano desde los boletines, lo que es lento y se presta a errores de digitacion. Quiero que el sistema lea el consolidado de notas que producen los docentes y arme el certificado con consecutivo, sin que yo pueda alterar las calificaciones.

**Criterios de aceptacion:**
La secretaria selecciona un estudiante de su colegio y el tipo "Certificado de notas", indicando el grado o periodo a certificar. El sistema lee el consolidado de notas en modo solo lectura (lo producen los docentes) y genera el documento con la identidad del colegio, los datos del estudiante y las calificaciones consolidadas, sin permitir a la secretaria editar ninguna nota (restriccion del rol). El certificado recibe un consecutivo unico e irrepetible dentro del tenant (`RN-GD-001`), queda archivado en gestion documental y la accion se registra en el log de auditoria (RR-03) con usuario, fecha y estudiante. Si hay documentos o pagos pendientes y el bloqueo esta activado (RR-08), el sistema advierte o bloquea la emision segun la configuracion del Rector. El certificado solo puede emitirse para estudiantes del propio colegio (RR-01) y puede reimprimirse sin generar un consecutivo nuevo.

**Documentacion:**
- PRD: PRD-07 Secretaria Academica
- Flow: Emision de documento oficial (certificado de notas)
- Prototipo: (link de Figma)

**Flujo:**
`Estudiante seleccionado con consolidado de notas disponible` -> MANUAL -> `Elegir tipo "Certificado de notas", indicar grado/periodo y confirmar emision` -> AUTOMATICO -> `Sistema lee las notas en solo lectura, valida pendientes (RR-08), genera el certificado con consecutivo unico (RN-GD-001) restringido al colegio (RR-01), lo archiva en gestion documental y registra la accion en el log (RR-03)`
