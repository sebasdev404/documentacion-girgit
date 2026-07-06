---
tags:
  - arquitectura
  - rol/personal-de-apoyo
  - permisos
aliases:
  - Permisos ROL-12
---

# Permisos Detallados — Personal de Apoyo

Detalle granular de permisos del rol, modulo por modulo. Para la vista cruzada con otros roles ver [[../_Globales/06 - Matriz de Permisos|Matriz de Permisos]] (columna `D-04`).

> Los permisos del **modulo de servicio** solo se activan para el **perfil** correspondiente (`RN-TU-004`). Una misma cuenta nunca tiene Bienestar + Salud + Biblioteca a la vez.

## Permisos estructurales (no modificables) — Nucleo comun

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Estudiante (ficha)** | Consultar ficha acotada | Ver | Identificacion, grupo, contacto del acudiente, alertas basicas (`RN-TU-006`) |
| **Observador** | Aportar anotacion | Crear | Con seleccion de visibilidad `RN-OB-081`; por defecto interna (`RN-TU-005`) |
| **Observador** | Editar aporte propio | Editar | Por anotacion adicional, sin borrar el original |
| **Observador** | Ver anotaciones permitidas | Ver | Solo las que su nivel de visibilidad `RN-OB-081` autorice |
| **Mi agenda** | Consultar bandeja del servicio | Ver | Citas, atenciones o prestamos a su cargo |
| **Remisiones** | Generar remision interna | Crear | A coordinacion u otro perfil; no decide (`RN-TU-010`) |

## Permisos estructurales por perfil (solo el del perfil asignado)

### Perfil Orientador / Psicologo — Bienestar (`RN-BW`)

| Funcionalidad | Permiso | Descripcion |
|---|---|---|
| Expediente de bienestar | Ver / Crear / Editar | Unico por estudiante, transversal al ano (`RN-BW-001`) |
| Agendar / reprogramar cita | Crear / Editar | Sin exponer motivo clinico en la notificacion (`RN-BW-006`) |
| Nota de seguimiento | Crear | Por defecto en nivel interna (`RN-BW-004`) |
| Plan de acompanamiento | Crear / Editar | Parte visible + parte interna (`RN-BW-008`) |
| Remision externa | Crear | Exige consentimiento del acudiente registrado (`RN-BW-005`) |
| Cerrar caso | Editar | Con resumen; preserva el historial (`RN-BW-009`) |

### Perfil Enfermeria — Salud (`RN-SA`)

| Funcionalidad | Permiso | Descripcion |
|---|---|---|
| Ficha medica del estudiante | Ver | La diligencia el acudiente (`RN-SA-001`); el rol consulta detalle clinico restringido (`RN-SA-002`) |
| Atencion en enfermeria | Crear | Registro inmutable: motivo, signos, disposicion (`RN-SA-004`) |
| Suministro de medicamento | Crear | Solo con autorizacion vigente del acudiente (`RN-SA-003`) |
| Control de vacunas | Editar | Marca estado al dia / pendiente / sin informacion (`RN-SA-009`) |
| Remision a centro medico | Crear | Notifica acudiente + Coordinador de Convivencia (`RN-SA-006`) |
| Aporte al observador (salud) | Crear | Visibilidad `RN-OB-081`, por defecto interna (`RN-SA-008`) |

### Perfil Bibliotecario — Biblioteca (`RN-BI`)

| Funcionalidad | Permiso | Descripcion |
|---|---|---|
| Catalogo y ejemplares | Crear / Editar | Material y ejemplar con codigo de barras |
| Prestamo | Crear | Sobre ejemplar concreto (`RN-BI-001`); vencimiento por configuracion (`RN-BI-002`) |
| Devolucion | Editar | Verifica retraso/dano; libera ejemplar |
| Multa | Crear | Por mora/dano/extravio segun politica (`RN-BI-005`); puede ir a cartera si el colegio lo activo (`RN-BI-006`) |
| Reservas | Crear / Editar | Cola por orden de llegada (`RN-BI-008`) |
| Inventario | Editar | Conciliacion fisica; registra faltantes (`RN-BI-010`) |

## Permisos configurables por el colegio

| Permiso | Default | Quien lo ajusta |
|---|---|---|
| Perfil concreto y modulo de servicio habilitado | Segun contratacion | Rector |
| Nivel de visibilidad por defecto de los aportes | interna (`RN-OB-081`) | Rector / coordinacion |
| Notificarse de remisiones internas a su servicio | Activado | Rector / coordinacion |
| Comunicarse con el acudiente via portal (RF-43) | Desactivado | Rector |
| Linea de reporte (Rector o coordinacion) | Segun colegio (`RN-TU-008`) | Rector |

## Permisos explicitamente NO otorgados

| Accion negada | Razon |
|---|---|
| Registrar/editar notas, boletines o consolidados | Rol no academico (`RN-TU-002`) |
| Acceder al expediente academico completo del estudiante | Solo ficha acotada (`RN-TU-006`) |
| Acceder a pagos, cartera o informacion financiera | Rol no financiero |
| Emitir documentos oficiales (certificados, paz y salvo, boletines) | Responsabilidad de Secretaria (ROL-06) |
| Configurar el colegio / parametros del tenant | Fuera de su alcance |
| Asignar/modificar roles, grupos, materias u horarios | Competencia del Rector / Coordinador |
| Operar el modulo de un perfil ajeno | Aislamiento entre perfiles (`RN-TU-004`) |
| Decidir sanciones, promocion o medidas academicas | Solo remite (`RN-TU-010`) |
| Acceder a datos de otros tenants | Aislamiento total (RR-01) |

## Reglas asociadas

- `RN-TU-001` a `RN-TU-010` — nucleo del rol.
- `RN-OB-081` — visibilidad de los aportes al observador.
- `RN-BW-*`, `RN-SA-*`, `RN-BI-*` — reglas de cada modulo de servicio.
- RR-03 Auditoria · RR-05 Configurabilidad acotada · RR-06 Acceso por subdominio.

## Fuente

`Logica del negocio/02-usuarios-roles-y-permisos/roles/09-personal-de-apoyo.md` y `Logica del negocio/12-bienestar-y-servicios/`.
