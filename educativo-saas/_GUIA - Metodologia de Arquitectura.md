---
tags:
  - arquitectura
  - guia
aliases:
  - Guia Metodologia de Arquitectura
  - Plantilla de Arquitectura
---

# GUIA — Metodologia de Arquitectura

> **Proposito:** documentar la metodologia de arquitectura de software que se usa para disenar, ordenar y comunicar este SaaS de gestion academica. Aplica a un proyecto donde existen **roles operativos** trabajando con **modulos de software** dentro del **flujo de negocio** de un colegio.

> **Nota de adaptacion:** la metodologia original distinguia departamentos. Para este proyecto **no hay departamentos**: la operacion completa pertenece a un solo colegio. Las referencias se mantienen aplanadas a nivel del proyecto entero.

---

## 1. Filosofia de la metodologia

La arquitectura no es solo el wireframe visual. Es el **conjunto completo** de documentacion que responde:

| Pregunta | Documento que la responde |
|---|---|
| Quienes usan el sistema? | Ficha de Rol · Ficha Detallada |
| Que hacen exactamente? | Acciones del Usuario · Casos de Uso |
| Que pueden ver/tocar/aprobar? | Permisos Detallados · Matriz de Permisos |
| Que pantallas usan? | Arquitectura wireframe |
| Que reglas rigen el sistema? | Reglas de Negocio |
| Que requerimientos cumple? | Tabla de Requerimientos · Por Modulo |
| Que se considera "terminado"? | Criterios de Aceptacion |
| De que depende? | Dependencias |
| Que informacion captura? | Campos del Formulario |
| Que bloquea? | Validaciones |
| Que responde el sistema? | Respuestas del Sistema |

---

## 2. Estructura de carpetas

```
Arquitectura/
│
├── _Globales/                      <- 9 archivos compartidos por todo el proyecto
│   ├── 01 - Portada.md
│   ├── 02 - PRD - Plataforma.md
│   ├── 03 - Tabla de Requerimientos.md
│   ├── 04 - Por Modulo.md
│   ├── 05 - Leyenda.md
│   ├── 06 - Matriz de Permisos.md
│   ├── 07 - Reglas de Negocio.md
│   ├── 08 - Criterios de Aceptacion.md
│   └── 09 - Dependencias.md
│
└── [NN - Rol]/                     <- carpeta por cada rol con 12 archivos + casos de uso
    ├── 00 - Arquitectura [Rol].md
    ├── 01 - Ficha de Rol.md
    ├── 02 - Ficha Detallada.md
    ├── 03 - PRD.md
    ├── 04 - Permisos Detallados.md
    ├── 05 - Requerimientos.md
    ├── 06 - Resumen Rapido.md
    ├── 07 - Feature Map.md
    ├── 08 - Acciones del Usuario.md
    ├── 09 - Campos del Formulario.md
    ├── 10 - Validaciones.md
    ├── 11 - Respuestas del Sistema.md
    └── Casos de Uso/
        ├── RF-XX [Nombre].md
        └── ...
```

Las carpetas de rol siguen el mismo orden jerarquico que se uso en `Logica del negocio/02-usuarios-roles-y-permisos/roles/` (prefijo `00-` para el rol mas alto, `08-` para el mas bajo).

---

## 3. Convenciones

### 3.1 Numeracion de archivos

Cada archivo lleva un **prefijo numerico** (`00 -`, `01 -`, ...) para forzar un orden de lectura especifico. El `00` es el wireframe principal del rol; del `01` al `11` son archivos de detalle.

### 3.2 IDs de roles

Formato: `ROL-NN` donde `NN` es el correlativo (01, 02, 03...).

Reservar siempre:
- Un ID para **Sistema** (automatizacion, no es persona).
- Un ID para **Administrador** o equivalente (gestion tecnica, puede quedar en pausa).

### 3.3 IDs de requerimientos

Formato: `[Tipo]-NN`

| Prefijo | Tipo | Define |
|---|---|---|
| **RF** | Requerimiento Funcional | QUE hace el sistema (acciones, flujos) |
| **RNF** | Requerimiento No Funcional | COMO lo hace (rendimiento, seguridad, usabilidad) |
| **RR** | Requerimiento de Negocio | POR QUE existe (reglas, politicas, restricciones) |
| **RI** | Requerimiento de Integracion | CON QUE conecta (otros modulos, sistemas externos) |

