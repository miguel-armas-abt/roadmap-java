# PRINCIPIOS SOLID

[← Regresar a notas](../../README.md) <br>

---

## 1. Conceptos clave

> #### Acoplamiento
> - Indica en qué medida un componente depende de otros.
> - ⚠️ <u>Alto acoplamiento</u>: Un cambio en un componente puede impactar significativamente en otros, dificultando la evolución del sistema.
> - ✅ <u>Bajo acoplamiento</u>: Los componentes son independientes entre sí, lo que facilita el mantenimiento y la flexibilidad ante cambios.

> #### Cohesión
> - Indica en qué medida un componente está enfocado a una única responsabilidad.
> - ✅ <u>Alta cohesión</u>: Facilita el mantenimiento y evolución del software debido a la legibilidad del código.
> - ⚠️  ️<u>Baja cohesión</u>: Los componentes asumen múltiples responsabilidades, lo que los hace difíciles de entender y mantener.

## 2. SOLID
- <u>**S**</u>ingle Responsability *(Responsabilidad única)*
- <u>**O**</u>pen Closed *(Abierto Cerrado)*
- <u>**L**</u>iskov Substitution *(Sustitución de Liskov)*
- <u>**I**</u>nterface Segregation *(Segregación de Interfaces)*
- <u>**D**</u>ependency Inversión *(Inversión de Dependencias)*

### Single Responsability
> 📋 **Definición** <br>
> - Cada componente debe tener una única responsabilidad.
> - Significa que si un componente tiene más de una razón para cambiar, incumple este principio.
>
> 📌 **Ejemplo** <br>
> Si una clase provee lógica de negocio y a la vez lógica de acceso a datos, entonces incumple este principio.

### Open Closed
> 📋 **Definición** <br>
> - Los componentes deben estar <u>abiertos para su extensión, pero cerrados para su modificación</u>.
> - Significa que se debe poder añadir nuevas funcionalidades sin alterar el código existente.
>
> 📌 **Ejemplo** <br>
> Agregar un nuevo tipo de tarjeta implica modificar el método:
> ```java
> public double retrieveBenefit(CreditCard card) {
>   if(card.getType().equals("CLASSIC")) 
>     retrun 0.01;
> 
>   if(card.getType().equals("GOLD")) 
>     retrun 0.02;
> 
>   if(card.getType().equals("PLATINUM")) 
>     return 0.03;
> 
>   return 0.0;
> }
> ```
> 
> 💡 **Solución** <br>
> En general, se debe generar una abstracción de la funcionalidad e implementar cada nuevo tipo en una clase concreta separada.
> ```java
> public abstract class CreditCard {
>   public abstract double getBenefit();
> }
> ```
> ```java
> public class ClassicCard extends CreditCard {
>   @Override
>   public double getBenefit() {
>     return 0.01;
>   }
> }
> ```
> ```java
> public class CreditCardService() {
>   public double retrieveBenefit(CreditCard card) {
>     return card.getBenefit();
>   }
> }
> ```

### Liskov Substitution
> 📋 **Definición** <br>
> Este principio indica que una subclase debe ser sustituible por su superclase. Si al hacer esto el programa falla, entonces estaremos violando este principio.
>
> 📌 **Ejemplo** <br>
>```java
> CreditCard classicCard = new ClassicCard();
> double benefit = retrieveBenefit(classicCard);
>
> CreditCard goldCard = new GoldCard();
> double benefit = retrieveBenefit(goldCard);
>````

### Interface Segregation
> 📋 **Definición** <br>
> - Este principio indica que las clases no deberían verse forzadas a depender de interfaces que no usan.
> - Las interfaces deben ser específicas y contener solo los métodos que realmente se necesitan.
> - Es mejor tener varias interfaces pequeñas y específicas que una única interfaz grande.
>
> 📌 **Ejemplo** <br>
>//ToDo
>
> 💡 **Solución** <br>
> //ToDo

### Dependency Inversión
> 📋 **Definición** <br>
> - Este principio indica que las clases no deberían depender de los detalles de implementación, sino de las abstracciones. 
> - Significa que no se deben instanciar clases concretas en nuestras clases, sino que se deben utilizar solo abstracciones.
> - Se logra mediante la inyección de dependencias.
>
> 📌 **Ejemplo** <br>
> El servicio depende directamente del repository, con lo cual incumple este principio.
> ```java
> public class CreditCardService {
>   private CreditCardRepository repository;
> 
>   public CreditCardService() {
>     repository = new CreditCardRepositoryImpl(); // Dependencia directa
>   }
> }
> ```
>
> 💡 **Solución** <br>
> Implementar inyección de dependencias para manejar las dependencias mediante abstracciones.
> ```java
> public class CreditCardService {
>   private CreditCardRepository repository;
> 
>   public CreditCardService(CreditCardRepository repository) {
>     this.repository = repository;
>   }
> }
> ```
