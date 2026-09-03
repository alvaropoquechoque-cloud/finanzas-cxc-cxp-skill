---
name: finanzas-cxc-cxp
description: Gestiona Estado de pagos, cuentas por cobrar, cuentas por pagar, grants y obligaciones recurrentes de Sommos.
---

# Finanzas Sommos — CxC y CxP

## Propósito

Administrar obligaciones pendientes de cobro y pago, sus vencimientos y su efecto en las proyecciones financieras de Sommos.

Archivo principal:
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

## Alcance principal

Esta skill opera principalmente:
- `Estado de pagos`
- `CxC`
- `CxP`
- `Transacciones`

También puede consultar:
- `Runway Mensual`
- `Dashboard`

## Regla central

`Transacciones` es la fuente de verdad operativa.

- `Ingreso + Pendiente` → CxC
- `Egreso + Pendiente` → CxP
- `Pagado/Cobrado` → deja de formar parte de CxC o CxP pendiente

No escribir manualmente valores en `CxC` o `CxP` si esas pestañas son vistas derivadas de `Transacciones`.

## Cuentas por cobrar

Una cuenta por cobrar no es caja.

### Grants

El monto total aprobado de un grant no debe registrarse automáticamente como CxC.

Registrar únicamente:
- desembolsos exigibles
- hitos aprobados con pago pendiente
- tramos con fecha pactada de cobro

Usar una fila separada por desembolso.

### Clientes

Para clientes recurrentes:
- registrar una obligación por periodo
- evitar duplicar periodos ya cobrados
- verificar si el pago ya fue conciliado antes de crear una nueva fila

## Cuentas por pagar

Registrar una fila por factura, deuda u obligación real.

Los gastos fijos recurrentes se documentan como reglas de recurrencia, pero no deben convertirse automáticamente en deuda de meses futuros antes de que el periodo correspondiente se devengue, salvo instrucción explícita.

## Estado de pagos

La lógica debe permitir identificar:
- Pendiente
- Vencido
- Pagado/Cobrado
- Fecha de vencimiento
- Responsable, cuando exista

Un movimiento pendiente:
- no afecta bancos
- no es gasto realizado
- no es ingreso realizado

## Fechas de vencimiento

- Usar la fecha contractual o la indicada por el usuario.
- No inventar fechas.
- Si solo se conoce el mes, mantener la incertidumbre hasta que exista una convención explícita.
- Si se acuerda una fecha de cierre de mes como convención, documentarla.

## Gastos recurrentes

Cuando una obligación es mensual:
1. documentar el proveedor y monto esperado;
2. documentar la regla de pago;
3. registrar cada factura cuando el periodo se haya devengado;
4. no crear automáticamente todos los meses futuros como CxP contable.

## Validación posterior

Después de registrar o modificar CxC/CxP:
1. verificar `Transacciones`;
2. verificar `CxC` o `CxP`;
3. comprobar vencimientos;
4. revisar impacto en `Runway Mensual`;
5. revisar `Dashboard`;
6. buscar errores de fórmula.

## Reglas transversales obligatorias

- El Google Sheet `Finanzas Sommos — Workflow y Control` es la fuente viva.
- `Transacciones` es la fuente de verdad operativa para movimientos realizados y pendientes.
- Antes de escribir, leer en vivo encabezados, fórmulas, validaciones y filas relacionadas.
- Nunca asumir posiciones históricas de columnas.
- Nunca duplicar una transacción existente.
- Nunca inventar país, categoría, responsable, fecha de vencimiento, cuenta o medio.
- Si no existe una categoría válida, usar `Por categorizar` hasta que se defina una regla.
- `Pendiente` no equivale a dinero realizado ni debe afectar bancos/caja.
- Después de cualquier modificación, verificar las vistas dependientes y buscar errores de fórmula.
- Los snapshots en GitHub documentan contexto; si contradicen el Sheet, prevalece el Sheet.
