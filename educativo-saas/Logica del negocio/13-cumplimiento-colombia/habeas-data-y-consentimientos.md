---
titulo: Habeas Data y consentimientos
modulo: 13-cumplimiento-colombia
tipo: proceso
estado: borrador
tags: [habeas-data, ley-1581, consentimientos, datos-personales, cumplimiento, menores]
---

# Habeas Data y consentimientos

## Descripción

Proceso por el cual el colegio (Responsable del Tratamiento) recolecta, almacena y demuestra las autorizaciones de tratamiento de datos personales exigidas por la Ley 1581 de 2012 y el Decreto 1377 de 2013. Como casi todos los titulares son menores de edad, el dato es **sensible** y la autorización la otorga el **acudiente** (titular de la patria potestad). Cada autorización se versiona contra la política de tratamiento vigente para poder probar qué consintió el acudiente y cuándo.

## Objetivo del proceso

Garantizar que el tenant pueda demostrar, ante una solicitud del titular o de la Superintendencia de Industria y Comercio (SIC), la existencia, alcance y fecha de cada autorización, y atender los derechos ARCO dentro de los plazos legales.

## Conceptos clave

| Concepto | En este sistema |
| --- | --- |
| Responsable del Tratamiento | El colegio (tenant). |
| Encargado del Tratamiento | El proveedor SaaS, que trata datos por cuenta del colegio bajo contrato de transmisión/transferencia. |
| Titular | El estudiante (menor de edad en la mayoría de los casos). |
| Quien autoriza | El acudiente con patria potestad. Ver [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]]. |
| Dato sensible | Datos de salud, biométricos, imagen, origen étnico, convicciones; aplican a menores con protección reforzada. |
| Finalidad | El propósito declarado para el cual se usan los datos (académico, financiero, comunicación, imagen). |

## Tipos de autorización

| Autorización | Naturaleza | Finalidad |
| --- | --- | --- |
| Tratamiento de datos personales | Obligatoria para operar la matrícula. | Gestión académica, financiera y de convivencia del estudiante. |
| Datos sensibles (salud) | Obligatoria si el colegio gestiona ficha de salud. | Atención de enfermería, alergias, EPS. Ver [[../12-bienestar-y-servicios/salud-y-enfermeria\|Salud y enfermería]]. |
| Uso de imagen | **Opcional**, granular. | Fotos/video en redes, página web, carné, material institucional. |
| Comunicaciones por canales digitales | Opcional. | WhatsApp, correo, push. Ver [[../05-comunicacion/comunicacion-con-padres\|Comunicación con padres]]. |
| Tratamiento por terceros | Informativa. | Pasarelas de pago, proveedores de transporte, etc. |

## Flujo principal

1. El acudiente, durante la matrícula, recibe la **política de tratamiento de datos** vigente del colegio (versión y fecha visibles).
2. El sistema presenta cada autorización con su finalidad, separando las **obligatorias** de las **opcionales** (imagen, canales).
3. El acudiente marca cada autorización de forma **expresa** (casilla no premarcada) y firma electrónicamente. Ver [[../11-plataforma-y-operacion/gestion-documental\|Gestión documental]].
4. El sistema registra el consentimiento: titular, acudiente que autoriza, finalidades aceptadas/rechazadas, versión de la política, fecha-hora, IP y evidencia de la firma.
5. El registro queda **inmutable**; cualquier cambio posterior crea una **nueva versión** y conserva la anterior.
6. Toda emisión, revocación o consulta de consentimiento se escribe en el [[../11-plataforma-y-operacion/log-de-auditoria\|Log de auditoría]].

## Derechos ARCO (acceso, rectificación, cancelación, oposición)

1. El acudiente radica una solicitud ARCO desde el portal o por el canal oficial del colegio.
2. El sistema crea un **caso ARCO** con tipo, fecha de radicación y reloj de vencimiento legal.
3. El rol responsable (secretaría académica / oficial de datos del colegio) gestiona la solicitud.
4. El colegio responde dentro de los plazos legales y la respuesta queda registrada.
5. La **cancelación/supresión** no aplica a datos cuya conservación sea obligatoria (históricos académicos, soportes legales): se documenta el motivo de retención.

| Derecho | Plazo de referencia (Ley 1581) |
| --- | --- |
| Consulta (Acceso) | 10 días hábiles, prorrogable 5. |
| Reclamo (Rectificación, Cancelación, Oposición) | 15 días hábiles, prorrogable 8. |

## Estados y transiciones

### Consentimiento

```
Solicitado → Otorgado → Vigente → Revocado
                      → Reemplazado (al publicarse nueva versión de la política)
```

### Caso ARCO

```
Radicado → En gestión → Resuelto
                      → Rechazado (con motivo)
                      → Trasladado (no es competencia del colegio)
```

## Configurabilidad por colegio

