# PROGRAMACIÓN ORIENTADA A OBJETOS (POO)

[← Regresar a notas](../../README.md) <br>

---

## Pilares de la POO
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
> La herencia solo aplica para miembros (métodos y atributos) <u>públicos</u> y <u>protegidos</u>, ya que los <u>privados</u> no pueden ser heredados.

> #### Polimorfismo
> Las subclases pueden proporcionar su propia versión o implementación de un método que ya está definido en su superclase.
> - `poli`: muchas
> - `morfos`: formas
>
> ```java
> class CreditCard {
>     void showBenefits() {
>         System.out.println("Beneficios: Estándar");
>     }
> }
> 
> class PlatinumCard extends CreditCard {
>     @Override
>     void showBenefits() {
>         System.out.println("Beneficios: 5% de devolución en compras.");
>     }
> }
> 
> class GoldCard extends CreditCard {
>     @Override
>     void showBenefits() {
>         System.out.println("Beneficios: 3% de devolución en compras.");
>     }
> }
> 
> public class Main {
>     public static void main(String[] args) {
>         CreditCard card;
> 
>         card = new PlatinumCard();
>         card.showBenefits(); // Output: Beneficios: 5% de devolución en compras.
> 
>         card = new GoldCard();
>         card.showBenefits(); // Output: Beneficios: 3% de devolución en compras.
>     }
> }
> ```

> #### Sobreescritura (@Override)
> Se refiere a que una subclase puede proporcionar una implementación específica de un método que ya está definido en su superclase.
> Cuando un método de la superclase es sobreescrito, la versión de la subclase se utiliza en lugar de la versión de la superclase

> #### Sobreecarga
> Se refiere a que una clase tiene métodos con el mismo nombre, pero diferentes tipos de parámetros.

> #### Constructor
> Es un método que tiene el mismo nombre que la clase y permite la creación o <u>instanciación</u> de un nuevo objeto. El constructor puede ser sobrecargado.

> #### Instanciar
> Se refiere al proceso de crear un objeto a partir de una clase. 
> Al instanciar una clase, se asigna memoria para el nuevo objeto y se inicializan sus atributos.

> #### Simil entre clase y objeto
> - **Clase**: 
>   - Una clase es como un plano arquitectónico de una casa.
>   - El plano <u>**define**</u> todos las características de la casa, como número de habitaciones, tipos de ventana, diseño de las puertas, etc.
>   - Sin embargo, el plano en sí no es una casa, solo es una guía para construirla.
> - **Objeto**:
>   - Cuando la casa se construye a partir del plano, el resultado tangible es el objeto (la casa real).
>   - Este objeto <u>**tiene**</u> todas las características y puedes utilizar sus funciones (baño, cocina, dormitorio, etc).
>   - Cada casa construida a partir del mismo plano puede tener variaciones, como el color de la pintura, decoraciones, etc, pero todas comparten la misma estructura básica definida por el plano.

| Clase                                                                  | Objeto                                                                       |
|------------------------------------------------------------------------|------------------------------------------------------------------------------|
| Plantilla que define la estructura de un objeto (atributos y métodos). | Es una instancia creada a partir de la clase. Tiene estado y comportamiento. |

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

> #### Diferencia entre THIS y SUPER
> - `this`
>   - Hace referencia a la instancia actual del objeto.
>   - Permite usar los métodos y atributos de la clase actual.
>   - Lo podemos omitir cuando hacemos una llamada a un método o atributo de la clase actual, ya que el compilador lo sobreentiende.
> - `super`
>   - Hace referencia a la instancia de la superclase de nuestro objeto.
>   - Permite acceso a los constructores, métodos y atributos de la superclase.

