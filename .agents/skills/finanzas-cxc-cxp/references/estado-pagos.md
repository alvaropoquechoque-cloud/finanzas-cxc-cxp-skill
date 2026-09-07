# Estado de pagos y cobros

## Propósito

Definir cómo se interpreta y actualiza el estado financiero de una transacción desde su registro hasta su conciliación bancaria.

La fuente de verdad es `Transacciones`.

---

## Estados principales

### Pendiente

La obligación o derecho de cobro existe, pero todavía no se ha realizado financieramente.

Ejemplos:

- factura de proveedor pendiente de pago;
- factura de cliente pendiente de cobro;
- desembolso de grant exigible pero aún no recibido;
- sueldo devengado pendiente.

Un movimiento `Pendiente`:

- sí puede formar parte de CxC o CxP;
- sí puede afectar Runway como compromiso futuro;
- no afecta saldo bancario;
- no representa ingreso o egreso realizado.

---

### Pagado/Cobrado

El movimiento ya ocurrió financieramente.

Debe existir evidencia suficiente, normalmente:

- extracto bancario;
- comprobante;
- transferencia confirmada;
- cargo automático;
- conciliación equivalente.

Al cambiar un movimiento a `Pagado/Cobrado`, registrar cuando sea posible:

- `Fecha pago / cobro`;
- cuenta bancaria;
- conciliación;
- información de transferencia si corresponde.

---

## Vencido

`Vencido` es una condición derivada, no necesariamente un estado manual.

Conceptualmente:

`Pendiente + Fecha vencimiento anterior a hoy = Vencido`

Una obligación vencida sigue siendo `Pendiente` hasta que se pague o cobre.

No cambiarla a `Pagado/Cobrado` únicamente porque pasó la fecha.

---

## Flujo recomendado

### Cuenta por pagar

`Egreso + Pendiente`
→ aparece en `CxP Mensual`
→ se paga
→ actualizar transacción original
→ `Pagado/Cobrado`
→ registrar fecha real
→ conciliar banco
→ desaparece del pendiente futuro.

### Cuenta por cobrar

`Ingreso + Pendiente`
→ aparece en `CxC Mensual`
→ se cobra
→ actualizar transacción original
→ `Pagado/Cobrado`
→ registrar fecha real
→ conciliar banco
→ desaparece del pendiente futuro.

---

## Regla de no duplicación

Nunca crear una segunda transacción únicamente para liquidar una cuenta pendiente existente.

Ejemplo incorrecto:

- Factura BCP: Ingreso + Pendiente
- luego crear otra fila adicional: Ingreso + Cobrado

Eso duplicaría el ingreso.

Procedimiento correcto:

- localizar la factura original;
- cambiar su estado;
- agregar `Fecha pago / cobro`;
- completar datos bancarios.

---

## Conciliación bancaria

Solo movimientos realizados deben afectar `Bancos`.

La conciliación debe comprobar:

`Saldo inicial + Ingresos realizados - Egresos realizados = Saldo final calculado`

Luego comparar contra el saldo real del banco.

Nunca crear movimientos artificiales para hacer que la conciliación llegue a cero.

Si existe diferencia:

1. revisar movimientos faltantes;
2. revisar duplicados;
3. revisar transferencias internas;
4. revisar dirección de transferencia;
5. revisar fechas;
6. revisar moneda y TC;
7. revisar comisiones;
8. revisar el extracto original.

---

## Transferencias internas

Las transferencias entre cuentas propias no son ingreso ni gasto operativo.

Deben identificarse como:

- Tipo relacionado con transferencia interna;
- Categoría = `Transferencias internas`;
- Cuenta origen;
- Cuenta destino.

Una transferencia debe afectar dos cuentas bancarias, pero no debe inflar ingresos, gastos ni burn.

---

## Fecha pago / cobro

`Fecha pago / cobro` representa la fecha financiera real de la liquidación.

No reemplaza:

- fecha de factura;
- fecha de registro;
- fecha de vencimiento.

Las tres fechas cumplen funciones distintas.

Esta fecha es especialmente importante para:

- conciliación bancaria;
- Real S&A;
- Operative incomes;
- CxC Mensual;
- CxP Mensual;
- flujo de caja;
- futuros estados financieros.

---

## Controles antes de cerrar

Antes de considerar una obligación liquidada:

- verificar evidencia bancaria;
- confirmar monto;
- confirmar moneda;
- confirmar cuenta;
- confirmar fecha;
- mantener la misma transacción fuente;
- revisar conciliación;
- comprobar vistas dependientes.

Si existe contradicción entre documentación histórica y el Google Sheet actual, prevalece el Google Sheet.