- Cada tenant carga su **propia política de tratamiento** y la versiona; el sistema no impone un texto único.
- El colegio define qué autorizaciones son **opcionales** (imagen, canales) y cuáles **bloquean la matrícula** si no se otorgan.
- El colegio designa el rol **responsable de datos** que atiende los casos ARCO.
- Periodos de retención documental configurables, respetando los mínimos legales de los históricos académicos.

## Integraciones con otros módulos

- [[../11-plataforma-y-operacion/gestion-documental\|Gestión documental]]: almacena el PDF firmado de cada autorización con su versión.
- [[../11-plataforma-y-operacion/log-de-auditoria\|Log de auditoría]]: traza emisión, revocación, consulta y respuesta ARCO.
- [[../04-procesos-academicos/matriculas\|Matrículas]]: la matrícula no se cierra sin las autorizaciones obligatorias.
- [[../04-procesos-academicos/observador-del-estudiante\|Observador del estudiante]] y [[../12-bienestar-y-servicios/salud-y-enfermeria\|Salud y enfermería]]: fuentes de datos sensibles que dependen de autorización específica.
- [[../06-monetizacion-y-pagos/pasarelas-de-pago\|Pasarelas de pago]]: tratamiento por encargado/tercero a informar.

## Reglas de negocio

- **RN-HD-001 — Autorización del acudiente para menores:** el consentimiento de tratamiento de un estudiante menor lo otorga el acudiente con patria potestad; el sistema no acepta autorización del propio menor como válida legalmente.
- **RN-HD-002 — Consentimiento expreso y granular:** las casillas de autorización no pueden venir premarcadas y cada finalidad (académica, imagen, canales) se acepta o rechaza por separado.
- **RN-HD-003 — Versionado contra la política:** todo consentimiento queda atado a la versión y fecha de la política de tratamiento vigente al momento de otorgarlo; una nueva política no reemplaza retroactivamente lo ya autorizado.
- **RN-HD-004 — Inmutabilidad y revocabilidad:** un consentimiento registrado es inmutable; revocarlo o cambiarlo genera una nueva versión y conserva el histórico anterior.
- **RN-HD-005 — Imagen es opcional y no bloquea matrícula:** rechazar el uso de imagen no impide matricular; el sistema marca al estudiante como "sin autorización de imagen" para que comunicación y publicaciones lo excluyan.
- **RN-HD-006 — Datos sensibles bajo finalidad explícita:** los datos de salud y biométricos solo se tratan si existe autorización específica para esa finalidad, distinta de la autorización general.
- **RN-HD-007 — Plazos ARCO con reloj:** cada caso ARCO arranca un contador de vencimiento legal (10/15 días hábiles); el sistema alerta antes del vencimiento al responsable de datos.
- **RN-HD-008 — Supresión limitada por retención legal:** una solicitud de cancelación no elimina datos cuya conservación es obligatoria (histórico académico, soportes financieros); se registra el motivo de retención.
- **RN-HD-009 — Trazabilidad obligatoria:** emisión, revocación, consulta y respuesta de consentimientos y casos ARCO se escriben en el log de auditoría con titular, actor, finalidad y fecha-hora.
- **RN-HD-010 — Aislamiento por tenant:** consentimientos y políticas de tratamiento son exclusivos del tenant; ningún dato de autorización cruza entre colegios.

## Notas y pendientes

- **[Decisión tomada]** La política de tratamiento es **propia de cada colegio y versionada** (RN-HD-003); el SaaS provee plantilla base pero no impone el texto legal.
- **[Decisión tomada]** El uso de imagen es **autorización opcional y granular** que no bloquea la matrícula (RN-HD-005).
- **[Pendiente — producto]** Definir el flujo cuando hay **dos acudientes con patria potestad** y autorizaciones de imagen discordantes (¿prevalece el rechazo?).
- **[Pendiente — producto]** Especificar la **transición de menor a mayor de edad**: cuándo y cómo el titular asume sus propios derechos ARCO y reconfirma autorizaciones.
- **[Pendiente — producto]** Validar con asesoría jurídica el formato del **contrato de transmisión/transferencia** entre colegio (Responsable) y SaaS (Encargado).

## Documentos relacionados

- [[../02-usuarios-roles-y-permisos/roles/08-estudiante-y-acudiente\|Estudiante / Acudiente]]
- [[../02-usuarios-roles-y-permisos/roles/05-secretaria-academica\|Secretaría académica]]
- [[../04-procesos-academicos/matriculas\|Matrículas]]
- [[../04-procesos-academicos/observador-del-estudiante\|Observador del estudiante]]
- [[../12-bienestar-y-servicios/salud-y-enfermeria\|Salud y enfermería]]
- [[../11-plataforma-y-operacion/gestion-documental\|Gestión documental]]
- [[../11-plataforma-y-operacion/log-de-auditoria\|Log de auditoría]]
- [[../05-comunicacion/comunicacion-con-padres\|Comunicación con padres]]
- [[../06-monetizacion-y-pagos/pasarelas-de-pago\|Pasarelas de pago]]
- [[../03-multi-tenancy/configuracion-por-colegio\|Configuración por colegio]]
