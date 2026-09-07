# Cuentas por cobrar — CxC

## Fuente de verdad

La fuente operativa principal es `Transacciones`.

Una cuenta por cobrar existe cuando una transacción cumple:

- Tipo = `Ingreso`
- Estado pago = `Pendiente`

La vista principal de control es:

- `CxC Mensual`

La antigua pestaña `CxC` fue eliminada y no debe volver a utilizarse como fuente.

---

## Principio contable

CxC representa dinero pendiente de cobrar.

No equivale a cash.

Por lo tanto:

- `Pendiente` → forma parte de CxC.
- `Pagado/Cobrado` → deja de formar parte de CxC.
- Solo los cobros realizados afectan bancos y caja disponible.

Cuando una factura se cobra:

1. localizar la transacción original;
2. cambiar su estado a `Pagado/Cobrado`;
3. registrar `Fecha pago / cobro`;
4. completar banco/cuenta correspondiente;
5. conciliar contra extracto.

Nunca duplicar el ingreso creando otra transacción únicamente para registrar el cobro.

---

## CxC Mensual

`CxC Mensual` es la vista visual de seguimiento.

Cada cliente o grant tiene un bloque con:

- Monto a facturar
- Cobro
- Saldo

Los meses avanzan horizontalmente de enero a diciembre.

### Histórico 2026

Los meses enero–agosto contienen información histórica cargada desde archivos financieros fuente de Sommos.

No modificar ese histórico sin confirmación explícita.

Desde septiembre 2026 en adelante, la vista debe alimentarse principalmente desde `Transacciones`.

---

## Clientes conocidos

La vista puede incluir cuentas como:

- Banco Sol
- BCP Perú
- BCP Perú + Habitat
- UNACEM - Progre Ahorro
- Rendinero
- LARA
- Leads Quiero BCP
- Primaa
- Guerreras Juntas - Caja Los Andes
- Others

Una cuenta puede existir visualmente aunque todavía no tenga movimiento en el periodo.

No eliminar bloques históricos solo porque actualmente estén en cero.

---

## Grants

Los grants deben mantenerse separados conceptualmente de los ingresos operativos.

Grants conocidos:

- INNOVATECH
- Startup Perú
- INCOFIN
- FIID Guatemala

Categoría utilizada:

`Other financing cash flow`

### Regla crítica

Monto aprobado de un grant no equivale automáticamente a CxC.

Solo debe reconocerse como cuenta por cobrar cuando exista:

- desembolso exigible;
- hito cumplido con derecho de cobro;
- factura o solicitud formal;
- calendario documentado que justifique el registro.

No registrar el total aprobado como CxC solo porque existe un convenio.

---

## Programación conocida de grants

### INNOVATECH

Aprobado: USD 90,000.

Los desembolsos deben tratarse según el calendario real documentado y el estado actual del Sheet.

### Startup Perú

Programa finalizado.

Conservar únicamente los importes efectivamente pendientes mientras sigan exigibles.

### INCOFIN

Mantener como vencido mientras el desembolso exigible siga pendiente.

### FIID Guatemala

Los desembolsos futuros deben reconocerse según las fechas documentadas.

Siempre revisar el Google Sheet antes de usar estos datos, porque los pagos pueden haber cambiado desde la última documentación.

---

## Fecha de reconocimiento

Para CxC pendiente:

- usar `Fecha vencimiento` para proyectar el cobro;
- no inventar una fecha si no existe evidencia.

Para cobros realizados:

- usar `Fecha pago / cobro` para identificar el mes real de caja.

El mes de factura y el mes de cobro pueden ser distintos.

---

## Operative incomes

`Operative incomes` es una vista de ingresos por mes y cliente.

No sustituye a `Transacciones`.

Puede combinar histórico cargado desde archivos financieros con información viva del modelo.

No usar el total de `Operative incomes` como cash disponible.

Debe distinguirse entre:

- ingreso registrado/devengado;
- CxC pendiente;
- cobro realizado.

---

## Validaciones obligatorias

Antes de registrar o modificar CxC:

1. leer encabezados actuales de `Transacciones`;
2. buscar duplicados;
3. validar cliente o grant;
4. validar categoría;
5. validar moneda y TC;
6. revisar vencimiento;
7. no inventar país, responsable o banco;
8. verificar actualización de `CxC Mensual`;
9. revisar impacto en `Runway Mensual` y `Dashboard`;
10. buscar errores de fórmulas.

Si el Google Sheet contradice un snapshot documentado en GitHub, prevalece el Google Sheet.
