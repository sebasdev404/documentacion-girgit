---
tags:
  - arquitectura
  - rol/secretaria-academica
  - caso-de-uso
aliases:
  - CU RF-37
---

# ID: RF-37
**Nombre:** Reportar a SIMAT

**Historia:**
Como secretaria academica debo reportar al SIMAT las novedades de matricula (ingresos, retiros y traslados) dentro de la ventana que abre el MEN. Hoy diligencio los archivos planos a mano y arriesgo errores de formato que el sistema oficial rechaza. Quiero que la plataforma arme el archivo en el formato requerido a partir de los datos ya cargados, para reportar a tiempo y sin cuadrar la informacion campo por campo.

**Criterios de aceptacion:**
La secretaria selecciona el periodo de reporte y el sistema reune las novedades de matricula del colegio (altas, retiros y traslados) generando el archivo en el formato oficial exigido por el MEN (RR-15, `RN-MO-001`). Antes de exportar, el sistema valida que los registros tengan los campos obligatorios del SIMAT (tipo y numero de documento, grado, grupo, fechas) y muestra un listado de los estudiantes con datos incompletos para corregir, sin permitir generar el archivo hasta resolverlos. El reporte solo incluye estudiantes del propio colegio (RR-01), la generacion del archivo queda registrada en el log de auditoria (RR-03) con usuario y fecha, y el archivo puede descargarse para cargarlo en el SIMAT (RI-02). La secretaria registra el resultado de la carga (exitoso o con observaciones) para dejar trazabilidad del cumplimiento.

**Documentacion:**
- PRD: PRD-07 Secretaria Academica
- Flow: Reporte de novedades al SIMAT
- Prototipo: (link de Figma)

**Flujo:**
`Novedades de matricula del periodo (altas, retiros, traslados)` -> MANUAL -> `Seleccionar periodo y solicitar generacion del reporte SIMAT` -> AUTOMATICO -> `Sistema valida campos obligatorios, lista incompletos, arma el archivo en el formato oficial del MEN (RR-15) restringido al colegio (RR-01), lo deja disponible para descarga (RI-02) y registra la generacion en el log (RR-03)`
