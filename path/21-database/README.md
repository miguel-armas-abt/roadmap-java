# BASES DE DATOS

[← Regresar a notas](../../README.md) <br>

---

[1. Conceptos clave](#1-conceptos-clave) <br>
[2.1. Modelo conceptual](#21-modelo-conceptual) <br>
[2.2. Modelo lógico](#22-modelo-lógico) <br>
[2.3. Modelo físico](#23-modelo-físico) <br>

---

## 1. Conceptos clave

> #### Dato e información
> - Un **dato** es un valor aislado sin contexto. Por ejemplo, `45.00` o `Mark`.
> - **Información** es el conjunto de datos en un contexto que proporcionan un significado. Por ejemplo, `Mark` tiene un saldo de `S/ 45.00`.

> #### Base de datos
> Es un contenedor donde se guardan datos estructurados que pueden ser consultados o manipulados.

> #### Sistema gestor de base de datos (SGBD)
> Es el software que se utiliza para interactuar con las bases de datos. Actúa como intermediario entre el usuario y las bases de datos.
> - MySQL
> - PostgreSQL
> - Oracle Database
> - Microsoft SQL Server
> - CosmosDB

> #### Llave primaria (PK)
> Es un atributo (o conjunto de atributos) que idetifica de manera única a cada fila de una tabla.

> #### Llave foránea (FK)
> Es un atributo (o conjunto de atributos) que crea una relación entre dos tablas. Este atributo debe coincidir con la llave primaria en la tabla relacionada.

> #### Cardinalidad
> Representa la cantidad de instancias de una entidad que se relacionan con otras entidades.

> #### Integridad referencial
> Se refiere a la característica de las bases de datos de garantizar que los valores de las llaves foráneas correspondan a una llave primaria existente.

> #### Transacción
> Se refiere a un conjunto de operaciones que se ejecutan como una unidad indivisible y siguen los principios ACID.
>   - `A`: Atomicidad
>   - `C`: Consistencia
>   - `I`: Aislamiento
>   - `D`: Durabilidad

--- 

## 2. Diseño de bases de datos
El diseño de bases de datos sigue un conjunto de etapas para garantizar que el sistema de datos sea eficiente, funcional y fácil de mantener.


### 2.1. Modelo conceptual
> - Consiste en representar gráficamente las entidades, sus atributos y las relaciones entre ellas.
> - Se utiliza un "Diagrama Entidad-Relación (ER)" que incluye cardinalidades para representar las relaciones.
>
> > **Caso de uso**: Gestionar el préstamo de libros de una biblioteca.
> 
<img src="../resources/images/database/ER.svg" width="600" height="260">

- `Un` usuario puede solicitar `0 o muchos` préstamos.
- `Un` préstamo puede ser solicitado por `un` solo usuario.
- `Un` préstamo contiene `un` solo libro.
- `Un` libro puede estar contenido en `0 o muchos` préstamos.

### 2.2. Modelo lógico
> - Consiste en refinar el modelo conceptual mediante el proceso de normalización.
> - La normalización permite reducir la redundancia y asegurar la consistencia de los datos.
> 
> > **Caso de uso**: Gestionar los pedidos de clientes en un restaurante.

*Tabla no normalizada:*

| order_id | customer_name   | customer_phone | product_name | product_quantity | unit_price | total | address              | district   |
|----------|-----------------|----------------|--------------|------------------|------------|-------|----------------------|------------|
| 1        | Mark Zuckerberg | 987654321      | Pizza        | 1                | 30.00      | 50.00 | Av. Siempre Viva 123 | San Borja  |
| 1        | Mark Zuckerberg | 987654321      | Bebida       | 1                | 20.00      | 50.00 | Av. Siempre Viva 123 | San Borja  |
| 2        | Elon Musk       | 987654322      | Hamburguesa  | 2                | 15.00      | 30.00 | Calle Falsa 456      | Miraflores |

> #### 2.2.1. Primera forma normal (1FN)
> **Objetivo:** <br>
> Cada celda de una tabla debe contener un único valor (datos atómicos) y no debe haber filas duplicadas. <br>
>
> **¿Cómo se logra?** <br>
> - Dividir en diferentes tablas con su propia llave primaria.
> - Dividir en diferentes columnas aquellos atributos que contienen múltiples valores.

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

> #### 2.2.2. Segunda forma normal (2FN)
> **Objetivo**: <br>
> Todos los atributos no clave deben depender completamente de la llave primaria.
>
> **¿Cómo se logra?** <br>
> Si existen atributos que dependen parcialmente de la clave primaria, entonces hay que dividir la tabla.

- En la tabla `order_details`, la llave primaria es una combinación del ID del pedido y el producto. 
- En la tabla `order_details` los atributos `product_name` y `unit_price` no dependen completamente de la llave compuesta.
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

> #### 2.2.3. Tercera forma normal (3FN)
> **Objetivo**: <br>
> No debe haber dependencias transitivas (un atributo no clave no debe depender de otro atributo no clave).
>
> **¿Cómo se logra?** <br>
> Eliminar columnas que dependan de otras columnas no clave y crear tablas adicionales para ellas.

- La tabla `customers` tiene la siguiente dependencia transitiva:
  - customers.id → address *(La dirección depende del cliente)*
  - address → district *(El distrito depende de la dirección)*
  - ¿El distrito depende del cliente? Esto viola la 3FN, ya que el distrito no depende directamente del cliente, sino de un atributo no clave de la dirección.
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

> **Modelo lógico final**: <br><br>
> **addresses** (`PK(id)`, `description`, `district`) <br>
> **customers** (`PK(id)`, `name`, `phone`, `FK(address_id)` references addresses) <br>
> **orders** (`PK(id)`, `customer_id`, `total`) <br>
> **products** (`PK(id)`, `name`, `unit_price`) <br>
> **order_details** (`PK(order_id, product_id)`, `FK(order_id)` references orders, `FK(product_id)` references products, `quantity`)

### 2.3. Modelo físico
El siguiente script funciona para MySQL.


```sql
CREATE TABLE addresses (
    id INT AUTO_INCREMENT PRIMARY KEY,
    description VARCHAR(255) NOT NULL,
    district VARCHAR(100) NOT NULL
);

CREATE TABLE customers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(15) NOT NULL,
    address_id INT NOT NULL,
    FOREIGN KEY (address_id) REFERENCES addresses(id)
);

CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    total DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);

CREATE TABLE products (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10, 2) NOT NULL
);

CREATE TABLE order_details (
    order_id INT NOT NULL,
    product_id INT NOT NULL,
    quantity INT NOT NULL,
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);

```

### 2.4. Reglas generales de cardinalidad

> #### 1:1
> - La FK se puede colocar en cualquiera de las dos tablas.
> > **users** (`PK(id)`, `username`) <br>
> > **personal_details** (`PK(id)`, `FK(user_id)` references users, `full_name`)

> #### 1:N
> - La FK se coloca en la tabla del lado "muchos".
> - Es más eficiente asociar cada registro de "muchos" con un único registro de "uno".
> > **customers** (`PK(id)`, name) <br>
> > **orders** (`PK(id)`, `FK(customer_id)` references customers, `total`)

> #### N:N
> - Se necesita una tabla intermedia (tabla de unión) para manejar la relación.
> - La tabla intermedia contiene 2 llaves foráneas, que referencian a las llaves primarias de las tablas involucradas.
> - ⚠️ La relación N:N no puede implementarse directamente en un modelo relacional.
> > **students** (`PK(id)`, name) <br>
> > **courses** (`PK(id)`, title) <br>
> > **students_courses** (`PK(student_id, course_id)`, `FK(student_id)` references students, `FK(course_id)` references courses) <br>