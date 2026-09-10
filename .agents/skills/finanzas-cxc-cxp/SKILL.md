---
name: finanzas-cxc-cxp
description: Gestiona y audita las cuentas por cobrar, cuentas por pagar, grants y sueldos por pagar de Sommos, separando correctamente devengo, cobro/pago, vencimiento y saldo.
---

# Finanzas Sommos — CxC y CxP

## Propósito

Gestionar la capa de capital de trabajo del workflow financiero de Sommos.

Esta skill es responsable principalmente de:

- `CxC Mensual`;
- `CxP Mensual`;
- `CxP Sueldos`;
- seguimiento de saldos;
- cobros y pagos;
- vencimientos;
- grants;
- obligaciones recurrentes;
- conciliación entre devengo y cash;
- validación de saldos que alimentan Balance Sheet y Cash Flow.

La regla central del modelo es:

**devengo ≠ cash**

Esta skill debe preservar siempre esa separación.

---

# Archivo principal

Google Sheet:

`Finanzas Sommos — Workflow y Control`

Spreadsheet ID:

`1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`

URL:

`https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

Antes de cualquier modificación:

1. leer las pestañas vivas;
2. leer encabezados y fórmulas;
3. identificar el mes afectado;
4. revisar fuentes de devengo;
5. revisar movimientos de cash;
6. revisar saldos anteriores;
7. verificar dependencias posteriores.

Nunca asumir posiciones históricas de filas o columnas.

---

# Pestañas principales

Esta skill opera principalmente:

- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`

Fuentes necesarias:

- `Operative incomes`
- `Real S&A`
- `Sueldos 2026`
- `Transacciones`

También puede consultar:

- `Bancos`
- `Real P&L`
- `Cash Flow`
- `Balance Sheet`
- `Runway Mensual`
- `Dashboard`
- `Config`
- `Reglas categorización`
- `TC BCB`

---

# Arquitectura contable

## Cuentas por cobrar

La lógica oficial es:

`Operative incomes`
→ devengo / monto a facturar

`Transacciones`
→ cobro real

`CxC Mensual`
→ roll-forward y saldo

Conceptualmente:

`Saldo final CxC = Saldo inicial + Monto a facturar - Cobros`

Por lo tanto:

**una CxC no nace únicamente porque exista una transacción marcada Pendiente.**

El derecho de cobro operativo se determina desde el calendario/devengo correspondiente.

---

# Cuentas por pagar

La lógica oficial es:

`Real S&A`
→ devengo / monto a pagar

`Transacciones`
→ pago real

`CxP Mensual`
→ roll-forward y saldo

Conceptualmente:

`Saldo final CxP = Saldo inicial + Monto a pagar - Pagos`

Por lo tanto:

**una CxP no nace únicamente porque exista un Egreso Pendiente en Transacciones.**

El gasto y obligación del periodo se determinan desde el devengo correspondiente.

---

# Sueldos por pagar

La lógica oficial es:

`Sueldos 2026`
→ gasto/devengo de nómina

`CxP Sueldos`
→ sueldo por pagar + adelantos - pagos = saldo

`Transacciones`
→ evidencia bancaria cuando corresponda

`CxP Sueldos` debe mantener separadamente:

- sueldos devengados;
- adelantos;
- sueldos pagados;
- cuenta por pagar de sueldos;
- neto gastado del mes.

El saldo de `CxP Sueldos` alimenta el pasivo del Balance Sheet.

---

# CxC Mensual

## Estructura

Cada cliente utiliza conceptualmente:

- Monto a facturar
- Cobro
- Saldo

Los meses avanzan horizontalmente.

## Monto a facturar

Debe provenir principalmente de:

`Operative incomes`

No calcular el devengo a partir del movimiento bancario.

## Cobro

Debe representar cash efectivamente cobrado o el calendario de cobro validado para forecast.

Para histórico realizado:

usar evidencia de `Transacciones` y conciliación bancaria.

## Saldo

Debe ser roll-forward.

No hardcodear un saldo solamente para conseguir que coincida con un total.

---

# Clientes

