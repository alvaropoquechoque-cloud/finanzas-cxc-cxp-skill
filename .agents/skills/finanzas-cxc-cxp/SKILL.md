---
name: finanzas-cxc-cxp
description: Gestiona cuentas por cobrar, cuentas por pagar, grants, sueldos por pagar, vencimientos y obligaciones recurrentes de Sommos.
---

# Finanzas Sommos — CxC y CxP

## Propósito

Gestionar y auditar las cuentas por cobrar y cuentas por pagar de Sommos sin confundir:

- compromisos futuros;
- obligaciones vencidas;
- movimientos pendientes;
- cobros y pagos realizados;
- caja bancaria real.

Esta skill trabaja sobre el Google Sheet financiero de Sommos y utiliza `Transacciones` como fuente de verdad operativa.

## Archivo principal

- Spreadsheet: `Finanzas Sommos — Workflow y Control`
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

## Pestañas principales

Esta skill opera principalmente:

- `Transacciones`
- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`

También puede consultar:

- `Sueldos 2026`
- `Operative incomes`
- `Real S&A`
- `Bancos`
- `Runway Mensual`
- `Dashboard`
- `Config`
- `Reglas categorización`
- `TC BCB`

## Fuente de verdad

`Transacciones` es la fuente de verdad operativa.

Las pestañas:

- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`

son vistas de control y seguimiento.

No registrar una misma obligación nuevamente en una vista mensual si ya existe en `Transacciones`.

Las antiguas pestañas `CxC` y `CxP` fueron eliminadas y no deben volver a utilizarse.

---

# Cuentas por cobrar

## Regla principal

Una cuenta por cobrar operativa nace cuando existe una transacción con:

- Tipo = `Ingreso`
- Estado pago = `Pendiente`

Mientras permanezca pendiente:

- forma parte de CxC;
- puede afectar la proyección de caja;
- no constituye cash realizado;
- no debe afectar Bancos.

Cuando el dinero sea efectivamente recibido:

- actualizar la misma transacción;
- cambiar el estado correspondiente a `Pagado/Cobrado`;
- registrar `Fecha pago / cobro`;
- conciliar el movimiento contra el extracto bancario.

No crear una segunda transacción para liquidar una CxC existente.

## CxC Mensual

`CxC Mensual` presenta las cuentas por cobrar en formato horizontal por mes.

Cada cuenta tiene un bloque conceptual:

- Monto a facturar
- Cobro
- Saldo

Los meses avanzan hacia la derecha.

Esta pestaña funciona como vista de seguimiento y no reemplaza `Transacciones`.

## Histórico 2026

En `CxC Mensual`:

- enero a agosto de 2026 contienen histórico cargado desde los archivos financieros fuente;
- septiembre de 2026 en adelante debe mantenerse conectado al modelo vivo y a `Transacciones`.

No sobrescribir el histórico enero-agosto sin autorización explícita.

## Clientes y cuentas conocidas

Entre las cuentas conocidas pueden aparecer:

- Banco Sol
- BCP Perú
- BCP Perú + Habitat
- UNACEM - Progre Ahorro
- Rendinero
- LARA
- Leads Quiero BCP
- Guerreras Juntas - Caja Los Andes
- Primaa
- Others

La lista puede crecer.

Antes de crear una nueva cuenta, comprobar si ya existe con otro nombre o variante.

---

# Grants y otros financiamientos

## Regla contable

El monto total aprobado de un grant no equivale automáticamente a CxC.

Distinguir:

1. monto aprobado;
2. monto recibido;
3. desembolso programado;
4. desembolso exigible;
5. desembolso vencido;
6. desembolso efectivamente cobrado.

Un grant puede registrarse como cuenta por cobrar cuando existe un desembolso concreto pendiente o una fecha programada que el modelo financiero de Sommos deba controlar.

## Grants conocidos

Programas documentados incluyen:

- INNOVATECH
- Startup Perú
- INCOFIN
- FIID Guatemala

Los grants deben utilizar la categoría:

`Other financing cash flow`

salvo que la configuración viva del Sheet indique otra cosa.

No tratarlos automáticamente como ingreso operativo ordinario.

## Importante

Antes de crear una nueva CxC de grant:

