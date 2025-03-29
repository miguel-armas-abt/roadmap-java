# PATRONES DE DISEÑO DE SOFTWARE

[← Regresar a notas](../../README.md) <br>

---

Los patrones de diseño de software son soluciones generales y reutilizables para problemas comunes en el diseño de software. 
Además, sirven como guía para reducir el acoplamiento e incrementar la cohesión.

---

### DTO (Data Transfer Object)
> Propone crear objetos que encapsulen únicamente datos, sin incluir lógica de negocio. Esto facilita el intercambio de datos entre diferentes capas del sistema.
>
> > #### Convención de nombres
> >- `_Dto`: Encapsula datos para la lógica de negocio o transporte entre capas.
> >- `_Entity`: Encapsula datos provenientes de una base de datos SQL.
> >- `_Document`: Encapsula datos provenientes de una base de datos NoSQL.
> >- `_RequestWrapper`: Encapsula datos de una solicitud hacia un servicio externo.
> >- `_ResponseWrapper`: Encapsula datos recuperados en la respuesta de un servicio externo.
>
> > 💡 Aisla la lógica de negocio de los datos.

### DAO (Data Access Object)
> Propone crear un objeto que encapsule la <u>lógica de acceso a datos</u> de una fuente de datos específica (`SQL`, `CSV`, `REST`, etc), generalmente a través de operaciones CRUD.
>
> > 💡 Aisla la lógica de negocio de la lógica de acceso a datos.

### Repository
> Propone crear un objeto que oculte los detalles de persistencia, combine datos de diversas fuentes (como DAOs) cuando sea necesario, y los transforme en modelos de datos adecuados para la lógica de negocio.
>
> > 💡 Aisla la lógica de negocio de la lógica de acceso a datos.

### Builder
> Propone crear una clase auxiliar (Builder) que construya el objeto DTO paso a paso, configurando solo los atributos necesarios antes de devolver la instancia final.
>
> > 💡 Hace el proceso de instanciación más claro.

### Strategy
> Propone crear una abstracción (clase abstracta o interface) que permita cambiar dinámicamente el comportamiento de un objeto de acuerdo a ciertas condiciones.
>
> > 💡 Añadir nuevas estrategias no afecta las clases existentes.

### Dependency Injection (DI)
> Propone delegar la inyección de las dependencias (objetos que un objeto necesita para funcionar) a otra parte del programa.
>
> ![DI](./../resources/images/20-design-patterns/dependency-injection.png)
> 
> > 💡 Oculta el detalle de implementación de las dependencias. `new Object() ❌`  <br>
> > 💡 Facilita el intercambio de implementaciones.
> 
> > #### DI mediante constructor
> > - Las dependencias se pasan a través del constructor.
> > - Se utiliza para las dependencias <u>obligatorias</u>.
> > - Las variables de instancia pueden ser marcados como `final`, asegurando que no cambien tras la construcción del objeto.
> > - Facilita la creación manual de las dependencias (mocks) en las pruebas unitarias.
>
> > #### DI mediante setters
> > - Las dependencias se pasan después de que el objeto fue creado, utilizando métodos setters.
> > - Se utiliza para dependencias <u>opcionales</u>.

### Service
> Service no es un patrón de diseño formal, pero se utiliza ampliamente para encapsular la lógica de negocio y/o aplicación.

### Mapper
> Mapper no es un patrón de diseño formal, pero se utiliza ampliamente para encapsular la <u>lógica de correspondencia entre atributos</u>.
>
> > 💡 Aisla la lógica de negocio de la lógica mapeo.

--- 

Los siguientes patrones no se implementan directamente con frecuencia, pero frameworks como Spring los utilizan internamente para gestionar eficientemente los objetos y controlar su ciclo de vida.

### Singleton
> Propone crear un objeto que garantice una única instancia en toda la aplicación y proporcione un punto de acceso a ella.
>
> > 💡 Evita instancias innecesarias en memoria.

### Factory
> Propone crear un objeto que facilite la creación de otros objetos sin exponer la lógica de creación ni acoplar el código a clases específicas.
>
> > 💡 Aisla la lógica de creación de objetos.
