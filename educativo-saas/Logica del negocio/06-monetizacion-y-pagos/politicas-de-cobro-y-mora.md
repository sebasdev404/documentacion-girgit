---
titulo: Políticas de cobro y mora
modulo: monetizacion-y-pagos
tipo: regla
estado: borrador
tags: [cobro, mora, intereses]
---

# Políticas de cobro y mora

## Fechas de corte y vencimiento

Cada cuota tiene tres fechas relevantes, configurables por colegio:

| Fecha | Significado |
| --- | --- |
| Fecha de generación | El sistema crea la cuota y la notifica al acudiente. |
| Fecha límite ordinaria | Hasta esta fecha el pago se hace sin recargo. |
| Fecha límite con recargo | A partir de aquí entra mora; se aplican intereses y/o recargos. |

Las fechas se definen por concepto (matrícula, pensión, transporte) o globalmente.

## Recordatorios automáticos

| Hito | Notificación |
| --- | --- |
| Generación | "Tu pago de [periodo] ya está disponible". |
| Pre-vencimiento (configurable: T-7, T-3, T-1) | Recordatorio amistoso. |
| Día del vencimiento | Aviso firme. |
| Post-vencimiento (T+1, T+3, T+7, T+15) | Aviso de mora con valor actualizado. |

Cada colegio puede ajustar la cadencia.

## Cálculo de intereses de mora

- Interés de mora calculado según la **tasa** configurada por el colegio (anual / mensual).
- Se respetan los topes legales del país (ej. en Colombia, tasa de usura).
- Se acumulan diariamente desde el día siguiente al vencimiento ordinario.
- Visible en el desglose de la cuota antes de pagar.

## Recargos administrativos

- Adicional al interés, el colegio puede aplicar un **recargo administrativo fijo** o porcentual.
- Aplicable una sola vez al entrar en mora, o de forma escalonada (cada 15 días).

## Acuerdos de pago

- El colegio puede pactar con el acudiente un acuerdo de pago: dividir el saldo en cuotas con fechas específicas.
- El acuerdo queda registrado con autor, fecha y soporte adjunto.
- Mientras se cumpla el acuerdo, no se aplican intereses adicionales sobre el saldo del acuerdo.
- El incumplimiento de una cuota del acuerdo lo cancela y reactiva la mora normal.

## Suspensión de servicios por mora

- El colegio define la política de suspensión: por ejemplo, restringir entrega de boletines o paz y salvo cuando hay deuda.
- La plataforma NO suspende automaticamente el acceso del estudiante al módulo académico (se considera derecho fundamental, especialmente en Colombia).
- El sistema marca al estudiante como **"con cartera vencida"** y dispara los flujos de comunicación y restricción configurados.

## Reglas de negocio

- **RN-CM-001 — Cartera no bloquea académico:** la deuda no impide al estudiante consultar sus notas, asistencia y observador.
- **RN-CM-002 — Topes legales:** la tasa de interés aplicada respeta el tope legal del país.
- **RN-CM-003 — Acuerdo de pago auditable:** todo acuerdo queda registrado con autor, fecha, condiciones y soporte.
- **RN-CM-004 — Boletín restringible:** el colegio puede configurar que la entrega del boletín final requiera estar al día; aplica como configuración, no por defecto.
- **RN-CM-005 — Paz y salvo:** un estudiante con cartera vencida no puede emitir [[paz-y-salvo|paz y salvo]] hasta normalizar.
- **RN-CM-006 — Cálculo transparente:** el desglose de mora (capital, interés, recargo) es visible al pagador antes de confirmar el pago.

## Notas y pendientes

- Definir la lista exacta de servicios que el colegio puede restringir por cartera, evitando los protegidos por ley.
- Validar la política para estudiantes nuevos vs antiguos en mora.