- buscar duplicados en `Transacciones`;
- revisar desembolsos ya cobrados;
- revisar vencimientos existentes;
- comprobar si el monto representa saldo total aprobado o una cuota específica.

---

# Cuentas por pagar

## Regla principal

Una cuenta por pagar nace cuando existe una transacción con:

- Tipo = `Egreso`
- Estado pago = `Pendiente`

Mientras permanezca pendiente:

- forma parte de CxP;
- puede afectar la proyección de caja;
- no constituye gasto bancario realizado;
- no debe afectar Bancos hasta el pago efectivo.

Cuando se pague:

- actualizar la transacción existente;
- cambiar el estado a `Pagado/Cobrado`;
- registrar `Fecha pago / cobro`;
- conciliar con el extracto bancario.

No duplicar la obligación creando otra transacción de pago.

## CxP Mensual

`CxP Mensual` presenta las obligaciones por proveedor o concepto con estructura:

- Monto a pagar
- Pago
- Saldo

Los meses avanzan horizontalmente.

La vista contiene tanto obligaciones históricas como proveedores recurrentes.

## Histórico 2026

En `CxP Mensual`:

- enero a agosto de 2026 contienen histórico cargado desde los archivos financieros fuente;
- septiembre de 2026 en adelante debe mantenerse conectado a `Transacciones`.

No sobrescribir el histórico anterior sin autorización explícita.

## Obligaciones recurrentes

Una obligación recurrente no significa que deba crearse toda la deuda futura inmediatamente.

Ejemplos conocidos de gastos recurrentes:

- PPO
- Big Picture
- Ronny - Sommos
- Caja Nacional de Salud
- Gestora
- ChatGPT
- Microsoft
- Claude
- Udemy
- IVA Sommos
- IT Sommos

Regla:

Crear la CxP cuando la obligación correspondiente al periodo ya exista o se haya devengado.

No crear automáticamente todos los meses futuros como deuda contable solo porque el proveedor sea recurrente.

---

# PPO

PPO es un proveedor conocido de servicios tercerizados.

Antes de modificar sus obligaciones:

- revisar las facturas existentes;
- revisar el monto en moneda original;
- revisar el TC utilizado;
- evitar consolidar varias facturas como una sola sin respaldo.

El detalle documental conocido incluye facturas mensuales individuales.

Si se recibe un estado de cuenta de PPO, conciliar cada factura contra la obligación correspondiente en `Transacciones` y `CxP Mensual`.

---

# Sueldos por pagar

## Pestañas

La gestión de nómina relacionada con CxP utiliza:

- `Sueldos 2026`
- `CxP Sueldos`

`Sueldos 2026` funciona como maestro y planificación de nómina.

`CxP Sueldos` controla principalmente:

- sueldos devengados;
- adelantos;
- pagos;
- saldos pendientes.

## Regla contable

El gasto de sueldo y el pago del sueldo son eventos relacionados pero conceptualmente distintos.

Un sueldo puede:

1. devengarse;
2. generar una obligación;
3. pagarse posteriormente.

El saldo pendiente debe poder utilizarse posteriormente como pasivo para el Balance General.

No confundir el plan de nómina con deuda efectivamente devengada.

---

# Vencimientos

## Fecha de vencimiento

Cuando exista una fecha contractual o documental:

usar la fecha real.

Cuando el usuario proporcione explícitamente una periodicidad mensual pero no un día contractual, puede utilizarse fin de mes únicamente cuando esa convención esté claramente acordada en el modelo.

Nunca inventar una fecha de vencimiento si no existe evidencia suficiente.

## Cuenta vencida

Una obligación es vencida cuando:

- Estado = `Pendiente`;
- existe Fecha vencimiento;
- Fecha vencimiento < fecha actual.

Esto aplica tanto a CxC como a CxP.

---

# Pago y cobro

## Fecha pago / cobro

`Transacciones` contiene una columna:

`Fecha pago / cobro`

Esta fecha representa cuándo el movimiento fue efectivamente realizado.

Debe utilizarse para:

- conciliación bancaria;
- ubicación mensual de pagos/cobros;
- análisis de caja;
- vistas mensuales.

No sustituir con ella la fecha original de factura o registro.

---

# Relación con extractos bancarios

Cuando se carga un extracto bancario:

1. identificar el movimiento;
2. buscar si ya existe una CxC o CxP pendiente;
3. evitar crear duplicados;
4. actualizar la obligación existente cuando corresponda;
5. registrar fecha real de pago/cobro;
6. completar banco/cuenta;
7. conciliar el movimiento;
8. verificar que el saldo mensual se actualice.

Un movimiento bancario no debe crear automáticamente una nueva CxC/CxP si ya existía una obligación pendiente.

---

# Transferencias internas

Las transferencias internas no representan:

- ingreso operativo;
- gasto operativo;
- CxC;
- CxP.

Deben utilizar:

- Tipo = `Transferencia interna`;
- Categoría = `Transferencias internas`.

Cuando sea posible registrar:

- Cuenta origen
- Cuenta destino
- Detalle transferencia

Las transferencias internas sí afectan los saldos de las cuentas bancarias involucradas, pero no el resultado financiero de la compañía.

---

# Moneda y tipo de cambio

No calcular manualmente conversiones si el Sheet ya dispone de la lógica automática.

Reglas conocidas:

- USD → 1
- SOL → 0.28
- BOB → TC oficial BCB correspondiente a la fecha
- otras monedas → TC manual cuando corresponda

Para BOB:

- usar el TC oficial aplicable a la fecha;
- fines de semana o feriados deben utilizar el último TC oficial disponible anterior o igual a la fecha.

La lógica específica de TC pertenece principalmente a la skill:

`finanzas-transacciones-tc`

---

# Categorías

No inventar categorías.

Si una obligación no puede clasificarse con seguridad:

usar el mecanismo de categorización definido por:

`finanzas-config-categorizacion`

No modificar reglas de categorización desde esta skill salvo que el usuario lo solicite expresamente.

---

# Validaciones antes de escribir

Antes de crear o modificar una CxC/CxP:

1. leer en vivo los encabezados actuales de `Transacciones`;
2. no asumir posiciones históricas de columnas;
3. buscar duplicados;
4. revisar descripción, moneda y monto;
5. revisar estado;
6. revisar vencimiento;
7. comprobar banco/cuenta cuando corresponda;
8. comprobar si existe una obligación previa del mismo concepto;
9. revisar la vista mensual relacionada.

---

# Validaciones después de escribir

Después de una modificación:

1. releer las filas modificadas en `Transacciones`;
2. comprobar `CxC Mensual` o `CxP Mensual`;
3. revisar `CxP Sueldos` si aplica;
4. revisar `Runway Mensual` si cambió un vencimiento;
5. revisar `Dashboard`;
6. revisar `Bancos` si se trató de un pago/cobro realizado;
7. buscar errores como:
   - `#REF!`
   - `#VALUE!`
   - `#N/A`
   - `#ERROR!`

---

# Reglas de seguridad financiera

- `Transacciones` es la fuente de verdad operativa.
- No duplicar movimientos para registrar pagos o cobros.
- Actualizar la obligación original cuando se liquide.
- `Pendiente` no equivale a cash.
- CxC no equivale a ingreso cobrado.
- CxP no equivale a gasto bancario realizado.
- Un grant aprobado no equivale automáticamente a CxC.
- Una recurrencia futura no equivale automáticamente a una deuda devengada.
- No inventar país, banco, responsable, vencimiento o cuenta.
- No inventar movimientos para cuadrar una conciliación.
- No modificar históricos provenientes de archivos fuente sin autorización.
- Si GitHub y el Google Sheet difieren, prevalece el Google Sheet vivo.

---

# Coordinación con otras skills

Usar `finanzas-config-categorizacion` para:

- Config
- catálogos
- validaciones
- reglas automáticas de categorización

Usar `finanzas-transacciones-tc` para:

- importación de extractos
- registro de movimientos
- TC
- transferencias internas
- conversión a USD

Usar `finanzas-presupuesto-bancos` para:

- presupuesto
- conciliación bancaria
- cierre mensual
- diferencias bancarias

Usar `finanzas-runway-dashboard` para:

- cash
- burn
- runway
- proyecciones
- KPIs ejecutivos

Esta skill debe concentrarse en:

- obligaciones pendientes;
- cuentas por cobrar;
- cuentas por pagar;
- vencimientos;
- grants;
- pagos recurrentes;
- sueldos por pagar;
- liquidación de obligaciones.
