# PATRONES DE DISEÑO

[← Regresar a notas](../../README.md) <br>

---

> #### Patrón de diseño de software
> - Un patrón de diseño es una solución general y reutilizable para <u>problemas comunes</u> en el diseño de software.
> - Proveen una guía para:
>   - Mejorar la organización del código.
>   - Reducir el acoplamiento.
>   - Incrementar la cohesión.

### DTO (Data Transfer Object)
> 📌 **Problema** <br>
> Transferir datos entre capas de una aplicación sin exponer la lógica de negocio.
>
> 📌 **Solución** <br>
> Crear un objeto que encapsule únicamente los datos necesarios para la transferencia, sin incluir lógica de negocio.
>
> 📌 **Beneficios** <br>
> - `Separación de responsabilidades`: Mantiene aislada la lógica de negocio de los datos.
> - `Reduce el acoplamiento`: Promueve la independencia entre capas.
> 
> 📌 **Convenciones** <br>
> Dependiendo de las convenciones del equipo, los sufijos en los nombres de las clases tipo DTO pueden variar:
> - `_DTO`: Objeto que encapsula los datos útiles para la lógica de negocio o transporte hacia otras capas.
> - `_Entity`: Objeto que encapsula los datos provenientes de una base de datos SQL.
> - `_Model`: Objeto que encapsula los datos provenientes de una base de datos NoSQL.
> - `_RequestWrapper`: Objeto que encapsula los datos que se envían en una solicitud a un servicio externo.
> - `_ResponseWrapper`: Objeto que encapsula los datos que se recuperan en la respuesta de un servicio externo.

### Mapper
> 📌 **Problema** <br>
> Convertir un tipo de objeto a otro.
>
> 📌 **Solución** <br>
> Crear un objeto que encapsule la lógica de correspondencia entre atributos de diferentes modelos.
>
> 📌 **Beneficios** <br>
> - `Separación de responsabilidades`: Evita mezclar la lógica de mapeo con la lógica de negocio.
> - `Reduce el acoplamiento`: Facilita el cambio de estructuras de datos sin impactar otras capas.

### DAO (Data Access Object)
> 📌 **Problema** <br>
> Acceder y manipular datos de una <u>fuente de datos específica</u>.
>
> 📌 **Solución** <br>
> Crear un objeto que encapsule la <u>lógica de acceso a datos</u>, generalmente a través de operaciones CRUD.
>
> 📌 **Beneficios** <br>
> - `Separación de responsabilidades`: Desacopla la lógica de negocio del acceso a datos.
> 
> 📌 **Características** <br>
> - Maneja los datos en su forma persistente.
> - Se aplica a cualquier fuente de datos:
>   - Consultas a bases de datos SQL o NoSQL.
>   - Lectura o escritura de archivos CSV, JSON, XML, etc
>   - Consumo de servicios externos TCP, SOAP o APIs REST.

### Repository
> 📌 **Problema** <br>
> Combinar diversas fuentes de datos, realizar transformacions complejas y abstraer el acceso a datos para que la lógica de negocio no dependa de los detalles de persistencia.
>
> 📌 **Solución** <br>
> Crear una capa de abstracción que utilice DAOs u otras fuentes de datos para entregar modelos de datos más adecuados para la lógica de negocio.
>
> 📌 **Beneficios** <br>
> - `Desacoplamiento`: Separa la lógica de negocio del acceso y manipulación de datos.
>
> 📌 **Características** <br>
> - Combina datos de varias fuentes (DAOs) si es necesario.
> - Transforma los datos hacia DTO, para que sean más útiles en la lógica de negocio. (Se apoya de un mapper).

### Service
> > **Lógica de negocio**: Reglas fundamentales del negocio, como validaciones de negocio, cálculos, etc.
>
> > **Lógica de aplicación**: Tareas que facilitan el funcionamiento de la aplicación, como validaciones generales, mapeos, cifrados, etc.
> 
> 📌 **Problema** <br>
> Encapsular la lógica de negocio y/o aplicación en capas independientes.
>
> 📌 **Solución** <br>
> - Crear uno o más objetos que proporcionen lógica de negocio y/o aplicación reutilizable.
> - Generalmete se accede al DAO o Repository para realizar las operaciones necesarias.
> - Si la lógica de aplicación se torna compleja, es recomendable separarla en otro servicio de tipo "Handler".
>
> 📌 **Beneficios** <br>
> - `Separación de responsabilidades`: Aísla la lógica de negocio y aplicación.

### Builder
> 📌 **Problema** <br>
> Crear objetos complejos con múltiples atributos opcionales, evitando constructores con demasiados parámetros o configuraciones poco claras.
>
> 📌 **Solución** <br>
> Proveer una clase auxiliar (Builder) que construya el objeto paso a paso, configurando solo los atributos necesarios antes de devolver la instancia final.
>
> 📌 **Beneficios** <br>
> - `Legibilidad`: Hace el proceso de instanciación más claro.

### Strategy
> 📌 **Problema** <br>
> Cambiar dinámicamente el comportamiento de un objeto de acuerdo a ciertas condiciones.
>
> 📌 **Solución** <br>
> Crear una interfaz común para un grupo de estrategias e implementar cada comportamiento como una clase concreta.
>
> 📌 **Beneficios** <br>
> - `Abierto - Cerrado`: Añadir nuevas estrategias no requiere modificar las clases existentes.

--- 

Los siguientes patrones no se implementan directamente con frecuencia, pero frameworks como Spring los utilizan internamente para gestionar eficientemente los objetos y controlar su ciclo de vida.

### Singleton
> 📌 **Problema** <br>
> Garantizar que una clase tenga una única instancia global en toda la aplicación.
>
> 📌 **Solución** <br>
> Crear un objeto que controle su propia instancia y proporcione un punto de acceso global a ella.
>
> 📌 **Beneficios** <br>
> - `Optimización de recursos`: Evita instancias innecesarias en memoria.

### Factory
> 📌 **Problema** <br>
> Crear objetos sin exponer la lógica de creación ni acoplar el código a clases específicas.
>
> 📌 **Solución** <br>
> Crear un objeto que actúe como fábrica, encapsulando la lógica de creación de objetos y devolviendo instancias según cierta configuración.
>
> 📌 **Beneficios** <br>
> - `Desacoplamiento`: Quien utiliza el factory no conoce los detalles de la creación del objeto.
> - `Abierto - Cerrado`: Facilita la adición de nuevos tipos de objetos sin modificar el código existente.