Entre las cuentas históricas conocidas pueden aparecer:

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

La estructura viva prevalece.

No eliminar un cliente histórico únicamente porque actualmente tenga saldo cero.

---

# Others en CxC

`Others` puede existir como detalle de conciliación.

Históricamente, el resumen principal de clientes del Control antiguo excluye `Others`.

No cambiar esa lógica sin revisar:

- resumen de CxC;
- Balance Sheet;
- Cash Flow;
- Dashboard.

---

# Grants

Los grants se controlan separadamente de los clientes operativos.

Programas conocidos:

- INNOVATECH
- Startup Perú
- INCOFIN
- FIID Guatemala

Un grant puede tener:

- monto aprobado;
- desembolso programado;
- desembolso exigible;
- cobro;
- saldo.

No confundir el monto total aprobado con una CxC exigible.

---

# Devengo de grants

El calendario financiero validado puede provenir de:

`Operative incomes`

o de la fuente específica utilizada por el modelo vivo.

El grant debe reconocerse según:

- hito;
- calendario;
- exigibilidad;
- documentación.

No registrar automáticamente todo el monto aprobado como CxC.

---

# Cobro de grants

Los cobros deben reflejar:

- cash real para histórico;
- calendario oficial validado para forecast.

Caso histórico conocido:

Startup Perú tiene un desembolso de aproximadamente:

`USD 934`

en septiembre de 2026 dentro del forecast validado.

No eliminar ese cobro sin revisar primero Cash Flow y Balance Sheet.

---

# CxP Mensual

## Estructura

Cada proveedor/concepto utiliza:

- Monto a pagar
- Pago
- Saldo

## Monto a pagar

Debe provenir principalmente de:

`Real S&A`

No derivar el gasto desde el pago bancario.

## Pago

Debe representar la liquidación de la obligación.

Para meses históricos:

debe respetarse la conciliación validada contra el antiguo `Accounts R&P 2` / lógica bancaria correspondiente.

## Saldo

Conceptualmente:

`Saldo actual = Saldo anterior + Devengo - Pago`

---

# Obligaciones recurrentes

Pueden existir conceptos como:

- PPO
- Big Picture
- Ronny - Sommos
- Caja Nacional de Salud
- Gestora
- ChatGPT
- Microsoft
- Anthropic / Claude
- Udemy
- Google Cloud
- IVA Sommos
- IT Sommos
- Marketing
- otros proveedores recurrentes

Que un concepto sea recurrente no significa que el pago deba reconocerse como gasto en el mes de cash.

El devengo sigue viniendo de:

`Real S&A`

---

# PPO

PPO es un caso importante.

Puede existir un único pago bancario que liquide varias facturas.

Cuando exista soporte:

- separar facturas por periodo;
- conservar fecha de factura;
- conservar monto documental;
- mantener fecha real de pago;
- comprobar que la suma de componentes coincida con el movimiento bancario total.

Nunca consolidar devengos de varios meses únicamente porque se pagaron juntos.

---

# Cutoff

El modelo puede contener diferencias entre:

- fecha de cargo;
- periodo contable;
- fecha de cierre.

Por ello:

un cargo bancario no necesariamente elimina una CxP en el mismo periodo.

Caso histórico conocido:

Figma en agosto tuvo movimiento bancario, pero el Control mantuvo la obligación abierta por lógica de cutoff.

No corregir automáticamente estos casos únicamente porque exista cash.

Revisar primero la lógica histórica y documental.

---

# CxP Sueldos

`CxP Sueldos` debe mantenerse alineado con:

`Sueldos 2026`

y con la lógica histórica validada del antiguo:

`Accounts P TH`

La pestaña contiene:

- personas;
- área;
- cargo;
- concepto salarial;
- meses;
- totales;
- sueldos por pagar;
- adelantos;
- sueldos pagados;
- cuenta por pagar;
- neto mensual.

No redondear prematuramente pagos o saldos.

La precisión interna debe conservar los decimales fuente aunque la presentación visual muestre menos.

---

# Adelantos

Los adelantos deben reducir correctamente el saldo pendiente según la lógica de nómina.

