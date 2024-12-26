# PRINCIPIOS SOLID

[← Regresar a notas](../../README.md) <br>

---

A continuación, se utiliza con frecuencia el término "componente" para referirnos principalmente a las clases. 
Sin embargo, los principios de diseño de software pueden aplicarse a cualquier elemento de software, como funciones, bibliotecas, APIs, etc.

## 1. Conceptos clave

> #### Acoplamiento
> - Indica en qué medida un componente depende de otros.
> - ⚠️ <u>Alto acoplamiento</u>: Un cambio en un componente puede afecar a otros, dificultando la evolución del sistema.
> - ✅ <u>Bajo acoplamiento</u>: Los componentes son independientes entre sí, lo que facilita el mantenimiento y la flexibilidad ante cambios.

> #### Cohesión
> - Indica en qué medida están bien agrupadas las responsabilidades dentro de un mismo componente.
> - ✅ <u>Alta cohesión</u>: Cada componente hace solo una cosa y la hace bien. Es más fácil de leer y mantener.
> - ⚠️  ️<u>Baja cohesión</u>: Un componente hace demasiadas cosas. Es más confuso y difícil de modificar.

## 2. SOLID
> Son principios de diseño orientado a objetos que sirven como guía para mejorar la calidad del código, hacerlo más flexible y fácil de mantener.

- <u>**S**</u>ingle Responsability *(Responsabilidad única)*
- <u>**O**</u>pen Closed *(Abierto Cerrado)*
- <u>**L**</u>iskov Substitution *(Sustitución de Liskov)*
- <u>**I**</u>nterface Segregation *(Segregación de Interfaces)*
- <u>**D**</u>ependency Inversión *(Inversión de Dependencias)*

### Single Responsability
> - Cada componente debe hacer una sola cosa.
> - Significa que si un componente tiene más de una razón para cambiar, entonces tiene muchas responsabilidades.
>
> > 📌 **Ejemplos** <br>
> > - Si una clase provee lógica de negocio y a la vez lógica de acceso a datos, entonces incumple este principio.
> > - Si una clase provee lógica para consultar transferencias, ejecutar un pago y enviar notificaciones, entonces incumple este principio.

### Open Closed
> - Los componentes deben estar abiertos para agregar nuevas funcionalidades, pero cerrados para modificar lo que ya funciona.
> - `Abierto para su extensión, pero cerrados para su modificación`.
>
> > 📌 **Ejemplos** <br>
> > - Si necesitas añadir una nueva forma de pago, deberías poder hacerlo sin modificar el código existente de las formas de pago actuales.


### Liskov Substitution
> - Las subclases deben comportarse como sus clases base (superclases) sin cambiar el comportamiento esperado. 
> - `Una subclase debe ser sustituible por su superclase`
>
>>  📌 **Ejemplo** <br>
>> ```java
>>  CreditCard classicCard = new ClassicCard();
>>  double benefit = classicCard.calculateBenefit();
>> 
>>  CreditCard goldCard = new GoldCard();
>>  double benefit = goldCard.calculateBenefit();
>> ````

### Interface Segregation
> - Las clases no deben estar obligadas a implementar métodos que no usan.
> - Las interfaces deben ser específicas y contener solo los métodos que las subclases necesitan.
> - Es mejor tener varias interfaces pequeñas y específicas que una única interfaz grande.

### Dependency Inversión
> - Las clases deben depender de abstracciones (interfaces o clases abstractas), no de implementaciones concretas.
> - Se logra mediante la inyección de dependencias (Dependency Injection, DI).
>
>> 📌 **Ejemplo** <br>
>> Incorrecto:
>> ```java
>> public class CreditCardService {
>>   private CreditCardRepository repository;
>> 
>>   public CreditCardService() {
>>     repository = new CreditCardRepositoryImpl(); // depende de una instancia de una clase concreta ❌
>>   }
>> }
>> ```
>>
>> Correcto:
>> ```java
>> public class CreditCardService {
>>   private CreditCardRepository repository;
>> 
>>   public CreditCardService(CreditCardRepository repository) {
>>     this.repository = repository; // no depende de ninguna implementación concreta gracias a la DI ✅
>>   }
>> }
>> ```
