# PROGRAMACIÓN ORIENTADA A OBJETOS (POO)

[← Regresar a notas](../../README.md) <br>

---

## 1. Introducción

> #### Constructor
> Es un método que tiene el mismo nombre que la clase y permite la creación o <u>instanciación</u> de un nuevo objeto. El método constructor puede ser sobrecargado.

> #### Sobreecarga
> Se refiere a que una clase tiene métodos con el mismo nombre, pero diferentes tipos de parámetros.

| Clase                                                                  | Objeto                                                                       |
|------------------------------------------------------------------------|------------------------------------------------------------------------------|
| Plantilla que define la estructura de un objeto (atributos y métodos). | Es una instancia creada a partir de la clase. Tiene estado y comportamiento. |

> #### Diferencia entre clase y objeto
> - **Clase**:
>   - Una clase es como un plano arquitectónico de una casa.
>   - El plano <u>**define**</u> todas las características de la casa, como número de habitaciones, tipos de ventana, diseño de las puertas, etc.
>   - Sin embargo, el plano en sí no es una casa, solo es una guía para construirla.
> 
> - **Objeto**:
>   - Cuando la casa se construye a partir del plano, el resultado tangible es el objeto (la casa real).
>   - Este objeto <u>**tiene**</u> todas las características y funciones (baño, cocina, dormitorio, etc).
>   - Cada casa construida a partir del mismo plano puede tener variaciones, como el color de la pintura, decoraciones, etc, pero todas comparten la misma estructura básica definida por el plano.

> #### Instanciar
> Se refiere al proceso de crear un objeto a partir de una clase.
> Al instanciar una clase, se asigna memoria para el nuevo objeto y se inicializan sus atributos.

> #### Variable local
> - Es aquella variable que se declara dentro de un método o bloque de código y solo es accesible dentro de ese contexto.
> - Las variables locales son creadas cuando se entra en el método y son destruidas al salir de él, lo que significa que su alcance está limitado al bloque donde fueron declaradas.
>
> ```java
> public class Application {
>     public static void main(String[] args) {
>         CreditCard card = new PlatinumCard();
> 
>         if(card instanceof PlatinumCard) {
>           String message = "Beneficios: 5% de devolución en compras.";
>           System.out.println(message);
>         }
>
>         // Aquí la variable 'message' no es accesible y causaría error de compilación
>     }
> }
> ````

> #### Variable de instancia
> - Es aquella variable que se declara dentro de una clase pero fuera de cualquier método.
> - Estas variables están asociadas a un objeto específico (una instancia de la clase) y se pueden acceder desde cualquier método de la clase.
> - No pueden ser estáticas.
>
> ```java
>  public class AccountService {
>   
>     private AccountsRepository accountsRepository;
>     
>     public AccountService() {
>       accountsRepository = new AccountsRepository();
>     }
>     
>     public Account findAccountById(Long id) {
>       Account account = accountsRepository.findById(id); // Aquí la variable 'accountsRepository' es accesible, ya que es una variable de instancia
>       return account;
>     }
>  } 
> ```

---

## 2. Pilares de la POO
- Abstracción 
- Encapsulamiento 
- Herencia 
- Polimorfismo

> #### Abstracción
> Capacidad para representar la información que es importante para el contexto del problema.

> #### Encapsulamiento
> Consiste en proteger el estado (atributos) de un objeto de los demás.
> Como regla general, todas las variables de instancia deben ser <u>privadas</u>. Ello se logra con los métodos getters y setters.

> #### Herencia
> Consiste en construir nuevas clases con el estado (atributos) y el comportamiento (métodos) heredados de clases que ya existen.

> #### Polimorfismo (`poli`: muchas, `morfos`: formas)
> Las subclases pueden proporcionar su propia versión o implementación de un método que ya está definido en su superclase.

---

## 3. Herencia en Java

> #### Sobreescritura (@Override)
> Se refiere a que una subclase puede proporcionar una implementación específica de un método que ya está definido en su superclase.
> Cuando un método de la superclase es sobreescrito, la versión de la subclase es utilizada en lugar de la versión de la superclase

> #### Método abstracto
> Es un método de una clase (o también de una interfaz) que no tiene cuerpo o implementación, solamente tiene <u>**declaración**</u>.

> #### Clase abstracta
> Es una clase que tiene como finalidad servir como base para otras clases (clases concretas).
> - No puede instanciarse, solo puede heredarse. Es decir, no se puede crear un nuevo objeto a partir de ella.
> - Se crea utilizando la palabra reservada `abstract` antes del nombre de la clase.
> - Puede tener métodos abstractos y no abstractos.
> - Las clases concretas que extienden de la clase abstracta deben suministrar una implementación para los métodos abstractos

> #### Clase concreta
> Es una subclase de una clase abstracta y suministra la implementación para los métodos abstractos.

> #### Herencia múltiple
> - Consiste en que una clase puede heredar de más de una clase, ello implica que puede adquirir las propiedades y el comportamiento de todas sus superclases. 
> - Java no admite la herencia múltiple.
>
> <img src="../resources/images/oop/multiple_inheritance.png" width="425" height="250">

> #### Interface
> Este concepto nace debido a que Java no puede implementar la herencia múltiple. 
> - Es una plantilla que tiene <u>**declaraciones**</u> de métodos, pero no sus implementaciones.
> - Sus métodos internamente son `public abstract void`.
> - Sus variables internamente son `public static final`.
> - Las clases pueden <u>**implementar**</u> la interface, pero no <u>**extenderla**</u>.
> - Las clases que implementan de una interface deben suministrar una implementación para los métodos declarados en la interface.

| Clase abstracta                                                                                            | Interface                                                                                        |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| Tiene un constructor predeterminado y se llama cada vez que se crea una instancia de la subclase concreta. | No tiene constructor y no puede ser instanciado.                                                 |
| Tiene métodos abstractos y no abstractos                                                                   | Solo tiene métodos abstractos.                                                                   |
| Solo los métodos abstractos deben implementarse en la subclase concreta                                    | Las clases que implementan la interfaz deben suministrar la implementación de todos los métodos. |
| La clase abstracta tiene variables de instancia                                                            | La interfaz sólo tiene constantes.                                                               |

> #### Diferencia entre `this` y `super`
> - `this`
    >   - Hace referencia a la instancia actual del objeto.
>   - Permite usar los métodos y atributos de la clase actual.
>   - Lo podemos omitir cuando hacemos una llamada a un método o atributo de la clase actual, ya que el compilador lo sobreentiende.
> - `super`
    >   - Hace referencia a la instancia de la superclase de nuestro objeto.
>   - Permite acceso a los constructores, métodos y atributos de la superclase.
