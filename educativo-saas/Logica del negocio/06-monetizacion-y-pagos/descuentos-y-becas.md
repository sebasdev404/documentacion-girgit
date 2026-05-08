---
titulo: Descuentos y becas
modulo: monetizacion-y-pagos
tipo: regla
estado: borrador
tags: [descuentos, becas]
---

# Descuentos y becas

## Concepto

Un **descuento** o una **beca** es una reducción autorizada sobre el valor que paga un estudiante por uno o varios conceptos. Aunque conceptualmente son distintos (descuento = comercial, beca = social / mérito), en la plataforma comparten el mismo motor de aplicación.

## Tipos típicos de descuento

| Tipo | Descripción |
| --- | --- |
| Hermanos | Aplicado al segundo / tercer hijo del mismo acudiente. |
| Pronto pago | Aplicado a quien paga antes de la fecha de gracia. |
| Empleados | Hijos de docentes o personal del colegio. |
| Antigüedad | Familias con varios años en el colegio. |
| Promocional | Por campañas comerciales puntuales. |

## Tipos típicos de beca

| Tipo | Descripción |
| --- | --- |
| Mérito académico | Por desempeño destacado. |
| Necesidad | Por situación socioeconómica. |
| Deportiva / cultural | Por talento específico. |
| Empleados / convenio | Por convenios con empresas o entidades. |

## Modalidades de aplicación

- **Porcentaje** sobre el concepto.
- **Valor fijo** descontado del concepto.
- **Cobertura total** del concepto (beca al 100%).

Aplicable a: matrícula, pensión, transporte, alimentación u otros conceptos según se configure.

## Acumulación y prelación

- El colegio define qué descuentos / becas son acumulables y en qué orden se aplican.
- Por defecto: las becas se aplican primero (sobre el bruto), luego los descuentos comerciales.
- El sistema valida que la suma no supere el 100% del concepto, salvo configuración explícita.

## Aprobación y vigencia

- Cada descuento / beca tiene **fecha de inicio y fin de vigencia**.
- Una beca puede requerir aprobación del comité académico o del rector según configuración.
- Las becas se renuevan o no al cierre de año, según rendimiento y política del colegio.

## Aplicación al estudiante

- Un estudiante puede tener uno o más beneficios activos.
- Cada beneficio queda en su perfil con: tipo, motivo, monto / porcentaje, conceptos cubiertos, vigencia, autor que lo aprobó.
- Al generar la cuota, el sistema aplica los beneficios vigentes.

## Reglas de negocio

- **RN-DB-001 — Vigencia obligatoria:** todo beneficio tiene fecha de inicio y de fin.
- **RN-DB-002 — Auditoría completa:** creación, modificación y revocación de beneficios quedan en log con autor.
- **RN-DB-003 — Becas requieren motivo:** una beca registra el motivo y, si aplica, los soportes adjuntos.
- **RN-DB-004 — No retroactividad por defecto:** un beneficio aprobado tras emitirse una factura no modifica esa factura; aplica desde la siguiente.
- **RN-DB-005 — Límite acumulado:** la suma de beneficios sobre un concepto no supera el 100%, salvo configuración explícita.
- **RN-DB-006 — Revocación con motivo:** revocar un beneficio antes de su fin natural requiere motivo registrado.

## Notas y pendientes

- Definir si las becas requieren reporte mensual al comité que las otorga.
- Definir el flujo cuando un estudiante con beca cambia de colegio dentro del mismo grupo empresarial.
