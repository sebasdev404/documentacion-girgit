# Plataforma SaaS de Gestion Academica

Proyecto de plataforma SaaS para gestion academica y convivencia escolar de colegios privados de Colombia.

## Metodologia de arquitectura

Este proyecto sigue una metodologia propia documentada en la guia adjunta. Antes de tocar cualquier archivo dentro de `Arquitectura/`, lee la guia completa para entender la estructura, las convenciones de IDs (RF-NN, RR-NN, ROL-NN, etc.) y el patron de archivos.

**Adaptacion del proyecto:** la metodologia original definia departamentos. Aqui el alcance es un solo colegio, asi que **no existen departamentos**: la estructura de `Arquitectura/` queda aplanada al nivel del proyecto.

**Guia de referencia obligatoria:**

@_GUIA - Metodologia de Arquitectura.md

## Convenciones del proyecto

- Estructura de `Arquitectura/`:
  - `Arquitectura/_Globales/` con 9 archivos compartidos (Portada, PRD, Tabla de Requerimientos, Por Modulo, Leyenda, Matriz de Permisos, Reglas de Negocio, Criterios de Aceptacion, Dependencias).
  - `Arquitectura/[NN - Rol]/` por cada rol, con 12 archivos numerados (00-11) + `Casos de Uso/`.
- Los IDs siguen el patron documentado en la guia (`RF-NN`, `RR-NN`, `ROL-NN`, `PRD-NN`, `AC-NN`, `RNF-NN`, `RI-NN`).
- Las carpetas de rol usan el mismo orden jerarquico que `Logica del negocio/02-usuarios-roles-y-permisos/roles/`.
- Los archivos de `Logica del negocio/` son la **fuente de verdad** del negocio.
- Las arquitecturas en `Arquitectura/` son la **interpretacion UX/sistema** de esa logica.
- **Sin emojis decorativos en archivos.** Solo simbolos funcionales que la guia define explicitamente (matriz de permisos, leyendas, semaforos).
- Mantener consistencia con el README.md general del proyecto.

## Como trabajar

1. **Antes de crear nueva arquitectura:** lee la guia y el README.
2. **Antes de modificar:** revisa wikilinks y referencias cruzadas en archivos relacionados.
3. **Casos de uso:** usar el formato `RF-NN [Nombre del caso].md`.
4. **Cambios de regla de negocio:** actualizar primero `Logica del negocio/`, luego propagar a `Arquitectura/_Globales/` y a los archivos por rol que dependen.
5. **IDs:** mantener correlativo unico en todo el proyecto (no reiniciar por seccion).