No tratarlos automáticamente como un gasto adicional.

El gasto de sueldo se reconoce desde nómina.

El adelanto representa una liquidación parcial o anticipada de esa obligación.

---

# Vencimientos

Una cuenta puede estar:

- vigente;
- vencida;
- pagada/cobrada.

Una obligación vencida sigue siendo una obligación pendiente hasta su liquidación.

Conceptualmente:

`Saldo pendiente > 0`
+
`Fecha vencimiento < hoy`
→ vencida

No usar el vencimiento para modificar el periodo del devengo.

---

# Próximos 30 días

El Dashboard utiliza indicadores de:

- cobros próximos 30 días;
- pagos próximos 30 días.

Estos indicadores deben alimentarse del calendario oficial de:

- CxC;
- CxP;
- CxP Sueldos.

No usar únicamente movimientos bancarios pendientes de `Transacciones`.

El objetivo es mostrar el calendario financiero, no solo movimientos ya cargados en banco.

---

# Estado de pago

`Estado pago` en `Transacciones` es un control operacional.

Puede incluir:

- `Pendiente`
- `Pagado/Cobrado`

Pero:

`Pendiente` no crea automáticamente el devengo.

Y:

`Pagado/Cobrado` no determina automáticamente el mes del P&L.

Su función principal es distinguir si el cash ocurrió.

---

# Liquidación de una obligación existente

Cuando un extracto confirma el pago/cobro de una obligación:

1. buscar la obligación relacionada;
2. validar contraparte;
3. validar monto;
4. validar moneda;
5. registrar Fecha pago/cobro;
6. completar banco/cuenta;
7. actualizar estado;
8. conciliar;
9. verificar CxC/CxP.

Evitar duplicar el hecho económico.

---

# Pagos parciales

Un pago parcial no debe cerrar automáticamente toda la obligación.

Calcular:

`Saldo = Obligación - Pago parcial`

Mantener el saldo restante hasta su liquidación.

---

# Cobros parciales

Misma regla:

`Saldo CxC = Derecho de cobro - Cobro parcial`

No marcar el total como cobrado si queda saldo.

---

# Moneda y TC

La lógica específica pertenece a:

`finanzas-transacciones-tc`

Esta skill debe respetar los montos USD calculados correctamente.

No recalcular TC de forma independiente salvo que sea necesario auditar una diferencia.

---

# Histórico reconciliado

Los históricos ya conciliados no deben modificarse automáticamente.

Actualmente existe una reconciliación validada contra el Control antiguo para:

- CxC Mensual
- CxP Mensual
- CxP Sueldos

especialmente hasta agosto de 2026.

Si una modificación altera ese histórico:

1. identificar la causa;
2. comparar contra la fuente;
3. cuantificar la diferencia;
4. revisar estados financieros;
5. no sobrescribir simplemente porque la nueva fórmula parezca más limpia.

---

# Relación con Real P&L

CxC/CxP no deben determinar directamente los ingresos/gastos del P&L.

La dirección correcta es principalmente:

`Operative incomes`
→ ingresos P&L
→ CxC

`Real S&A`
→ gastos P&L
→ CxP

`Sueldos 2026`
→ salarios P&L
→ CxP Sueldos

No invertir esa lógica.

---

# Relación con Balance Sheet

Los saldos finales alimentan principalmente:

## Activos

- CxC clientes
- grants por cobrar cuando corresponda

## Pasivos

- CxP proveedores
- CxP Sueldos
- otras obligaciones específicas

Antes de modificar un saldo histórico:

revisar el impacto en Balance Sheet.

---

# Relación con Cash Flow

Cash Flow utiliza principalmente:

- cambios de CxC;
- cambios de CxP;
- cambios de CxP Sueldos;
- cobros de grants;
- pagos.

Por ello una modificación en esta skill puede afectar directamente Cash Flow.

Después de cambios materiales comprobar:

`Cash Flow vs Balance Sheet`

---

# Validaciones antes de modificar CxC

