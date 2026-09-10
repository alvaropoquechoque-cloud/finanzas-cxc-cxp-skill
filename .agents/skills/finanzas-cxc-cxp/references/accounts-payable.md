# Finanzas Sommos — Cuentas por pagar (CxP)

## Propósito

Documentar la lógica de cuentas por pagar utilizada por Sommos.

Esta referencia pertenece a:

`finanzas-cxc-cxp`

La vista principal es:

`CxP Mensual`

La lógica fundamental es:

`Real S&A → Devengo`
`Transacciones → Pago`
`CxP Mensual → Saldo`

Para nómina:

`Sueldos 2026 → Devengo`
`CxP Sueldos → Pago / Adelanto / Saldo`

---

# Principio contable

CxP representa obligaciones pendientes.

No equivale a:

- gasto de banco;
- cash;
- gasto necesariamente reconocido en el mes de pago.

El mes del gasto y el mes del pago pueden ser distintos.

---

# Fuente del devengo

Para proveedores y gastos operativos, el monto a pagar debe provenir principalmente de:

`Real S&A`

No derivar el gasto desde `Transacciones`.

Conceptualmente:

`Monto a pagar = gasto devengado del periodo`

---

# Fuente del pago

El cash realizado se identifica principalmente desde:

`Transacciones`

utilizando cuando aplique:

- Fecha pago / cobro;
- Banco / cuenta;
- Estado pago;
- referencia;
- conciliación.

---

# Roll-forward

Conceptualmente:

`Saldo final = Saldo inicial + Monto a pagar - Pagos`

Cada periodo debe partir del saldo del mes anterior.

No hardcodear saldos para conseguir que cierre un total.

---

# Estructura CxP Mensual

Cada proveedor/concepto puede contener:

- Monto a pagar
- Pago
- Saldo

No asumir filas fijas sin leer primero la estructura viva.

---

# Obligaciones conocidas

Pueden aparecer conceptos como:

- PPO
- Big Picture
- Ronny - Sommos
- Caja Nacional de Salud
- Gestora
- Vales
- Síndico
- Viáticos
- Retiro
- Uber
- Pasajes
- ChatGPT
- Figma
- Freepik
- Microsoft
- GitHub
- Anthropic
- Udemy
- Google Workspace
- Google Cloud
- Comisiones bancarias
- Exchange
- IVA Sommos
- IT Sommos
- Marketing

La lista viva prevalece.

---

# PPO

PPO es un caso crítico porque un pago bancario puede cubrir varias facturas.

Cuando exista documentación:

mantener separadamente:

- factura;
- fecha documental;
- mes del devengo;
- importe;
- moneda;
- fecha real de pago.

Regla obligatoria:

`SUMA de facturas/componentes = pago bancario total`

No mover todos los devengos al mes del pago.

---

# Pagos agrupados

Un pago puede liquidar múltiples obligaciones.

No obligar una relación uno-a-uno entre:

- movimiento de banco;
- factura.

El objetivo es conservar:

- trazabilidad bancaria;
- trazabilidad documental;
- devengo correcto;
- saldo correcto.

---

# Cutoff

El cierre mensual puede generar casos donde:

- existe cargo bancario;
- pero la obligación permanece abierta al cierre;

o viceversa.

No asumir que cualquier pago bancario elimina automáticamente CxP del mismo mes.

Caso histórico conocido:

Figma en agosto de 2026.

El Control mantuvo el saldo abierto por lógica de cutoff.

Antes de modificar:

revisar la lógica contable y el periodo de cierre.

---

# Viajes Innovatech

Algunos pagos pueden agrupar movimientos relacionados con el proyecto/categoría Innovatech.

No depender únicamente de una descripción literal.

Revisar:

- categoría;
- proyecto;
- concepto;
- documentación.

---

# Bank fees

El Control histórico puede contener importes de comisión que no tienen una única transacción limpia asociada.

No inventar movimientos bancarios para reproducirlos.

Cuando sea necesario mantener una conciliación histórica:

documentar explícitamente la fuente y lógica utilizada.

---

# Impuestos

Conceptos como:

