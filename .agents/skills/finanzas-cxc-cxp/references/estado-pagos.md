# Estado de pagos

## Propósito

Identificar qué obligaciones están:
- Pendientes
- Vencidas
- Pagadas/Cobradas

## Fuente

El estado se deriva de `Transacciones`.

Campos principales:
- Tipo
- Estado pago
- Fecha vencimiento
- Fecha
- Descripción
- Monto
- Moneda
- Responsable

## Reglas

### CxC

`Ingreso + Pendiente` → cuenta por cobrar.

### CxP

`Egreso + Pendiente` → cuenta por pagar.

### Realizado

Cuando cambia a `Pagado/Cobrado`:
- deja de aparecer como pendiente
- puede afectar bancos si existe movimiento bancario real

## Vencido

Una obligación está vencida cuando:
- Estado = Pendiente
- Fecha vencimiento < fecha actual

No modificar automáticamente una obligación vencida a Pagado/Cobrado.

## Conciliación

Pagar o cobrar una obligación no significa inventar una nueva transacción.

Se debe actualizar la transacción fuente correspondiente y luego conciliarla contra el movimiento bancario real.

Nunca duplicar la obligación para registrar su liquidación.