Ejemplos: `RF-01`, `RR-05`, `RNF-02`, `RI-04`.

### 3.4 IDs de PRDs

Formato: `PRD-NN`
- `PRD-01` = PRD del proyecto completo (Plataforma).
- `PRD-02`, `03`, ... = PRD por rol, en el mismo orden que ROL-NN.

### 3.5 IDs de criterios de aceptacion

Formato: `AC-NN`. Ejemplo: `AC-01`.

### 3.6 Frontmatter de cada archivo

```yaml
---
tags:
  - arquitectura
  - rol/[nombre-del-rol]       # solo en archivos de rol
aliases:
  - [Alias corto del documento]
---
```

### 3.7 Wikilinks

```markdown
[[Ruta/Archivo|Alias visible]]
```

Conectar cada documento con todo lo que referencia (semaforos, otros roles, modulos, reglas). El grafo se construye solo.

---

## 4. Plantillas por archivo

### _Globales/

#### 01 - Portada.md

**Funcion:** indice del proyecto. Lista los roles, los IDs, las jerarquias y los nombres.

**Estructura:**
- Cabecera con datos del documento (version, estado, relacionado a PRD).
- Tabla "ROLES DEFINIDOS EN ESTE DOCUMENTO" con: ID, Rol, Descripcion breve.
- Seccion de Jerarquias (si aplica): tabla con cada jerarquia + roles aplicables.
- Callout informativo con notas clave.

---

#### 02 - PRD - Plataforma.md

**Funcion:** Product Requirements Document del proyecto completo.

**Estructura:**
- Cabecera: ID PRD, HU, Funcionalidad, Actor Principal, Dispositivo, Estado, Version.
- **Objetivo** (1 parrafo).
- **Alcance:** Incluye / Fuera del alcance.
- **Flujo General** (1 linea + diagrama opcional).
- **Actores:** tabla con Actor, Tipo, Responsabilidad principal.
- **Restricciones / Reglas aplicables:** referencia a 07 - Reglas de Negocio.
- **Integraciones (RI):** tabla con ID, Integracion, Descripcion.
- **Dependencias:** referencia a 09 - Dependencias.

---

#### 03 - Tabla de Requerimientos.md

**Funcion:** todos los RFs, RNFs, RRs, RIs del proyecto en una tabla grande para Sheet/Excel.

**Estructura:**
- Cabecera del documento.
- Tipos de Requerimiento (leyenda RF/RNF/RR/RI).
- Prioridad y Estado (leyenda visual).
- Tabla maestra:

| ID | Tipo | Modulo | Requerimiento | Descripcion Detallada | Rol(es) | Criterio de Aceptacion | Prioridad | Estado | Notas |
|---|---|---|---|---|---|---|---|---|---|

---

#### 04 - Por Modulo.md

**Funcion:** agrupar los RFs por **modulo del sidebar**. Cada modulo tiene su descripcion corta + tabla de RFs.

**Estructura por modulo:**
```markdown
## [Nombre del Modulo]

Descripcion corta de 1-2 lineas que explica que hace el modulo.

| ID | Requerimiento | Rol(es) | Prioridad |
|---|---|---|---|
| RF-NN | ... | ... | Alta |
```

Cerrar con secciones para:
- Configuracion (Admin en pausa)
- No Funcionales (Transversal)
- Reglas de Negocio (resumen con enlace a 07)
- Integraciones

---

#### 05 - Leyenda.md

**Funcion:** explicar los simbolos de la matriz de permisos.

**Estructura:**
- Tabla de Simbolos / Significado / Aplica a.
- Tabla de Roles definidos en el documento.

Simbolos tipicos a usar (estos son funcionales de la metodologia, no decorativos):
- CRUD · Crear · Ver · C · E · Aprobar · Rechazar · Investigar · Reportar · Auto · — Sin permiso · En pausa

---

#### 06 - Matriz de Permisos.md

**Funcion:** quien puede hacer que, modulo por modulo, accion por accion.

**Estructura:**

| Modulo | Funcionalidad / Accion | ROL-01 | ROL-02 | ROL-03 | ... |
|---|---|---|---|---|---|
| **NOMBRE** | Accion 1 | Crear | Ver | — | ... |
| | Accion 2 | — | C · E | Auto | ... |

Cerrar con seccion "Notas clave" con las reglas de oro del proyecto.

