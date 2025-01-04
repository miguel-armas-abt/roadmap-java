# BASES DE DATOS

[← Regresar a notas](../../README.md) <br>

---

[1. Conceptos clave](#1-conceptos-clave) <br>
[2. Reglas generales de cardinalidad](#2-reglas-generales-de-cardinalidad) <br>
[3.1. Modelo conceptual](#31-modelo-conceptual) <br>
[3.2. Modelo lógico](#32-modelo-lgico) <br>
[3.3. Modelo físico](#33-modelo-fsico) <br>


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

> #### Llave primaria (PK)
> Es un atributo (o conjunto de atributos) que idetifica de manera única a cada fila de una tabla.

> #### Llave foránea (FK)
> Es un atributo (o conjunto de atributos) que crea una relación entre dos tablas. Este atributo debe coincidir con la llave primaria en la tabla relacionada.
>
> <img src="../resources/images/22-database/foreign-key.svg" width="500" height="348">

> #### Integridad referencial
> Se refiere a la característica de las bases de datos de garantizar que los valores de las llaves foráneas correspondan a una llave primaria existente.

> #### Cardinalidad
> Representa la cantidad de instancias de una entidad que se relacionan con otras entidades.

> #### Transacción
> Se refiere a un conjunto de operaciones que se ejecutan como una unidad indivisible y siguen los principios `ACID`.
> - Commit ✅: Establece que la transacción finalizó exitosamente
> - Rollback ❌: Establece que la transacción falló y se debe reestablecer

--- 

## 2. Diseño de bases de datos
El diseño de bases de datos sigue un conjunto de etapas para garantizar que el sistema de datos sea eficiente, funcional y fácil de mantener.

---

### 2.1. Modelo conceptual
- Consiste en representar gráficamente las entidades, sus atributos y las relaciones entre ellas.
- Se utiliza un "Diagrama Entidad-Relación (ER)" que incluye cardinalidades para representar las relaciones.

> 
> <img src="../resources/images/22-database/ER.svg" width="600" height="260">
>
> - `Un usuario puede solicitar 0 o muchos préstamos` y `un préstamo puede ser solicitado por un solo usuario`.
> - `Un préstamo contiene un solo libro` y `un libro puede estar contenido en 0 o muchos préstamos`.

---

### 2.2. Modelo lógico
Consiste en refinar el modelo conceptual aplicando reglas de cardinalidad para definir dónde ubicar las llaves foráneas.

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

---

No siempre diseñaremos una base de datos desde cero. Puede ocurrir que en algún momento heredemos una base de datos mal 
estructurada y debamos optimizarla. En tal caso, para obtener el modelo lógico hay que aplicar la [normalización](./22.1-normalization/README.md).

---

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
