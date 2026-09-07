---
name: finanzas-cxc-cxp
description: Gestiona cuentas por cobrar, cuentas por pagar, grants, obligaciones recurrentes y CxP de sueldos de Sommos a partir de Transacciones.
---

# Finanzas Sommos — CxC y CxP

## Propósito

Gestionar las obligaciones pendientes de cobro y pago de Sommos, mantener su trazabilidad mensual y asegurar que los saldos de CxC y CxP sean coherentes con `Transacciones`.

Archivo principal:
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

## Fuente de verdad

`Transacciones` es la fuente de verdad operativa.

Las pestañas:
- `CxC Mensual`
- `CxP Mensual`

son vistas de control y seguimiento.

No deben utilizarse como fuente primaria para crear movimientos si el movimiento ya existe en `Transacciones`.

## Alcance principal

Esta skill opera principalmente:

- `Transacciones`
- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`

Puede consultar:

- `Estado de pagos`
- `Sueldos 2026`
- `Bancos`
- `Runway Mensual`
- `Dashboard`
- `Operative incomes`
- `Real S&A`

## Regla fundamental de CxC

Una cuenta por cobrar operativa nace cuando existe una transacción que representa un derecho de cobro.

Regla general:

- Tipo = `Ingreso`
- Estado pago = `Pendiente`

Ejemplos:
- factura emitida a cliente;
- cuota mensual exigible;
- desembolso de grant ya programado y exigible.

Cuando se recibe el dinero:

- actualizar la transacción existente;
- Estado pago → `Pagado/Cobrado`;
- completar `Fecha pago / cobro`;
- completar cuenta bancaria y conciliación cuando corresponda.

No crear otra transacción para liquidar la misma CxC.

## Regla fundamental de CxP

Una cuenta por pagar nace cuando existe una obligación real y devengada.

Regla general:

- Tipo = `Egreso`
- Estado pago = `Pendiente`

Ejemplos:
- factura de proveedor;
- impuestos por pagar;
- obligación contractual;
- software facturado;
- viáticos reconocidos;
- servicios profesionales devengados.

Cuando se paga:

- actualizar la transacción existente;
- Estado pago → `Pagado/Cobrado`;
- completar `Fecha pago / cobro`;
- completar cuenta bancaria y conciliación cuando corresponda.

No duplicar la obligación para registrar su pago.

## Fechas

Distinguir siempre entre:

### Fecha

Fecha del movimiento, factura, reconocimiento o registro.

### Fecha vencimiento

Fecha en la que la obligación debe ser cobrada o pagada.

Se usa para ubicar obligaciones pendientes en el tiempo.

### Fecha pago / cobro

Fecha real en la que el dinero entró o salió.

Se usa para ubicar el cobro o pago realizado en el mes correcto.

No reemplazar la fecha original de una factura por la fecha de pago.

## Lógica mensual

Las vistas `CxC Mensual` y `CxP Mensual` trabajan con bloques:

- Monto a facturar / Monto a pagar
- Cobro / Pago
- Saldo

Conceptualmente:

`Saldo mes = Saldo anterior + Monto del mes - Cobro/Pago del mes`

Para meses dinámicos:

- el monto se ubica por `Fecha vencimiento` cuando existe;
- si no existe vencimiento, se usa `Fecha`;
- el pago/cobro se ubica por `Fecha pago / cobro`;
- si no existe, se usa `Fecha`.

## Histórico 2026

Actualmente las vistas mensuales contienen histórico enero–agosto 2026 proveniente del archivo financiero histórico utilizado para reconstruir el modelo.

Ese histórico no debe sobrescribirse automáticamente con fórmulas nuevas sin validar primero el impacto.

Desde septiembre 2026 en adelante las vistas continúan alimentándose dinámicamente desde `Transacciones`.

Si el histórico y `Transacciones` presentan diferencias, señalar la discrepancia antes de modificar datos históricos.

## Grants

Los grants se controlan dentro de CxC, pero deben distinguirse de ingresos operativos.

Categoría utilizada:
`Other financing cash flow`

Regla:

`monto aprobado total ≠ CxC automáticamente`

Solo debe registrarse como CxC cuando exista:

- desembolso exigible;
- cuota programada;
- derecho de cobro identificado;
- fecha esperada o vencimiento definido.

No considerar automáticamente todo el grant aprobado como cuenta por cobrar.

Los grants no deben mezclarse con ingresos operativos ordinarios.

## Clientes

Los clientes pueden tener:

- facturas individuales;
- pagos mensuales recurrentes;
- proyectos;
- proof of concept;
- integraciones;
- desarrollos adicionales.

Antes de agregar una nueva CxC:

1. buscar si ya existe en `Transacciones`;
2. revisar `CxC Mensual`;
3. comparar descripción, monto, moneda y fecha;
4. evitar duplicados.

## Proveedores y obligaciones recurrentes

Algunas obligaciones son recurrentes.

Que un gasto sea recurrente no significa que todas sus cuotas futuras sean automáticamente CxP contable.

Regla:

- obligación ya devengada → puede registrarse como CxP;
- gasto futuro todavía no devengado → tratar como proyección o presupuesto;
- no crear deuda contable futura salvo que el usuario indique que ya existe una obligación exigible.

## CxP Sueldos

`CxP Sueldos` controla obligaciones relacionadas con nómina, adelantos, pagos y saldos de sueldos.

El maestro de personas, cargos y planificación se encuentra en:

`Sueldos 2026`

No duplicar información del maestro de sueldos dentro de CxP si ya está enlazada.

Distinguir:

- gasto de sueldo;
- sueldo pagado;
- adelanto;
- saldo pendiente de pago.

`CxP Sueldos` es una fuente complementaria para el pasivo laboral y posteriormente para los estados financieros.

No mezclar automáticamente sus saldos con `CxP Mensual` sin comprobar que no exista duplicidad.

## Estado de pago

Estados operativos principales:

### Pendiente

Existe una obligación o derecho de cobro todavía no realizado.

Afecta:
- CxC o CxP;
- proyección de caja.

No afecta:
- saldo bancario realizado;
- cobro o pago efectivo.

### Pagado/Cobrado

El movimiento ya ocurrió financieramente.

Debe tener, cuando sea posible:

- cuenta bancaria;
- conciliación;
- fecha pago / cobro.

Deja de formar parte de la obligación pendiente.

## Conciliación con extractos

Cuando un extracto bancario confirma un cobro o pago:

1. buscar primero la obligación existente;
2. verificar monto, moneda, contraparte y fecha;
3. actualizar la transacción existente;
4. marcar `Pagado/Cobrado`;
5. completar `Fecha pago / cobro`;
6. asignar cuenta bancaria;
7. conciliar;
8. verificar `CxC Mensual` o `CxP Mensual`.

No crear un segundo movimiento si se trata de la liquidación de una obligación existente.

## Control de duplicados

Antes de crear una obligación buscar coincidencias por:

- contraparte;
- descripción;
- monto;
- moneda;
- período;
- factura;
- vencimiento.

Si existe una coincidencia razonable, detenerse y revisar antes de escribir.

## Validaciones después de modificar

Después de cualquier cambio relacionado con CxC o CxP:

1. volver a leer la transacción modificada;
2. revisar `CxC Mensual` o `CxP Mensual`;
3. comprobar el saldo mensual;
4. revisar `Runway Mensual` si cambia un vencimiento;
5. revisar `Dashboard` si cambia un pendiente;
6. revisar `Bancos` si hubo pago o cobro;
7. buscar errores `#REF!`, `#VALUE!`, `#N/A` o `#ERROR!`.

## Reglas transversales obligatorias

- El Google Sheet es la fuente viva.
- Leer encabezados y fórmulas actuales antes de escribir.
- Nunca asumir posiciones históricas de columnas.
- Nunca duplicar una obligación para registrar su liquidación.
- Nunca inventar fechas de vencimiento.
- Nunca inventar país, responsable, proveedor, cliente o cuenta bancaria.
- `Pendiente` no significa dinero realizado.
- Un grant aprobado no significa CxC total.
- Una recurrencia futura no significa deuda devengada.
- No modificar históricos sin identificar primero su fuente.
- Si GitHub y el Google Sheet se contradicen, prevalece el Google Sheet.
