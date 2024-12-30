# NORMALIZACIÓN DE BASES DE DATOS

[← Regresar](../README.md) <br>

---

- La normalización es un proceso que <u>se aplica sobre bases de datos mal estructuradas e inconsistente</u>.
- Permite reducir la redundancia y asegurar la consistencia de los datos.

## Caso de uso 
> Gestionar los pedidos de clientes en un restaurante.

### Tabla no normalizada

| order_id | customer_name   | customer_phone | product_name | product_quantity | unit_price | total | address              | district   |
|----------|-----------------|----------------|--------------|------------------|------------|-------|----------------------|------------|
| 1        | Mark Zuckerberg | 987654321      | Pizza        | 1                | 30.00      | 50.00 | Av. Siempre Viva 123 | San Borja  |
| 1        | Mark Zuckerberg | 987654321      | Bebida       | 1                | 20.00      | 50.00 | Av. Siempre Viva 123 | San Borja  |
| 2        | Elon Musk       | 987654322      | Hamburguesa  | 2                | 15.00      | 30.00 | Calle Falsa 456      | Miraflores |

### Primera forma normal (1FN)
> 💡 Cada celda de una tabla debe contener un único valor (datos atómicos) y no debe haber filas duplicadas. <br>
>
> > - Dividir en diferentes tablas con su propia llave primaria.
> > - Dividir en diferentes columnas aquellos atributos que contienen múltiples valores.

---

**customers** (`PK(id)`, `name`, `phone`, `address`, `district`)

| id | name            | phone     | address              | district   |
|----|-----------------|-----------|----------------------|------------|
| 1  | Mark Zuckerberg | 987654321 | Av. Siempre Viva 123 | San Borja  |
| 2  | Elon Musk       | 987654322 | Calle Falsa 456      | Miraflores |

---

**orders** (`PK(id)`, `FK(customer_id)` references a customers, `total`)

| id | customer_id | total |
|----|-------------|-------|
| 1  | 1           | 50.00 |
| 2  | 2           | 30.00 |

---

**order details** (`PK(order_id, product_name)`, `FK(order_id)` references orders, `quantity`, `unit_price`)

| order_id | product_name | quantity | unit_price |
|----------|--------------|----------|------------|
| 1        | Pizza        | 1        | 30.00      | 
| 1        | Bebida       | 1        | 20.00      | 
| 2        | Hamburguesa  | 2        | 20.00      | 

---

### Segunda forma normal (2FN)
> 💡 Todos los atributos no clave deben depender completamente de la llave primaria.
>
> > Si existen atributos que dependen solo parcialmente de la clave primaria, entonces hay que dividir la tabla.

- En la tabla `order_details`, la llave primaria es una combinación del ID del pedido y el producto.
- Se debe crear una tabla separada `products` y mantener solo la referencia en `order_details`.

---

**products** (`PK(id)`, `name`, `unit_price`)

| id | name         | unit_price |
|----|--------------|------------|
| 1  | Pizza        | 30.00      |
| 2  | Bebida       | 20.00      |
| 3  | Hamburguesa  | 15.00      |

----

**order_details** (`PK(order_id, product_id)`, `FK(order_id)` references orders, `FK(product_id)` references products, `quantity`)

| order_id | product_id | quantity |
|----------|------------|----------|
| 1        | 1          | 1        |
| 1        | 2          | 1        |
| 2        | 3          | 2        |

---

### Tercera forma normal (3FN)
> 💡 No debe haber dependencias transitivas (un atributo no clave no debe depender de otro atributo no clave).
>
> > Eliminar columnas que dependan de otras columnas no clave y crear tablas adicionales para ellas.

- La tabla `customers` tiene la siguiente dependencia transitiva:
  - *La dirección depende del cliente*
  - *El distrito depende de la dirección*
  - *¿El distrito depende del cliente?* ❌

- Se debe crear la tabla `addresses` que incluya el distrito para evitar la transitividad.

---

**addresses** (`PK(id)`, `description`, `district`)

| id | description          | district   |
|----|----------------------|------------|
| 1  | Av. Siempre Viva 123 | San Borja  |
| 2  | Calle Falsa 456      | Miraflores |

---

**customers** (`PK(id)`, `name`, `phone`, `FK(address_id)` references addresses)

| id | name            | phone     | address_id |
|----|-----------------|-----------|------------|
| 1  | Mark Zuckerberg | 987654321 | 101        |
| 2  | Elon Musk       | 987654322 | 102        |

---

### Modelo lógico final
> **addresses** (`PK(id)`, `description`, `district`) <br>
> **customers** (`PK(id)`, `name`, `phone`, `FK(address_id)` references addresses) <br>
> **orders** (`PK(id)`, `customer_id`, `total`) <br>
> **products** (`PK(id)`, `name`, `unit_price`) <br>
> **order_details** (`PK(order_id, product_id)`, `FK(order_id)` references orders, `FK(product_id)` references products, `quantity`)
