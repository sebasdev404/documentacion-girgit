---
tags:
  - arquitectura
  - rol/coordinador-academico-y-convivencia
  - caso-de-uso
aliases:
  - CU RF-29
---

# ID: RF-29
**Nombre:** Generar reportes de convivencia

**Historia:**
Como Coordinador Academico y de Convivencia necesito generar reportes de convivencia por estudiante, por grupo, por tipologia o por rango de fechas, para hacer seguimiento de casos recurrentes y reincidencia, y para preparar los informes institucionales de convivencia que exige la normativa. Estos reportes consolidan las anotaciones del observador y los casos Ley 1620, y alimentan los reportes oficiales al SIUCE.

**Criterios de aceptacion:**
El coordinador puede generar reportes de convivencia unicamente sobre los datos de su propio colegio (RR-01), filtrando por estudiante, grupo, tipologia de anotacion o periodo. Los reportes respetan la visibilidad de cada anotacion: las marcadas como internas no se exponen a quien no esta autorizado (RN-OE-005 / RN-OB-081), de modo que el reporte refleja solo la informacion que el solicitante puede ver. El reporte consolida anotaciones del observador (RF-26) y casos de convivencia para evidenciar reincidencia y patrones. El coordinador puede descargar el reporte en PDF y preparar el informe institucional que alimenta el reporte oficial al SIUCE dentro de los reportes MEN. La generacion de reportes sobre datos sensibles queda registrada en el log de auditoria del tenant (RR-03). El coordinador no puede acceder al expediente clinico de bienestar; los reportes de convivencia no exponen ese expediente (restriccion del rol, RN-BW-002).

**Documentacion:**
- PRD: PRD-06 Coordinador Academico y de Convivencia
- Flow: Generacion de reportes de convivencia e informe institucional
- Prototipo: (link de Figma)

**Flujo:**
`Anotaciones del observador y casos de convivencia registrados (RF-26, Ley 1620)` -> MANUAL -> `Coordinador selecciona filtros: estudiante, grupo, tipologia o periodo` -> AUTOMATICO -> `Sistema consolida los datos respetando la visibilidad de cada anotacion (RN-OE-005, RN-OB-081)` -> MANUAL -> `Coordinador descarga el reporte en PDF o prepara el informe institucional` -> AUTOMATICO -> `Reporte generado para seguimiento de reincidencia y alimentacion del SIUCE; generacion registrada en el log de auditoria (RR-03)`