---

#### 07 - Reglas de Negocio.md

**Funcion:** reglas RR-NN consolidadas con ID, regla, descripcion.

**Estructura:**

| ID | Regla | Descripcion |
|---|---|---|
| RR-01 | Nombre corto | Descripcion detallada |

Cerrar con seccion "Referencias cruzadas" enlazando a documentos relacionados.

---

#### 08 - Criterios de Aceptacion.md

**Funcion:** condiciones que se deben cumplir para considerar el sistema "terminado".

**Estructura:**

| # | Criterio |
|---|---|
| AC-01 | El sistema cumple X cuando ocurre Y bajo Z condiciones |

Cada criterio referencia la regla RR/RF que cubre. Son verificables (si/no).

---

#### 09 - Dependencias.md

**Funcion:** mapear que necesita el proyecto para funcionar.

**Estructura:** 5 secciones:
1. **Dependencias internas** (otros modulos del sistema).
2. **Dependencias externas** (apps, sistemas, integraciones).
3. **Dependencias de catalogos** (configuracion del sistema).
4. **Dependencias entre roles** (roles que intervienen en flujos compartidos).
5. **Dependencias semaforicas** (estados visuales del flujo).

Cada seccion es una tabla con Dependencia / Descripcion.

---

### Carpeta de cada rol

#### 00 - Arquitectura [Rol].md

**Funcion:** **wireframe principal del rol**. Es el documento mas visual y referenciado.

**Estructura obligatoria:**
1. **N0 — Inicio**: diagrama del flujo de login.
2. **HEADER** (presente en toda la app):
   - Perfil del usuario
   - Buscador
   - Notificaciones
3. **N1 — SIDEBAR**: lista de modulos a los que tiene acceso.
4. **Detalle por modulo** (uno por uno):
   - Sub-vistas
   - Filtros
   - Detalle
   - Acciones
   - Callouts informativos / importantes / warning
   - **Como se usa este modulo** (flujo narrativo de como lo opera el rol dia a dia)
5. **Diferencias clave vs [otros roles]**: tabla comparativa.
6. **Diagrama ASCII general** del wireframe completo.
7. **Relacionado**: lista de wikilinks.

---

#### 01 - Ficha de Rol.md

**Funcion:** tarjeta resumen del rol en formato compacto.

**Estructura:** tabla con: ID Rol, Nombre, Tipo, Reporta a, Supervisa a.

Secciones cortas:
- Descripcion (1 parrafo)
- Objetivo en el sistema
- Acciones principales (bullets)
- Permisos clave
- Nivel de acceso
- Dispositivo
- Frecuencia de uso

---

#### 02 - Ficha Detallada.md

**Funcion:** ficha extendida con todos los campos para Sheet/Excel.

**Estructura:** una tabla larga con todos los campos de 01 + adicionales:
- Modulos que usa
- Permisos CRUD
- Dolor / Necesidad actual
- Notas UX / Recomendaciones

---

#### 03 - PRD.md

**Funcion:** PRD especifico del rol.

