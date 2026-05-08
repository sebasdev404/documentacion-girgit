---
titulo: "Rol: Secretaría Académica"
modulo: usuarios-roles-y-permisos
tipo: rol
estado: borrador
tags: [rol, secretaria, administrativo, matricula, simat, tenant]
---

# Rol: Secretaría Académica

## Identificación

- **Nombre del rol:** Secretaría Académica
- **Tipo de usuario asociado:** Personal administrativo del colegio
- **Ámbito:** Tenant (colegio)
- **Configurable por el colegio:** sí — permisos configurables dentro de límites del sistema
- **Tipo:** principal

## Descripción

Gestiona los **procesos administrativos del colegio**: matrícula, registro de estudiantes y acudientes, emisión de documentos oficiales, control de documentos pendientes y reporte SIMAT. No tiene acceso a registrar ni editar notas.

## Responsabilidades

### Estudiantes y acudientes
- Registrar y actualizar la información de estudiantes y acudientes.
- Mantener el directorio de contactos del colegio.

### Matrícula
- Gestionar el proceso de matrícula: inscripción, recepción de documentos requeridos y asignación de grupo.
- Llevar el control de documentos de matrícula pendientes.
- Bloquear la generación de ciertos documentos cuando hay documentos o pagos pendientes (según la configuración del colegio).

### Documentos oficiales
- Generar **constancias de estudio**, **certificados de notas** y **paz y salvos**.
- Mantener la trazabilidad de documentos emitidos (consecutivos, fechas, firmas).

### Reporte oficial
- Preparar los reportes de matrícula para el **SIMAT** (Sistema Integrado de Matrícula del Ministerio de Educación Nacional de Colombia), al que los colegios están obligados a reportar.

## Scope / alcance de visibilidad

- Ve **todos los estudiantes y acudientes del tenant**.
- Ve la información de matrícula y documentos por estudiante.
- **No ve notas como datos editables** — solo las puede leer en formato de certificado/consolidado para emitir documentos.
- No ve datos de otros tenants.

## Permisos estructurales (no modificables)

| Permiso | Detalle |
| --- | --- |
| Crear y editar estudiantes | Datos personales, contacto, ficha de matrícula |
| Crear y editar acudientes | Vincularlos a estudiantes |
| Asignar estudiante a grupo | Como parte del proceso de matrícula |
| Cargar documentos de matrícula | Y marcarlos como recibidos / pendientes |
| Generar constancias y certificados | Con consecutivo y trazabilidad |
| Emitir paz y salvos | Cuando aplica |
| Reportar a SIMAT | Generar archivos / formatos requeridos |

## Permisos configurables por el colegio

| Permiso | Default | Notas |
| --- | --- | --- |
| Bloquear emisión de documentos por documentos pendientes | activado | Algunos colegios prefieren emitirlos igual y dejar la advertencia |
| Bloquear emisión de documentos por pagos pendientes | configurable | Depende de si el colegio integra la cartera con la secretaría |
| Editar grupo del estudiante después de matriculado | configurable | Algunos colegios lo restringen al Coordinador Académico |
| Generar paz y salvos sin pasar por contabilidad | configurable | |

## Permisos explícitamente NO otorgados

- No registra ni edita notas académicas.
- No registra asistencia ni observaciones disciplinarias.
- No modifica la configuración base del sistema.
- No accede a datos de otros tenants.

## Reglas de asignación

- Lo asigna el Rector / Administrador del Colegio.
- Cantidad típica: 1–3 por tenant.

## Compatibilidad con otros roles

- Un usuario con este rol no requiere roles adicionales para sus responsabilidades habituales.
- No es típicamente compatible con docencia (separación de funciones).

## Variantes según configuración del colegio

- En colegios pequeños este rol puede ser absorbido por el Rector.
- Algunos colegios separan "Secretaría" y "Tesorería" en dos roles; en ese caso, los permisos relacionados con cartera/pagos pueden separarse.

## Notas y pendientes

- Definir el formato exacto del reporte SIMAT (caso de uso aparte).
- Definir flujo de aprobación / firma para documentos oficiales: ¿basta con la secretaría, o requiere visto bueno del Rector?
- Definir consecutivos: por colegio, por tipo de documento, formato.
