# Guía Completa: Estructura de SAP Business One y Maestro de Clientes

## Incluye Hands-on Practice for SAP Business One Logistics Virtual Machine

> Versión ampliada con laboratorios prácticos, ejercicios funcionales, consultas SQL y proyecto integrador.

# 28. Hands-on Practice for SAP Business One - Logistics Virtual Machine

## Objetivo

El propósito de estos laboratorios es que el estudiante:

- Navegue la interfaz de SAP Business One.
- Comprenda la estructura de los datos maestros.
- Cree clientes y contactos.
- Genere documentos de ventas.
- Analice el impacto financiero de las operaciones.
- Realice consultas SQL sobre SQL Server o SAP HANA.

---

# Laboratorio 1 - Exploración del Entorno SAP Business One

## Actividades

1. Iniciar sesión en SAP Business One.
2. Identificar Finanzas, Compras, Ventas, Inventario y Socios de Negocio.
3. Documentar la navegación.

## Evidencia

Captura de pantalla del menú principal.
![alt text](image-2.png)
---

# Laboratorio 2 - Creación de un Cliente

Crear:

Código: C-TRAIN-001
Nombre: Cliente Capacitación
RFC: XAXX010101000
Moneda: MXN

Preguntas:

1. ¿Cuál fue el CardCode? C-TRAIN-001
2. ¿Qué campos son obligatorios? Codigo, nombre, rfc, moneda
3. ¿Qué validaciones realizó SAP?
![alt text](image-3.png)
---

# Laboratorio 3 - Direcciones del Cliente

Agregar direcciones de Facturación y Entrega.

Consulta:

```sql
SELECT *
FROM CRD1
WHERE CardCode='C-TRAIN-001';
```
![alt text](image-4.png)
---

# Laboratorio 4 - Contactos

Registrar dos contactos y validar en OCPR.

```sql
SELECT *
FROM OCPR
WHERE CardCode='C-TRAIN-001';
```
![alt text](image-5.png)
---

# Laboratorio 5 - Condiciones de Pago

Asignar plazo a 30 días.

```sql
SELECT CardCode, GroupNum
FROM OCRD
WHERE CardCode='C-TRAIN-001';
```
![alt text](image-13.png)
![alt text](image-6.png)
---

# Laboratorio 6 - Límite de Crédito

Asignar límite de crédito de 100,000 MXN.

```sql
SELECT CardCode, CardName, CreditLine
FROM OCRD
WHERE CardCode='C-TRAIN-001';
```
![alt text](image-7.png)
---

# Laboratorio 7 - Flujo Comercial Completo

Flujo:

```text
Cliente
 ↓
Cotización (OQUT)
 ↓
Pedido (ORDR)
 ↓
Entrega (ODLN)
 ↓
Factura (OINV)
 ↓
Pago (ORCT)

```

![Cliente](image-8.png)
![Pedido](image-9.png)
![Entrega](image-10.png)
![Factura](image-11.png)
![Pago](image-12.png)

# Laboratorio 8 - Trazabilidad

Utilizar Mapa de Relaciones y documentar los documentos vinculados.
![alt text](image.png)
1. Datos Generales del Flujo
    Socio de Negocios: C-TRAIN-001 - Cliente Capacitación   
    Moneda de la Operación: Peso Mexicano (MXP)   
    Herramienta Utilizada: Mapa de Relaciones (Relationship Map)
2. Lista de Documentos Vinculados en la Cadena de TrazabilidadPaso 
    1: Cotización de VentasNombre en SAP: Sales Quotation (OQUT)
        Número de Documento: 678   
        Fecha: 01/10/2026   
        Importe Total: $76,757.18 MXP   
        Estado del Documento: Cerrado (Closed)   
    Paso 2: Orden de Venta / Pedido
        Nombre en SAP: Sales Order (ORDR)
        Número de Documento: 669   
        Fecha: 01/10/2026   
        Importe Total: $76,757.18 MXP   
        Estado del Documento: Cerrado (Closed)   
    Paso 3: Entrega de Mercancía
        Nombre en SAP: Delivery (ODLN)
        Número de Documento: 657   
        Fecha: 01/10/2026   
        Importe Total: $76,757.18 MXP   
        Estado del Documento: Cerrado (Closed)   
    Paso 4: Factura de Clientes
        Nombre en SAP: A/R Invoice (OINV)
        Número de Documento: 627   
        Fecha: 01/10/2026   
        Importe Total (Con Impuestos): $89,038.33 MXP   
        Estado del Documento: Cerrado (Closed / Reconciliado con saldo en 0)   
    Paso 5: Pago Recibido
        Nombre en SAP: Incoming Payments (ORCT)
        Número de Documento: 113   
        Fecha: 01/10/2026   
        Importe Aplicado: $76,757.18 MXP   
        Estado del Documento: Reconciliado / Aplicado

---

# Laboratorio 9 - Consultas SQL

Clientes activos:

```sql
SELECT CardCode, CardName
FROM OCRD
WHERE CardType='C';
```
![alt text](image-1.png)

Clientes con saldo:

```sql
SELECT CardCode, CardName, Balance
FROM OCRD
WHERE Balance > 0;
```
![alt text](image-14.png)

Clientes y contactos:

```sql
SELECT T0.CardCode,T0.CardName,T1.Name
FROM OCRD T0
INNER JOIN OCPR T1 ON T0.CardCode=T1.CardCode;
```
![alt text](image-15.png)
---

# Laboratorio 10 - Investigación de la Base de Datos

Explorar:

```sql
SELECT TOP 100 * FROM OCRD;
![alt text](image-16.png) 
SELECT TOP 100 * FROM CRD1;
![alt text](image-17.png)
SELECT TOP 100 * FROM OCPR;
![alt text](image-18.png)
SELECT TOP 100 * FROM ORDR;
![alt text](image-19.png)
SELECT TOP 100 * FROM OINV;
![alt text](image-20.png)
SELECT TOP 100 * FROM ORCT;
![alt text](image-21.png)

```

---

# Proyecto Integrador

1. Crear cliente.
![alt text](image-22.png)
2. Configurar direcciones.
![alt text](image-23.png)
3. Crear contactos.
![alt text](image-24.png)
4. Asignar crédito.
![alt text](image-25.png)
5. Crear cotización.
![alt text](image-26.png)
6. Crear pedido.
![alt text](image-27.png)
7. Crear entrega.
![alt text](image-28.png)
8. Facturar.
![alt text](image-29.png)
9. Registrar pago.
![alt text](image-30.png)
10. Obtener reporte SQL.

Consulta final:

```sql
SELECT CardCode, CardName, Balance, CreditLine
FROM OCRD
WHERE CardCode='C-TRAIN-001';
```
![alt text](image-31.png)
---

# Reto Avanzado

Construir una consulta que muestre:

- Cliente
- RFC
- Condición de pago
- Saldo
- Crédito disponible
- Última factura
- Último pago
- Total vendido del año

Utilizando OCRD, OCTG, OINV, INV1, ORCT y RCT2.