**Estructura:**
- Cabecera (ID PRD, HU, Funcionalidad, Actor, Dispositivo, Estado, Version).
- Objetivo
- Flujo General
- Casos de Uso (tabla con ID, Caso, Prioridad)
- **Reglas de Negocio Aplicables** (tabla con ID, Regla, Descripcion, Prioridad)
- **Restricciones / Permisos** (tabla con #, Accion que NO puede hacer, Por que, Quien SI puede)

> **Tip:** estas dos ultimas secciones se hacen como tablas para que sean copiables a Google Sheets.

---

#### 04 - Permisos Detallados.md

**Funcion:** detalle granular de permisos del rol, modulo por modulo.

**Estructura:**

| Modulo | Funcionalidad | Permiso | Descripcion |
|---|---|---|---|
| **Modulo X** | Accion 1 | Crear | Detalle de la accion |

---

#### 05 - Requerimientos.md

**Funcion:** lista de RFs/RRs/RNFs aplicables a este rol especificamente (filtrado de 03 - Tabla de Requerimientos).

**Estructura:**

| ID | Requerimiento | Prioridad |
|---|---|---|

Agrupar por categoria si tiene sentido (Operativas / Ejecutivas / etc.).

---

#### 06 - Resumen Rapido.md

**Funcion:** one-pager con lo esencial.

**Estructura:** tabla compacta con Rol, Objetivo, Permisos Clave, Dispositivo, Acciones Principales, Nivel.

---

#### 07 - Feature Map.md

**Funcion:** mapa visual de todas las features del rol agrupadas por modulo + clasificacion primaria/secundaria.

**Estructura:** arbol con 2 ramas principales:

```
[ROL]
│
├── PRIMARIAS
│   │
│   ├── Modulo 1
│   │   └── Features core
│   └── Modulo 2
│       └── Features core
│
└── SECUNDARIAS
    │
    ├── Analisis
    │   └── Metricas, dashboards
    └── Utilidades
        └── Exportar, descargar, soporte
```

**No usar emojis para clasificar.** La estructura del arbol clasifica. Lo que cae bajo "Primarias" son los modulos core del sidebar; lo que cae bajo "Secundarias" son features transversales (analisis, utilidades, integraciones).

---

#### 08 - Acciones del Usuario.md

**Funcion:** tabla de accion -> resultado.

**Estructura:**

| Accion | Resultado |
|---|---|
| Click en X | Sistema ejecuta Y · Notifica a Z · Cambia estado a W |

---

#### 09 - Campos del Formulario.md

**Funcion:** campos de cada formulario que el rol llena.

**Estructura por formulario:**

```markdown
## A) Formulario "Nombre del formulario" (RF-NN)

| Campo | Tipo de Input | Obligatorio | Validacion | Descripcion |
|---|---|---|---|---|
```

Repetir por cada formulario (A, B, C, ...).

---

#### 10 - Validaciones.md

**Funcion:** casos de validacion y que hace el sistema.

**Estructura:**

| Caso | Comportamiento del Sistema |
|---|---|
| Campo vacio | Bloquea envio; muestra "..." |
| Email invalido | Bloquea envio; muestra "..." |

---

#### 11 - Respuestas del Sistema.md

**Funcion:** que responde el sistema ante eventos.

**Estructura:**

| Evento | Respuesta del Sistema |
|---|---|
| Usuario X hace Y | Sistema cambia Z · Notifica a W · Registra log |

---

### Casos de Uso/ (subcarpeta dentro del rol)

#### RF-NN [Nombre del caso].md

**Funcion:** detalle narrativo de un caso de uso especifico, listo para copiar al Sheet.

**Estructura fija:**

```markdown
---
tags:
  - arquitectura
  - rol/[rol]
  - caso-de-uso
aliases:
  - CU RF-NN
---

# ID: RF-NN
**Nombre:** [Nombre del caso]

**Historia:**
[2-4 lineas narrando el contexto y por que importa]

**Criterios de aceptacion:**
[1 parrafo con los criterios verificables]

**Documentacion:**
- PRD: PRD-NN [Rol]
- Flow: [Nombre del flow]
- Prototipo: (link de Figma)

**Flujo:**
`Estado/Origen` -> MANUAL -> `Accion` -> AUTOMATICO -> `Resultado`
```

---

## 5. Pasos para aplicar la metodologia

### Paso 1 — Definir el alcance
Identificar los **roles** del proyecto. Para este SaaS de gestion academica son los 9 roles documentados en `Logica del negocio/02-usuarios-roles-y-permisos/roles/`.

### Paso 2 — Por cada rol, definir
- Nombre tecnico (corto)
- Nombre comercial / alias
- Jerarquia (a quien reporta, a quien supervisa)
- Si es operativo, supervisor o ejecutivo

### Paso 3 — Crear `_Globales/`
Empezar SIEMPRE por aqui. Estos 9 archivos son la base que el resto referencia:
1. Portada (roles e IDs)
2. PRD del proyecto (objetivo + alcance)
3. **Tabla de Requerimientos** (los RFs/RRs/RNFs/RIs)
4. Por Modulo (RFs agrupados)
5. Leyenda
6. Matriz de Permisos
7. Reglas de Negocio (RRs)
8. Criterios de Aceptacion
9. Dependencias

### Paso 4 — Por cada rol, crear su carpeta con 12 archivos
Empezar por:
- **00 - Arquitectura** (el wireframe — es lo mas visible)
- **01 - Ficha de Rol** (resumen)
- **04 - Permisos Detallados** (que puede hacer)
- **05 - Requerimientos** (RFs aplicables al rol)

Luego completar:
- 02 Ficha Detallada
- 03 PRD del rol
- 06 Resumen Rapido
- 07 Feature Map
- 08 Acciones del Usuario
- 09 Campos del Formulario
- 10 Validaciones
- 11 Respuestas del Sistema

### Paso 5 — Casos de Uso
Por cada RF importante del rol, crear un archivo en `Casos de Uso/` con el formato narrativo (Historia / Criterios / Flujo).

### Paso 6 — Iterar
La arquitectura es viva. Cuando cambia una regla de negocio:
1. Actualizar `Logica del negocio/` primero (fuente de verdad).
2. Propagar a `Arquitectura/_Globales/07 - Reglas de Negocio.md`.
3. Propagar a la Matriz de Permisos.
4. Ajustar archivos por rol (Permisos, Acciones, Validaciones).
5. Actualizar Casos de Uso que dependen de la regla.

---

## 6. Buenas practicas

### Lo que SI hacer
- Usar wikilinks intensivamente para conectar todo.
- Tablas para Sheet/Excel: estructurar pensando en copiar-pegar.
- Descripciones cortas (1-2 lineas) bajo cada heading de modulo.
- Cada cambio de status / accion critica con regla RR-NN asociada.
- Frontmatter consistente para que el grafo se vea bien.
- Casos de uso con numero RF para trazabilidad.

### Lo que NO hacer
- No duplicar contenido entre archivos. Usar referencias.
- No usar ASCII art complejo si no se necesita (mejor narrativa).
- No clasificar features con colores en arbol (la estructura clasifica).
- No mezclar reglas de negocio (RR) con criterios de aceptacion (AC).
- No olvidar el rol "Sistema" (automatizacion) y "Administrador" (en pausa).
- No empezar por wireframes sin haber definido roles + reglas + RFs.
- No usar emojis decorativos. Solo los simbolos funcionales que esta guia define para matrices / leyendas / semaforos.

---

## 7. Checklist de calidad

Antes de considerar la arquitectura "terminada":

- [ ] Existen los 9 archivos de `_Globales/`.
- [ ] Cada rol tiene sus 12 archivos + Casos de Uso.
- [ ] Cada RF en la tabla de requerimientos tiene un caso de uso o esta cubierto por la matriz.
- [ ] Cada accion de la matriz de permisos tiene una RR que la justifica si es exclusiva.
- [ ] Los wikilinks no estan rotos (`[[X]]` que no existe).
- [ ] Frontmatter consistente en todos los archivos.
- [ ] La matriz de permisos cubre TODAS las acciones del wireframe.
- [ ] Las dependencias externas estan explicitas.
- [ ] Los casos de uso siguen el formato Historia + Criterios + Flujo.
- [ ] La Portada lista todos los roles correctamente con ID y descripcion.

---

## 8. Como exportar este documento a PDF (Obsidian)

1. Abre este archivo en Obsidian.
2. Haz click en los **3 puntos** arriba a la derecha (More options).
3. Selecciona **"Export to PDF..."**.
4. Elige opciones:
   - **Paper size:** A4 o Letter
   - **Include footer**: opcional
   - **Open after export**: si
5. Guarda donde quieras.

> **Alternativa con Pandoc** (si no tienes Obsidian):
> ```
> pandoc "_GUIA - Metodologia de Arquitectura.md" -o guia.pdf
> ```

---

## 9. Glosario

| Termino | Significado |
|---|---|
| **PRD** | Product Requirements Document |
| **HU** | Historia de Usuario |
| **RF** | Requerimiento Funcional |
| **RNF** | Requerimiento No Funcional |
| **RR** | Requerimiento de Negocio (Regla) |
| **RI** | Requerimiento de Integracion |
| **AC** | Criterio de Aceptacion |
| **CU** | Caso de Uso |
| **Wireframe** | Mockup visual de baja fidelidad de las pantallas |
| **Sidebar** | Menu lateral con los modulos del rol |
| **Trigger Automatico** | Conjunto de acciones que ejecuta el sistema automaticamente al ocurrir un evento |
| **Semaforo** | Indicador visual de estado (tipicamente Verde / Amarillo / Rojo) |

---

> **Esta guia es la metodologia oficial del proyecto.** Aplicala consistentemente. La estructura de `Logica del negocio/` define la fuente de verdad; la estructura de `Arquitectura/` es la interpretacion UX/sistema de esa logica.
