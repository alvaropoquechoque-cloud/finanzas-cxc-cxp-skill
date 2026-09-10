# Finanzas Sommos — Cuentas por cobrar (CxC)

## Propósito

Documentar la lógica de cuentas por cobrar utilizada por Sommos.

Esta referencia pertenece a:

`finanzas-cxc-cxp`

La vista principal es:

`CxC Mensual`

La lógica fundamental es:

`Operative incomes → Devengo`
`Transacciones → Cobro`
`CxC Mensual → Saldo`

---

# Principio contable

CxC representa derechos de cobro pendientes.

No equivale a:

- cash;
- saldo bancario;
- ingreso cobrado.

El mes del ingreso y el mes del cobro pueden ser diferentes.

---

# Fuente del devengo

Para clientes operativos, el monto a facturar debe provenir principalmente de:

`Operative incomes`

Por lo tanto:

`Monto a facturar ≠ cobro bancario`

No utilizar movimientos de `Transacciones` para decidir automáticamente cuánto ingreso se devengó en un mes.

---

# Fuente del cobro

Para histórico realizado, el cobro debe estar respaldado principalmente por:

`Transacciones`

y por la conciliación bancaria correspondiente.

Utilizar cuando aplique:

- Fecha pago / cobro;
- Banco / cuenta;
- Estado pago;
- referencia bancaria;
- conciliación.

---

# Roll-forward

Conceptualmente:

`Saldo final = Saldo inicial + Monto a facturar - Cobros`

Cada mes debe continuar desde el saldo anterior.

No hardcodear un saldo final solamente para alcanzar un total esperado.

---

# Estructura de CxC Mensual

Cada cuenta puede contener:

- Monto a facturar
- Cobro
- Saldo

Los meses avanzan horizontalmente.

No asumir posiciones de filas.

Buscar siempre el nombre del cliente/concepto en la hoja viva.

---

# Clientes conocidos

Entre los clientes históricos pueden aparecer:

- Banco Sol
- BCP Perú
- BCP Perú + Habitat
- UNACEM - Progre Ahorro
- Rendinero
- LARA
- Leads Quiero BCP
- Prima
- Guerreras Juntas - Caja Los Andes
- Others

La lista viva prevalece.

No eliminar cuentas históricas únicamente porque estén actualmente en cero.

---

# LARA

Existe un caso histórico donde los cobros asociados a LARA pueden aparecer bajo una descripción bancaria relacionada con:

`CAJA RURAL DE AHORRO Y CREDITO LOS`

o:

`LARA`

No modificar esa lógica sin revisar movimientos históricos.

La categorización específica pertenece a:

`finanzas-config-categorizacion`

---

# Others

`Others` puede utilizarse como detalle de conciliación.

Históricamente, el resumen principal de clientes del Control antiguo excluye `Others`.

No incluirlo automáticamente en el total principal de clientes sin revisar la lógica vigente.

Una modificación puede afectar:

- CxC total;
- Balance Sheet;
- Cash Flow;
- Dashboard.

---

# Grants

Los grants se presentan separadamente de la CxC operativa.

Programas conocidos:

- INNOVATECH
- Startup Perú
- INCOFIN
- FIID Guatemala

Un grant puede tener diferentes estados:

- aprobado;
- programado;
- exigible;
- cobrado;
- pendiente.

No confundir estos conceptos.

---

# Monto aprobado vs CxC

El monto total aprobado de un grant no constituye automáticamente una cuenta por cobrar.

Solo registrar como derecho de cobro cuando exista una base válida como:

- hito cumplido;
- desembolso exigible;
- calendario documentado;
- solicitud aprobada;
- derecho contractual de cobro.

---

# Cobro de grant

Para histórico:

usar cash real cuando exista.

Para forecast:

utilizar el calendario validado del modelo.

Caso conocido:

Startup Perú contempla aproximadamente:

`USD 934`

de cobro en septiembre de 2026 dentro del forecast validado.

No eliminar o mover este cobro sin revisar:

- CxC Mensual;
- Cash Flow;
- Balance Sheet.

---

# Pago/cobro parcial

Si un cliente paga solo una parte:

`Saldo restante = Derecho de cobro - Cobro parcial`

No marcar toda la cuenta como cobrada.

Mantener el saldo pendiente.

---

# Fecha de factura

La fecha de factura/devengo pertenece al reconocimiento del ingreso.

No reemplazarla con la fecha de cash.

---

# Fecha de vencimiento

Se utiliza para:

- seguimiento;
- aging;
- vencidos;
- cobros próximos.

No determina por sí sola el mes del ingreso.

---

# Fecha pago / cobro

Representa cuándo ocurrió el cash.

Se utiliza para:

- cobro mensual;
- Cash Flow;
- conciliación;
- análisis de liquidez.

No modifica automáticamente el periodo de devengo.

---

# CxC vencida

Conceptualmente:

`Saldo pendiente > 0`
+
`Fecha vencimiento < hoy`

→ CxC vencida

Debe seguir existiendo hasta que:

- se cobre;
- se cancele formalmente;
- exista una decisión explícita de baja.

---

# Próximos 30 días

El indicador de cobros próximos 30 días debe utilizar:

- saldos de CxC;
- vencimientos/calendario oficial;
- grants cuando corresponda.

No limitar el cálculo a transacciones bancarias pendientes.

---

# Relación con P&L

La dirección principal es:

`Operative incomes`
→ `Real P&L`

y:

`Operative incomes`
→ `CxC Mensual`

No calcular Revenue del P&L desde el saldo de CxC.

---

# Relación con Cash Flow

Cash Flow utiliza:

- cobros;
- variación de Accounts Receivable;
- grants cobrados.

Una modificación de CxC puede afectar directamente Cash Flow.

---

# Relación con Balance Sheet

El saldo final de CxC alimenta activos.

Antes de modificar un histórico:

revisar el impacto en Balance Sheet.

---

# Histórico reconciliado

El histórico hasta agosto de 2026 fue reconciliado contra el Control antiguo.

No modificarlo automáticamente.

Si una nueva fórmula cambia un mes cerrado:

1. identificar la diferencia;
2. revisar Operative incomes;
3. revisar Transacciones;
4. revisar saldo inicial;
5. comparar contra el Control;
6. revisar estados financieros.

---

# QA

Después de modificar CxC comprobar:

- Monto a facturar;
- Cobro;
- Saldo;
- saldo anterior;
- cliente correcto;
- grant correcto;
- mes correcto;
- Cash Flow;
- Balance Sheet;
- Dashboard.

Buscar además:

- `#REF!`
- `#VALUE!`
- `#N/A`
- `#DIV/0!`
- `#ERROR!`

---

# Guardrails

- No crear CxC únicamente porque exista un Ingreso Pendiente.
- No mover el ingreso al mes del cobro.
- No duplicar un cobro.
- No inventar vencimientos.
- No inventar grants.
- No registrar todo el grant aprobado como CxC.
- No hardcodear saldos para cuadrar.
- No modificar históricos reconciliados sin validación.

---

# Regla final

Para cada cuenta por cobrar deben poder responderse tres preguntas diferentes:

1. ¿Cuánto se devengó?
2. ¿Cuánto se cobró?
3. ¿Cuánto sigue pendiente?

No mezclar esas tres respuestas.