- IVA Sommos;
- IT Sommos;

pueden tener diferencias entre:

- devengo;
- pago;
- saldo.

No asumir que el monto pagado es igual al gasto del mes.

---

# Diferencias de cambio

`Exchange rate differences` puede ser una partida contable y no necesariamente un cash individual equivalente.

No forzar su liquidación desde una transacción bancaria si la lógica del Control demuestra otra metodología.

---

# Interés convertible

El interés de financiamiento convertible debe mantenerse separado cuando el Balance Sheet lo presenta en su propia línea.

No incluirlo automáticamente dentro del saldo general de CxP proveedores si eso genera doble conteo.

---

# CxP Sueldos

La nómina debe gestionarse separadamente de proveedores.

Pestañas:

- `Sueldos 2026`
- `CxP Sueldos`

La estructura conceptual incluye:

- sueldo devengado;
- adelantos;
- pagos;
- saldo.

El saldo final alimenta:

`Balance Sheet`

---

# Precisión de CxP Sueldos

No redondear prematuramente.

El modelo histórico validado conserva decimales exactos.

Por ejemplo, diferencias de centavos pueden afectar:

- Cash Flow;
- Balance Sheet;
- check de caja.

La visualización puede redondear.

La fórmula fuente no debe hacerlo innecesariamente.

---

# Adelantos

Los adelantos:

- no son un gasto adicional;
- reducen la obligación cuando corresponda.

No sumar gasto + adelanto como si fueran dos gastos independientes.

---

# Vencimientos

`Fecha vencimiento` sirve para:

- seguimiento;
- aging;
- pagos próximos;
- vencidos.

No determina el mes de gasto.

---

# Próximos 30 días

El Dashboard debe poder estimar pagos próximos utilizando:

- CxP Mensual;
- CxP Sueldos;
- calendario/vencimientos.

No depender únicamente de transacciones pendientes.

---

# Relación con P&L

La dirección principal es:

`Real S&A`
→ `Real P&L`

y:

`Real S&A`
→ `CxP Mensual`

Para salarios:

`Sueldos 2026`
→ `Real P&L`

y:

`Sueldos 2026`
→ `CxP Sueldos`

No construir gastos P&L desde pagos bancarios.

---

# Relación con Cash Flow

Cash Flow utiliza:

- pagos;
- variación de Accounts Payable;
- variación de CxP Sueldos.

La variación de CxP Sueldos debe estar amarrada al saldo que llega a Balance Sheet cuando corresponda.

---

# Relación con Balance Sheet

El saldo final de:

- CxP proveedores;
- CxP Sueldos;

alimenta pasivos.

Evitar doble conteo de obligaciones presentadas en líneas específicas.

---

# Histórico reconciliado

El histórico hasta agosto de 2026 fue reconciliado contra:

`Accounts R&P 2`

del Control antiguo.

`CxP Sueldos` fue reconciliado contra:

`Accounts P TH`

No modificar estos periodos automáticamente.

---

# QA

Después de modificar CxP comprobar:

- devengo;
- pago;
- saldo;
- saldo anterior;
- concepto;
- periodo;
- cutoff;
- precisión;
- CxP Sueldos si aplica;
- Balance Sheet;
- Cash Flow.

Buscar errores:

- `#REF!`
- `#VALUE!`
- `#N/A`
- `#DIV/0!`
- `#ERROR!`

---

# Guardrails

- No crear CxP solo porque exista un Egreso Pendiente.
- No reconocer gasto nuevamente al pagar.
- No mover el gasto al mes del cash.
- No cerrar una obligación parcial totalmente.
- No eliminar diferencias de cutoff automáticamente.
- No inventar pagos.
- No inventar vencimientos.
- No hardcodear saldos.
- No redondear innecesariamente.
- No mezclar proveedores y sueldos.
- No duplicar el interés del convertible.

---

# Regla final

Para cada cuenta por pagar deben separarse:

1. gasto/devengo;
2. pago;
3. saldo.

El objetivo no es solamente saber cuánto salió del banco.

El objetivo es saber también cuánto se debía y cuánto sigue pendiente.
