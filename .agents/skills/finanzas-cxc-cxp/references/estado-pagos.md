# Finanzas Sommos — Estado de pagos y cobros

## Propósito

Documentar cómo interpretar:

- Pendiente;
- Pagado/Cobrado;
- vencido;
- pagos parciales;
- cobros parciales;
- fecha real de liquidación.

Este documento no representa una pestaña llamada `Estado de pagos`.

La antigua pestaña `Estado de pagos` fue eliminada del Google Sheet por ser redundante.

La información vive principalmente en:

- `Transacciones`
- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`

---

# Principio fundamental

El estado de pago responde:

**¿ocurrió el cash?**

No responde por sí solo:

**¿cuándo se devengó el ingreso o gasto?**

Mantener siempre separados:

- devengo;
- vencimiento;
- liquidación;
- conciliación.

---

# Pendiente

`Pendiente` significa que el cash todavía no ha sido liquidado según la evidencia disponible.

Puede corresponder a:

- cobro pendiente;
- pago pendiente;
- grant pendiente;
- obligación pendiente.

Pero:

**Pendiente no crea automáticamente CxC o CxP.**

El devengo oficial se determina desde las fuentes contables correspondientes.

---

# Pagado/Cobrado

`Pagado/Cobrado` significa que existe evidencia suficiente de que el cash ocurrió.

Evidencia habitual:

- extracto bancario;
- comprobante;
- transferencia confirmada;
- cargo automático;
- evidencia equivalente.

Al liquidar revisar:

- Fecha pago / cobro;
- Banco / cuenta;
- monto;
- moneda;
- referencia;
- conciliación.

---

# Fecha pago / cobro

Es la fecha efectiva del cash.

No reemplaza:

- fecha de factura;
- fecha del devengo;
- fecha de vencimiento.

Ejemplo:

factura de julio pagada en agosto:

- devengo → julio
- vencimiento → según factura
- cash → agosto

---

# Vencido

`Vencido` debe entenderse preferentemente como una condición derivada.

Conceptualmente:

`Saldo pendiente > 0`
+
`Fecha vencimiento < hoy`
→ vencido

Una cuenta vencida sigue pendiente hasta su liquidación.

---

# Cuenta por cobrar

Flujo conceptual:

`Operative incomes`
→ monto a facturar
→ `CxC Mensual`

Luego:

`Transacciones`
→ cobro

Finalmente:

`Saldo CxC = saldo anterior + devengo - cobro`

El estado de pago controla el cash, no el devengo.

---

# Cuenta por pagar

Flujo conceptual:

`Real S&A`
→ monto a pagar
→ `CxP Mensual`

Luego:

`Transacciones`
→ pago

Finalmente:

`Saldo CxP = saldo anterior + devengo - pago`

---

# Sueldos

Flujo:

`Sueldos 2026`
→ devengo

`CxP Sueldos`
→ obligación / adelanto / pago / saldo

El pago de nómina no debe generar un segundo gasto.

---

# No duplicación

Cuando un cash claramente liquida una obligación existente:

preferir actualizar la fila/registro existente.

No crear automáticamente:

- factura pendiente;
- otra fila idéntica cobrada;

si ambas representan el mismo hecho económico.

---

# Excepción: múltiples documentos

Un movimiento bancario puede pagar varias facturas.

En ese caso puede existir más de un componente documental.

No confundir:

`una transferencia bancaria`

con:

`una única obligación`

Caso conocido:

PPO.

---

# Pago parcial

Si una obligación de USD 1,000 recibe un pago de USD 400:

el saldo no es cero.

Conceptualmente:

`Saldo = 1,000 - 400 = 600`

Mantener el saldo restante pendiente.

---

# Cobro parcial

Misma lógica.

No marcar como completamente cobrada una factura mientras quede saldo.

---

# Pagos agrupados

Cuando un pago cubre varias obligaciones:

asignar cada componente según la evidencia disponible.

Comprobar:

`SUMA asignada = pago bancario total`

---

# Conciliación

`Pagado/Cobrado` y `Conciliado` son conceptos diferentes.

Un movimiento puede:

- haber ocurrido;
- pero aún no estar completamente conciliado.

La conciliación responde:

**¿el registro coincide con el banco?**

El estado de pago responde:

**¿el cash ocurrió?**

---

# Transferencias internas

No constituyen pago de gasto ni cobro de ingreso por sí mismas.

Usar:

`Tipo = Transferencia interna`

y:

`Categoría = Transferencias internas`

No utilizar estado de pago para convertir una transferencia en ingreso/gasto.

---

# Impacto en Bancos

Solo el cash realizado debe afectar el saldo bancario.

Una obligación pendiente no debe disminuir la caja bancaria.

---

# Impacto en Cash Flow

Cash Flow debe utilizar:

- cobros reales;
- pagos reales;
- variaciones de CxC/CxP.

No usar exclusivamente el Estado pago para construir el estado financiero completo.

---

# Impacto en Dashboard

El Dashboard puede utilizar estados y vencimientos para mostrar:

- CxC vencida;
- CxP próxima;
- cobros próximos 30 días;
- pagos próximos 30 días;
- movimientos sin conciliar;
- cierre mensual.

---

# Mes cerrado

No modificar estados de pagos/cobros de un mes cerrado sin revisar:

- Bancos;
- CxC/CxP;
- Cash Flow;
- Balance Sheet.

Actualmente agosto de 2026 es un periodo validado/cerrado.

---

# QA antes de liquidar

Comprobar:

- obligación correcta;
- contraparte;
- monto;
- moneda;
- fecha;
- banco;
- evidencia;
- si es pago total o parcial.

---

# QA después de liquidar

Revisar:

- Estado pago;
- Fecha pago / cobro;
- conciliación;
- CxC/CxP;
- saldo restante;
- Bancos;
- Cash Flow;
- Balance Sheet.

---

# Guardrails

- No marcar Pagado/Cobrado sin evidencia.
- No considerar vencido como pagado.
- No duplicar una obligación al liquidarla.
- No cerrar pagos parciales completamente.
- No cambiar fecha de devengo por fecha de cash.
- No usar Estado pago para cuadrar estados financieros.
- No inventar fecha de liquidación.
- No inventar banco.

---

# Regla final

Siempre separar estas cuatro preguntas:

**¿Cuándo se devengó?**

**¿Cuándo vencía?**

**¿Cuándo se pagó o cobró?**

**¿Cuándo quedó conciliado?**

Pueden ser cuatro fechas o estados distintos.
