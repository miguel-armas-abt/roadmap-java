# INYECCIÓN DE DEPENDENCIAS (DI)

[← Regresar a patrones de diseño](../README.md) <br>

> ⚠️ **Problema** <br>
> Hacer que los objetos dependan de otros objetos sin tener que instanciarlos por sí mismos.
>
> ✅ **Solución** <br>
> Delegar la inyección de los objetos que un objeto necesita (`dependencias`¹) a otra parte del programa.
>
> 🔍 **Diccionario**
> 1. `Dependencias`: Son los objetos que un objeto necesita para funcionar.
> 
> ![DI](./../../resources/images/20-design-patterns/dependency-injection.png)

### Ventajas
- **Desacoplamiento**: Los objetos no conocen los detalles de implementación de sus dependencias.
- **Flexibilidad**: Facilita el cambio de implementaciones sin modificar el código dependiente.
- **Reusabilidad**: Las clases pueden ser fácilmente reutilizadas.
- **Pruebas unitarias**: Facilita la creación de pruebas unitarias con dependencias simuladas (mocks).

---

### DI mediante constructor
Las dependencias se pasan a través del constructor. Se utiliza para las dependencias obligatorias.

```java
public class CreditCardService {
  private PaymentProcessor paymentProcessor;

  public CreditCardService(PaymentProcessor paymentProcessor) {
    this.paymentProcessor = paymentProcessor;
  }

  public void pay(CreditCard card, double amount) {
    paymentProcessor.process(card, amount);
  }
}
```

### DI mediante setters
Las dependencias se pasan después de que el objeto fue creado, utilizando métodos. Se utiliza para dependencias opcionales.

```java
public class CreditCardService {
  private PaymentProcessor paymentProcessor;
  private NotificationHelper notificationHelper;

  public CreditCardService(PaymentProcessor paymentProcessor) {
    this.paymentProcessor = paymentProcessor;
  }

  public void setNotificationHandler(NotificationHelper notificationHelper) {
    this.notificationHelper = notificationHelper;
  }
  
  public void pay(CreditCard card, double amount) {
    paymentProcessor.process(card, amount);
    if(notificationHelper != null)
      notificationHelper.notify(card, amount);
  }
}
```

### Recomendaciones para DI
Es una buena práctica utilizar inyección por constructor siempre que sea posible por las siguientes razones:
- **Dependencias explícitas**: Los argumentos que requiere el constructor son evidentes.
- **Inmutabilidad**: Los campos de la clase pueden ser marcados como `final`, asegurando que no cambien tras la construcción del objeto.
- **Pruebas unitarias**: Facilita la creación manual de las dependencias (mocks) sin configuraciones adicionales durante las pruebas.
