---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - respuestas-sistema
aliases:
  - Respuestas Sistema ROL-12
---

# Respuestas del Sistema — Personal de Apoyo

Que responde el sistema ante cada evento.

## Nucleo comun

| Evento | Respuesta del Sistema |
|---|---|
| El Rector crea la cuenta y asigna un perfil | Habilita el **modulo de servicio** del perfil · aplica el nucleo comun de consulta · activa la cuenta (`RN-TU-003`, `RN-TU-004`) |
| El funcionario consulta la ficha de un estudiante | Muestra la **ficha acotada** · oculta notas/cartera · registra la consulta en log con usuario, fecha, hora e IP (`RN-TU-006`, `RN-TU-009`) |
| El funcionario crea un aporte al observador | Guarda la anotacion con visibilidad seleccionada (default **interna**) · la hace visible solo a la audiencia que permite `RN-OB-081` · registra en log |
| El funcionario genera una remision interna | Crea la remision · notifica al destinatario **sin el motivo sensible** · no aplica decision alguna (`RN-TU-010`) |
| Llega una remision interna dirigida a su servicio | Notifica al funcionario (si el colegio activo esa notificacion) · la coloca en su bandeja |

## Perfil Orientador / Psicologo (Bienestar, `RN-BW`)

| Evento | Respuesta del Sistema |
|---|---|
| Se agenda una cita | Crea la cita · reserva consultorio si es presencial · notifica fecha/hora/lugar **sin el motivo clinico** (`RN-BW-006`) |
| Una alerta de riesgo alcanza el umbral (`RN-VA-101`) | Enruta la alerta al area de orientacion para abrir o actualizar un caso; **no** actua sola sobre el estudiante (`RN-BW-007`) |
| Se registra una nota de seguimiento | Guarda en nivel **interna** por defecto · no alimenta el boletin ni los reportes academicos (`RN-BW-003`, `RN-BW-004`) |
| Se genera una remision externa | Exige consentimiento del acudiente registrado antes de compartir datos (`RN-BW-005`) |
| Se cierra un caso | Conserva todas las notas y remisiones; no permite borrado fisico (`RN-BW-009`) |

## Perfil Enfermeria (Salud, `RN-SA`)

| Evento | Respuesta del Sistema |
|---|---|
| Se identifica al estudiante en enfermeria | Carga la ficha medica con alertas activas (alergias, condiciones cronicas) |
| Se guarda una atencion | **Notifica al acudiente** segun severidad; los graves notifican de inmediato y escalan al segundo contacto si no hay confirmacion (`RN-SA-005`) |
| Se suministra un medicamento | Verifica autorizacion vigente; si existe, registra el suministro; si no, **bloquea** (`RN-SA-003`) |
| Se genera una remision a centro medico | Notifica acudiente + Coordinador de Convivencia (`RN-SA-006`) · marca la atencion como remitida |
| El evento de salud se lleva al observador | Crea la anotacion con visibilidad `RN-OB-081`, por defecto **interna** (`RN-SA-008`) |

## Perfil Bibliotecario (Biblioteca, `RN-BI`)

| Evento | Respuesta del Sistema |
|---|---|
| Se registra un prestamo | Asocia un ejemplar concreto · calcula vencimiento por configuracion · cambia el ejemplar a `Prestado` · notifica la fecha y programa recordatorios (`RN-BI-001`, `RN-BI-002`) |
| Se registra una devolucion con retraso | Genera **multa** segun politica · libera el ejemplar · atiende la cola de reservas (`RN-BI-005`, `RN-BI-008`) |
| Se genera una multa con integracion a cartera activa | Incorpora el cargo al estado de cuenta del acudiente · puede afectar el paz y salvo (`RN-BI-006`, `RN-BI-007`) |
| Se devuelve un ejemplar con reservas en cola | Notifica al primero de la cola y abre la ventana de retiro; caduca si no retira (`RN-BI-008`) |
| Se declara un ejemplar extraviado | Genera multa de reposicion y da de baja el ejemplar del inventario disponible (`RN-BI-009`) |

## Transversales

| Evento | Respuesta del Sistema |
|---|---|
| Cualquier consulta o aporte del rol | Registra entrada inmutable en el log del tenant con usuario, fecha, hora e IP (`RN-TU-009`, RR-03) |
| Login fallido | Mensaje generico (no revela si el usuario existe) · registra en log de seguridad |
| Intento de operar un modulo no permitido | Rechaza en backend · registra el intento (RR-02) |

## Relacionado

- [[08 - Acciones del Usuario]]
- [[10 - Validaciones]]
- [[../_Globales/07 - Reglas de Negocio|Reglas de Negocio]]
- Fuente: `Logica del negocio/12-bienestar-y-servicios/` y `Logica del negocio/04-procesos-academicos/observador-del-estudiante.md`
