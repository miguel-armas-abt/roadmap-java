# CONTEXT DEPENDENCY INJECTION (CDI)

[← Regresar a notas](../../README.md) <br>

---

CDI es una especificación dentro de Jakarta EE que proporciona un marco para la inyección de dependencias (DI)
y la gestión del ciclo de vida de los componentes en aplicaciones Java sin necesidad de un contenedor de IoC tradicional.

> #### 🔎 Diccionario
> 1. `Ámbitos`: Anotaciones que especifican al CDI el ciclo de vida asignado a los beans dentro de la aplicación.
> 2. `Beans`: Representan a los objetos que son instanciados, configurados y destruidos por el CDI.

## Características
- Soporte para la DI en Java.
- Define varios `ámbitos` que gestionan el ciclo de vida de los `beans`.
- Soporte para publicar y suscribir eventos dentro de la aplicación.
- Carga de beans personalizados con `@Produces`.
- Soporta interceptores y decoradores para añadir comportamiento adicional a los beans.

## Declaración de dependencias
Jakaarta EE utiliza ámbitos para definir los beans gestionados por el CDI.

| Ámbitos              | Descripción                                                                                                                          |  
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| `@Produces`          | Anotación utilizada en métodos para producir beans que no pueden ser gestionadas directamente por la aplicación (beans de terceros). |
| `@ApplicationScoped` | Indica que una clase es un bean disponible durante toda la vida de la aplicación.                                                    |
| `@Singleton`         | Indica que una única instancia del bean será compartida en toda la aplicación.                                                       |
| `@RequestScoped`     | Anota una clase para indicar que sus instancias deben ser creadas una vez por cada solicitud HTTP.                                   |

```java
@ApplicationScoped
public class Properties {
  //...
}

@Singleton
public class RestTemplateConfig {

  @Produces
  @Default
  public RestTemplate restTemplate(Properties properties) {
    return new RestTemplate(properties);
  }
}
```

## Inyección por constructor

```java
@Singleton
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

## Inyección automática
Jakarta EE utiliza anotaciones para inyectar beans automáticamente.

| Anotación | Descripción                                                                                                                        |  
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| `@Inject` | Indica que una dependencia debe ser inyectada automáticamente por el CDI.                                                          |
| `@Named`  | Calificador utilizado junto con @Inject para especificar cuál bean debe ser inyectado cuando hay múltiples candidatos disponibles. |

```java
@Singleton
public class CreditCardService {

  @Inject
  private PaymentProcessor paymentProcessor;
  
  public void pay(CreditCard card, double amount) {
    paymentProcessor.process(card, amount);
  }
}
```