---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - acciones
aliases:
  - Acciones ROL-12
---

# Acciones del Usuario — Personal de Apoyo

Tabla accion -> resultado. Cada consulta de ficha y cada aporte al observador genera entrada en el log de auditoria del tenant (`RN-TU-009`, RR-03).

## Nucleo comun (todos los perfiles)

| Accion | Resultado |
|---|---|
| Busca un estudiante y abre su ficha | Sistema muestra **ficha acotada** (identificacion, grupo, contacto del acudiente, alertas basicas) · oculta notas/cartera · registra la consulta en log (`RN-TU-006`, `RN-TU-009`) |
| Crea un aporte al observador | Sistema preselecciona visibilidad **interna** (`RN-TU-005`) · permite cambiar a docentes/publica (`RN-OB-081`) · guarda la anotacion · registra en log |
| Edita un aporte propio | Sistema agrega una anotacion correctiva (no borra el original) · registra en log |
| Genera una remision interna | Sistema crea la remision a coordinacion u otro perfil · notifica al destinatario sin exponer motivo sensible · no aplica ninguna decision (`RN-TU-010`) |
| Abre su agenda / bandeja | Sistema lista citas, atenciones o prestamos a su cargo segun el perfil |
| Cierra sesion | Sistema invalida token · registra logout en log |

## Perfil Orientador / Psicologo (Bienestar, `RN-BW`)

| Accion | Resultado |
|---|---|
| Abre o ubica el expediente de bienestar | Sistema carga el expediente unico del estudiante (transversal al ano, `RN-BW-001`) · registra el acceso (`RN-BW-010`) |
| Agenda una cita | Sistema crea la cita (fecha/hora/modalidad) · notifica al destinatario **sin el motivo clinico** (`RN-BW-006`) · reserva consultorio si aplica |
| Registra una nota de seguimiento | Sistema guarda la nota en nivel **interna** por defecto (`RN-BW-004`) · no la publica en boletin (`RN-BW-003`) |
| Define un plan de acompanamiento | Sistema separa parte visible (compromisos/citas) de parte interna (hipotesis) (`RN-BW-008`) |
| Genera una remision externa | Sistema exige **consentimiento del acudiente** registrado antes de compartir datos (`RN-BW-005`) |
| Cierra el caso | Sistema exige resumen · conserva todo el historial (`RN-BW-009`) |

## Perfil Enfermeria (Salud, `RN-SA`)

| Accion | Resultado |
|---|---|
| Identifica al estudiante en enfermeria | Sistema carga la ficha medica con alertas activas (alergias, condiciones cronicas) |
| Registra una atencion | Sistema crea un registro inmutable (motivo, signos, disposicion) (`RN-SA-004`) |
| Suministra un medicamento | Sistema verifica **autorizacion vigente**; si existe, registra el suministro; si no, **bloquea** y obliga a contactar al acudiente (`RN-SA-003`) |
| Guarda la atencion | Sistema **notifica al acudiente** segun severidad; los graves notifican de inmediato y escalan al segundo contacto (`RN-SA-005`) |
| Genera una remision a centro medico | Sistema notifica acudiente + Coordinador de Convivencia (`RN-SA-006`) · marca la atencion como remitida · exige desenlace para cerrar |
| Actualiza el estado de vacunacion | Sistema marca al dia / pendiente / sin informacion (`RN-SA-009`) |
| Aporta el evento al observador | Sistema crea la anotacion con visibilidad `RN-OB-081`, por defecto **interna** (`RN-SA-008`) |

## Perfil Bibliotecario (Biblioteca, `RN-BI`)

| Accion | Resultado |
|---|---|
| Registra un prestamo | Sistema valida cupo, morosidad y disponibilidad · asocia un **ejemplar concreto** (`RN-BI-001`) · calcula vencimiento por configuracion (`RN-BI-002`) · notifica la fecha |
| Registra una devolucion | Sistema verifica retraso/dano · si aplica genera **multa** (`RN-BI-005`) · libera el ejemplar y atiende la cola de reservas (`RN-BI-008`) |
| Genera una multa | Sistema la liquida segun politica · si el colegio activo la integracion, la lleva a cartera (`RN-BI-006`) y puede afectar el paz y salvo (`RN-BI-007`) |
| Atiende una reserva | Sistema notifica al primero de la cola y abre ventana de retiro; caduca si no retira |
| Concilia inventario | Sistema compara catalogo vs ejemplares hallados · registra faltantes y bajas en log (`RN-BI-010`) |

## Relacionado

- [[10 - Validaciones]] — que bloquea el sistema en cada accion
- [[11 - Respuestas del Sistema]] — eventos y respuestas
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