- leer `Operative incomes`;
- leer el bloque correspondiente de `CxC Mensual`;
- revisar cobros en `Transacciones`;
- revisar saldo anterior;
- comprobar cliente/grant;
- comprobar mes;
- revisar vencimiento;
- buscar duplicados.

---

# Validaciones antes de modificar CxP

- leer `Real S&A`;
- leer `CxP Mensual`;
- revisar pagos en `Transacciones`;
- revisar saldo anterior;
- comprobar proveedor/concepto;
- comprobar mes;
- revisar cutoff;
- revisar posibles pagos agrupados.

---

# Validaciones antes de modificar CxP Sueldos

- leer `Sueldos 2026`;
- leer `CxP Sueldos`;
- revisar pago/adelanto;
- revisar saldo anterior;
- conservar precisión;
- comparar contra histórico validado si el periodo está cerrado.

---

# QA posterior

Después de cualquier modificación material:

1. releer las celdas modificadas;
2. comprobar monto/devengo;
3. comprobar pago/cobro;
4. comprobar saldo;
5. comprobar roll-forward;
6. revisar `Balance Sheet`;
7. revisar `Cash Flow`;
8. revisar `Dashboard`;
9. comprobar checks del modelo.

Buscar:

- `#REF!`
- `#VALUE!`
- `#N/A`
- `#DIV/0!`
- `#ERROR!`

---

# Regla de reconciliación

Nunca considerar correcta una modificación únicamente porque el saldo final coincida.

Debe verificarse también:

- fuente del devengo;
- fuente del cash;
- periodo;
- signo;
- saldo anterior;
- trazabilidad.

Un saldo correcto obtenido con una fórmula incorrecta sigue siendo un error.

---

# Guardrails

- No confundir devengo con cash.
- No crear CxC solo porque exista un Ingreso Pendiente.
- No crear CxP solo porque exista un Egreso Pendiente.
- No mover ingresos/gastos al mes del cobro/pago.
- No duplicar obligaciones al liquidarlas.
- No inventar vencimientos.
- No inventar pagos/cobros.
- No inventar TC.
- No hardcodear saldos para cuadrar.
- No modificar históricos reconciliados sin revisión.
- No eliminar excepciones de cutoff sin entenderlas.
- No redondear valores fuente innecesariamente.
- No usar CxC/CxP para cuadrar Balance Sheet artificialmente.

---

# Regla de finalización

Una tarea de CxC/CxP solamente está terminada cuando:

- devengo correcto;
- cash correcto;
- saldo correcto;
- roll-forward correcto;
- Balance Sheet consistente;
- Cash Flow consistente;
- checks correctos;
- celdas modificadas releídas en vivo.

Nunca reportar “listo” solamente porque se ejecutó una escritura.

---

# Coordinación con otras skills

## `finanzas-config-categorizacion`

Usar para:

- categorías;
- catálogos;
- reglas de categorización.

## `finanzas-transacciones-tc`

Usar para:

- extractos;
- movimientos bancarios;
- TC;
- cash;
- transferencias;
- conciliación a nivel transacción.

## `finanzas-presupuesto-bancos`

Usar para:

- Bancos;
- presupuesto;
- Budget vs P&L;
- conciliación consolidada.

## `finanzas-runway-dashboard`

Usar para:

- runway;
- próximos cobros/pagos;
- KPIs;
- Dashboard.

## `finanzas-estados-financieros`

Cuando exista, usar para:

- Real P&L;
- Cash Flow;
- Balance Sheet;
- checks de tres estados.

## `finanzas-cierre-mensual`

Cuando exista, usar para:

- cierre mensual completo;
- validación de CxC/CxP;
- estado final `✓ CERRADO`.

---

# Referencias

Consultar cuando corresponda:

- `references/accounts-receivable.md`
- `references/accounts-payable.md`
- `references/estado-pagos.md`

---

# Alcance final

Esta skill debe responder principalmente:

**¿cuánto se devengó, cuánto se cobró/pagó y cuánto sigue pendiente?**

Su objetivo es mantener el capital de trabajo de Sommos:

- correcto;
- trazable;
- reconciliado;
- consistente con P&L;
- consistente con Balance Sheet;
- consistente con Cash Flow.
