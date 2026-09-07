# Cuentas por pagar — CxP

## Fuente de verdad

La fuente operativa principal es `Transacciones`.

Una cuenta por pagar existe cuando una transacción cumple:

- Tipo = `Egreso`
- Estado pago = `Pendiente`

La vista principal para control es:

- `CxP Mensual`

Para obligaciones laborales también existe:

- `CxP Sueldos`

La antigua pestaña `CxP` fue eliminada y no debe volver a utilizarse como fuente.

---

## Principio contable

Una obligación pendiente no representa todavía una salida de caja.

Por lo tanto:

- `Pendiente` → forma parte de CxP.
- `Pagado/Cobrado` → deja de formar parte de CxP.
- Solo los movimientos realizados afectan bancos y burn real.

Nunca crear una segunda transacción para registrar el pago de una obligación ya existente.

Cuando se paga:

1. localizar la transacción original;
2. cambiar su estado a `Pagado/Cobrado`;
3. registrar `Fecha pago / cobro`;
4. completar cuenta bancaria si corresponde;
5. conciliar contra el extracto.

---

## CxP Mensual

`CxP Mensual` es la vista de control visual.

Cada proveedor u obligación tiene un bloque con:

- Monto a pagar
- Pago
- Saldo

Los meses avanzan horizontalmente de enero a diciembre.

### Histórico 2026

Los meses enero–agosto contienen histórico cargado desde los archivos financieros fuente de Sommos.

No modificar ese histórico sin confirmación explícita.

Desde septiembre 2026 en adelante, la vista debe alimentarse principalmente desde `Transacciones`.

---

## Fecha de reconocimiento

Para obligaciones pendientes:

- usar `Fecha vencimiento` para determinar el mes esperado de pago;
- si no existe vencimiento documentado, no inventarlo.

Para obligaciones pagadas:

- usar `Fecha pago / cobro` para identificar el mes real de salida de caja;
- si no existe esa fecha, revisar el extracto antes de asumirla.

---

## Gastos recurrentes conocidos

Existen obligaciones recurrentes como:

- PPO
- Big Picture
- Ronny - Sommos
- Caja Nacional de Salud
- Gestora
- IVA Sommos
- IT Sommos
- ChatGPT
- Microsoft
- Claude
- Udemy

Las recurrencias documentadas sirven como referencia, pero no se deben crear deudas futuras automáticamente antes de que corresponda su reconocimiento o exista soporte suficiente.

---

## PPO

PPO corresponde a servicios tercerizados.

Al revisar obligaciones de PPO, considerar el detalle real de las facturas y no consolidar meses distintos si existe documentación separada.

El registro debe conservar:

- fecha de factura;
- importe;
- moneda;
- descripción del periodo;
- vencimiento, cuando esté documentado;
- estado de pago.

---

## CxP Sueldos

Los sueldos por pagar se controlan separadamente en `CxP Sueldos`.

Esta vista puede contener:

- sueldos devengados;
- adelantos;
- pagos;
- saldo pendiente.

No mezclar automáticamente la CxP de proveedores con la CxP laboral.

Ambas forman parte de pasivos para futuros estados financieros, pero deben conservar su naturaleza.

---

## Validaciones obligatorias

Antes de registrar o modificar CxP:

1. leer encabezados actuales de `Transacciones`;
2. buscar si la obligación ya existe;
3. validar categoría;
4. validar moneda y TC;
5. no inventar país, responsable, banco ni vencimiento;
6. verificar que `CxP Mensual` se actualice correctamente;
7. revisar impacto en `Runway Mensual` y `Dashboard`;
8. buscar errores de fórmulas.

Si el Google Sheet contradice un snapshot documentado en GitHub, prevalece el Google Sheet.
