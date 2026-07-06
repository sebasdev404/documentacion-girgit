---
tags:
  - plan
  - completado
  - gobernanza
aliases:
  - Plan Maestro de Completado
  - Roadmap de Documentacion
estado: en-progreso
---

# Plan Maestro de Completado

> **Proposito:** columna vertebral del trabajo de completado de la documentacion. Define (A) las decisiones que resuelven las inconsistencias detectadas, (B) el catalogo de modulos nuevos a documentar segun como funciona un SIS real, (C) el catalogo de valor agregado, y (D) la asignacion de rangos de ID para que la escritura en paralelo no colisione. Cualquier archivo nuevo o modificado debe respetar las decisiones e IDs de aqui.

> **Como usar este documento.** La fuente de verdad sigue siendo `Logica del negocio/`. Este plan es el acuerdo de gobernanza para llegar a "terminado" segun el checklist de la [[_GUIA - Metodologia de Arquitectura#7. Checklist de calidad|guia]]. Convenciones en [[CLAUDE]].

---

## A. Decisiones de saneamiento (resuelven inconsistencias)

Estas decisiones cierran las contradicciones halladas en la auditoria. Se aplican primero en `Logica del negocio/` y luego se propagan a `Arquitectura/`.

| ID | Decision | Regla(s) afectada(s) | Resolucion | Archivos a tocar |
|---|---|---|---|---|
| **D-01** | MFA en el MVP | `RN-RG-421` vs `autenticacion.md` | MFA **obligatorio desde el MVP** para Superadministrador y roles de alto privilegio (rector, coordinadores, secretaria). Opcional/expansion progresiva para el resto. SSO Google/Microsoft permanece como futuro. Se elimina el rotulo "MFA opcional (futuro)". | `02-.../autenticacion.md` |
| **D-02** | Caducidad de cuentas inactivas | `RN-CV-370`, nota MVP | **Sin transicion automatica a Inactivo en MVP**: el cambio `Activo -> Inactivo` es **manual** por rol con permiso. Se corrigen las tablas de transiciones y eventos del ciclo de vida para que digan "manual", coherente con la nota ya decidida. | `02-.../ciclo-de-vida-de-usuario.md` |
| **D-03** | Quien reabre el año cerrado | `RN-PR-005`, `RN-PR-101`, `RN-HC-280`, `RN-HC-281` | **Modelo de dos niveles unico:** (1) reapertura **intra-ventana** -> cualquier rol con permiso `cierre.reabrir` (`RN-PR-101`/`RN-HC-280`), con justificacion y log inmutable; (2) reapertura **fuera de ventana / post-cierre** -> **exclusiva del superadministrador** (`RN-HC-281`). `RN-PR-005` se reescribe para remitir a este modelo y prohibir edicion directa. | `04-.../promocion-y-reprobacion.md`, `11-.../historico-y-anos-cerrados.md` |
| **D-04** | Rol "Personal de apoyo" | `RN-TU-411`, `RN-OB-081` | Se **formaliza** como tipo de usuario y rol: se agrega al catalogo de `tipos-de-usuario.md`, a la matriz de permisos (columna propia) y a `Arquitectura` como **ROL-12**. Permisos minimos: consulta acotada del expediente + aporte al observador con visibilidad `RN-OB-081`. | `02-.../tipos-de-usuario.md`, `02-.../matriz-de-permisos.md`, nuevo `roles/09-personal-de-apoyo.md`, `Arquitectura/_Globales/01,05,06`, nueva carpeta `Arquitectura/09 - Personal de Apoyo/` |
| **D-05** | "Catalogo cerrado 1:1" | nota en `tipos-de-usuario.md` | Se ajusta la nota: el catalogo es cerrado pero incluye **Personal de apoyo**; sigue siendo 1:1 tipo-rol. | `02-.../tipos-de-usuario.md` |
| **D-06** | Trazabilidad RN <-> RR/RF | gap de mapeo | Se crea el global **`_Globales/10 - Mapeo RN-RR.md`** con tabla de equivalencia bidireccional `RN-XX-NNN` (Logica) -> `RR/RF-NN` (Arquitectura). | nuevo `Arquitectura/_Globales/10 - Mapeo RN-RR.md` |
| **D-07** | ROL-10 / ROL-11 fuera de matriz | cobertura de roles | Se documenta explicitamente que **ROL-10 (Sistema)** y **ROL-11 (Administrador Tecnico)** no tienen columna en la matriz operativa por diseño (automatizacion / en pausa). Se anade nota en Leyenda y Portada. | `Arquitectura/_Globales/01,05,06` |
| **D-08** | RR-09..RR-15 y columna AC | sincronia de tablas | Se agregan las filas `RR-09..RR-15` a `03 - Tabla de Requerimientos` y se completa la columna AC de los RF (cruce con `08 - Criterios de Aceptacion`). | `Arquitectura/_Globales/03`, `08` |
| **D-09** | Prefijo RN-PR duplicado | colision Periodos vs Promocion | Periodos academicos pasa a prefijo **`RN-PA`** ya existente para Periodos? No: se mantiene `RN-PR` para Promocion y se renombra Periodos a **`RN-PD`** (periodos) en `reglas-por-modulo.md`; documentar el prefijo `RN-RT` ya en uso. | `07-.../reglas-por-modulo.md` |

---

## B. Catalogo de modulos nuevos (gaps vs SIS real)

Modulos que un sistema de gestion escolar (SIS) completo necesita y que hoy no estan documentados. Se agregan como nuevos archivos en `Logica del negocio/`. Prioridad: **P1** (core de operacion / requisito legal Colombia), **P2** (servicios frecuentes), **P3** (deseable).

### B.1 Nueva seccion `12-bienestar-y-servicios/`

| Modulo | Por que (SIS real) | Prefijo RN | Archivo | Prioridad |
|---|---|---|---|---|
| Salud / Enfermeria | Ficha medica, EPS, alergias, medicamentos, atenciones, vacunas. Critico para responsabilidad legal del colegio. | `RN-SA` | `12-.../salud-y-enfermeria.md` | P2 |
| Bienestar / Orientacion escolar | Seguimiento psicosocial, remisiones, citas; alimenta el observador (`RN-OB-081`). | `RN-BW` | `12-.../bienestar-y-orientacion.md` | P2 |
| Biblioteca | Catalogo, prestamos, devoluciones, multas, reservas. | `RN-BI` | `12-.../biblioteca.md` | P3 |
| Transporte escolar | Rutas, paradas, monitores, novedades, cobro del servicio, notificacion de abordaje. | `RN-TR` | `12-.../transporte-escolar.md` | P2 |
| Restaurante / Comedor | Planes alimentarios, restricciones, cobro por tiquete o mensual. | `RN-RE` | `12-.../restaurante-y-comedor.md` | P3 |
| Inventario y activos | Dotacion, equipos, aulas, prestamo de recursos. | `RN-IV` | `12-.../inventario-y-activos.md` | P3 |
| Tienda escolar / otros cobros | Uniformes, salidas pedagogicas, eventos; conceptos cobrables fuera de pension. | `RN-TI` | `12-.../tienda-y-otros-cobros.md` | P2 |

### B.2 Nueva seccion `13-cumplimiento-colombia/` (legal MEN)

| Modulo | Por que (Colombia) | Prefijo RN | Archivo | Prioridad |
|---|---|---|---|---|
| Convivencia escolar (Ley 1620) | Comite de convivencia, Ruta de Atencion Integral (RAI), situaciones tipo I/II/III. Obligatorio por ley. | `RN-CVE` | `13-.../convivencia-ley-1620.md` | P1 |
| Reportes oficiales (SIMAT / DANE / Saber) | Reporte de matricula oficial, novedades, exportaciones al MEN/ICFES. Ya referenciado por `RR-15`. | `RN-MO` | `13-.../reportes-oficiales-men.md` | P1 |
| Habeas Data (Ley 1581) | Consentimientos, tratamiento de datos del menor, derechos ARCO, autorizaciones de imagen. | `RN-HD` | `13-.../habeas-data-y-consentimientos.md` | P1 |

### B.3 Ampliaciones de secciones existentes

| Modulo | Por que | Prefijo RN | Archivo | Prioridad |
|---|---|---|---|---|
| Admisiones | Proceso distinto de matricula: aspirantes, pruebas, entrevistas, lista de espera, conversion a matricula. | `RN-AM` | `04-.../admisiones.md` | P1 |
| Talento humano docente | Hoja de vida, contratos, evaluacion docente, capacitaciones; mas alla de la asignacion. | `RN-RH` | nueva `14-talento-humano/gestion-docente.md` | P2 |
| Tareas y actividades (LMS-lite) | Entrega de tareas, recursos por clase; antesala del LMS nativo (`RN-OI-340`). | `RN-TA` | `04-.../tareas-y-actividades.md` | P2 |
| Encuestas | Clima escolar, satisfaccion, autoevaluacion institucional. | `RN-EC` | `05-.../encuestas.md` | P3 |
| Eventos y reservas | Auditorios, salidas pedagogicas con autorizacion firmada del acudiente. | `RN-EV` | `04-.../eventos-y-reservas.md` | P3 |

---

## C. Catalogo de valor agregado (diferenciadores estandar)

Diferenciadores frente a la competencia colombiana (Phidias, Master2000, Ciudad Educativa, etc.). Se documentan en `Logica del negocio/15-valor-agregado/` y se asignan IDs `RN-VA`. Son features **sin IA**, opt-in por colegio.

### C.1 Estandar (vendibles ya, bajo riesgo)

| ID | Feature | Valor diferencial | Prioridad |
|---|---|---|---|
| `RN-VA-001` | App/Portal de Acudientes con notificaciones push y vista multi-hijo | Adelanta la "vista consolidada multi-hijo" hoy diferida; experiencia movil real. | P1 |
| `RN-VA-002` | Pagos sin friccion (PSE, Nequi, Daviplata, link de pago, debito recurrente, recordatorios) | Reduce cartera; pago en menos clics; medios locales CO. | P1 |
| `RN-VA-003` | WhatsApp como canal oficial (comunicados, notas, estado de cuenta) | Canal real de los padres en Colombia; mayor tasa de lectura que email. | P1 |
| `RN-VA-004` | Firma electronica de documentos (matricula, paz y salvo, autorizaciones) | Cero papel; trazabilidad legal; agiliza matricula. | P2 |
| `RN-VA-005` | Carne digital con QR y control de acceso (entrada/salida con aviso al acudiente) | Seguridad; tranquilidad del acudiente; dato de asistencia. | P2 |
| `RN-VA-006` | Tablero ejecutivo en tiempo real para el Rector | Vision de cartera, asistencia, convivencia y academico en una pantalla. | P2 |
| `RN-VA-007` | Generador automatico de horarios (optimizacion con restricciones) | Ahorra dias de trabajo manual a la coordinacion. | P3 |

### C.2 IA — descartada

> **Decision de producto:** las features de IA que se habian propuesto (alertas tempranas de riesgo, asistente de redaccion de boletines y asistente conversacional para acudientes) fueron **descartadas**. El catalogo de valor agregado queda solo con los diferenciadores estandar de C.1. Los IDs `RN-VA-101..103`, `RN-VA-110..119`, `RR-18`, `RF-87..89`, `RNF-08`, `RI-10` y `AC-28` quedan **retirados** (no reutilizar; sus huecos en la numeracion son intencionales).

---

## D. Asignacion de rangos de ID (anti-colision para escritura paralela)

### D.1 Prefijos `RN-XX` nuevos (Logica del negocio)

Libres y asignados: `RN-SA` salud, `RN-BW` bienestar, `RN-BI` biblioteca, `RN-TR` transporte, `RN-RE` restaurante, `RN-IV` inventario, `RN-TI` tienda, `RN-CVE` convivencia Ley 1620, `RN-MO` reportes oficiales MEN, `RN-HD` habeas data, `RN-AM` admisiones, `RN-RH` talento humano, `RN-TA` tareas, `RN-EC` encuestas, `RN-EV` eventos, `RN-VA` valor agregado. Cada modulo numera desde `-001`.

### D.2 IDs de Arquitectura (continuan los correlativos existentes)

| Tipo | Maximo actual | Nuevos desde |
|---|---|---|
| RF (Req. Funcional) | RF-50 | **RF-51** en adelante |
| RR (Regla de Negocio) | RR-15 (faltan en tabla maestra) | **RR-16** en adelante (+ migrar RR-09..15 a la tabla) |
| RNF (No Funcional) | RNF-07 | **RNF-08** en adelante |
| RI (Integracion) | RI-07 | **RI-08** en adelante |
| AC (Criterio Aceptacion) | AC-25 | **AC-26** en adelante |
| ROL | ROL-11 | **ROL-12** = Personal de Apoyo |
| PRD | PRD-02 (Superadmin) | **PRD-03** Rector ... **PRD-10** Estudiante, **PRD-11** Personal de Apoyo |

### D.3 Mapa carpeta de rol <-> ROL-NN <-> PRD-NN

| Carpeta Arquitectura | ROL | PRD | Estado actual |
|---|---|---|---|
| 00 - Superadministrador de la Plataforma | ROL-01 | PRD-02 | Completo (12/12) |
| 01 - Rector | ROL-02 | PRD-03 | 4/12 |
| 02 - Coordinador Academico | ROL-03 | PRD-04 | 4/12 |
| 03 - Coordinador de Convivencia | ROL-04 | PRD-05 | 4/12 |
| 04 - Coordinador Academico y Convivencia | ROL-05 | PRD-06 | 4/12 |
| 05 - Secretaria Academica | ROL-06 | PRD-07 | 4/12 |
| 06 - Docente | ROL-07 | PRD-08 | 4/12 |
| 07 - Director de Grupo | ROL-08 | PRD-09 | 4/12 |
| 08 - Estudiante y Acudiente | ROL-09 | PRD-10 | 4/12 |
| 09 - Personal de Apoyo (nuevo) | ROL-12 | PRD-11 | 0/12 |

---

## E. Orden de ejecucion

- **Fase 0 — Spec maestro** (este documento). Estado: hecho.
- **Fase 1 — Saneamiento.** Aplicar D-01..D-09 en `Logica del negocio/` + crear `_Globales/10 - Mapeo RN-RR.md`.
- **Fase 2 — Completar `Logica del negocio/`.** Escribir los modulos de la seccion B y el catalogo de valor agregado C (cada modulo con su plantilla de proceso/regla).
- **Fase 3 — Propagar a `Arquitectura/`.** Llenar los 8 roles en esqueleto (00, 02, 03, 07-11), crear ROL-12 Personal de Apoyo, generar los Casos de Uso por rol, y actualizar los `_Globales` (matriz, tabla de requerimientos, reglas, dependencias) con los nuevos RF/RR/RI/RNF.

---

## F. Checklist de cierre (seccion 7 de la guia)

- [ ] D-01..D-09 aplicadas y sin contradicciones residuales.
- [ ] `_Globales/10 - Mapeo RN-RR.md` cubre todas las RR existentes.
- [ ] Modulos B documentados con sus RN.
- [ ] Catalogo de valor agregado C documentado.
- [ ] 9 roles + ROL-12 con sus 12 archivos redactados.
- [ ] Casos de Uso por rol creados (no quedan subcarpetas vacias).
- [ ] Matriz de permisos cubre ROL-01..ROL-09 + ROL-12 y todas las acciones nuevas.
- [ ] Tabla de Requerimientos incluye RR-09..RR-16+ y columna AC completa.
- [ ] Wikilinks sin romper.
- [ ] Frontmatter consistente; sin emojis decorativos.
