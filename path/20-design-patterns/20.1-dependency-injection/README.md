# INYECCIÓN DE DEPENDENCIAS (DI)

[← Regresar a patrones de diseño](../README.md) <br>

> >⚠️ **Problema**:
> >Hacer que los objetos dependan de otros objetos sin tener que instanciarlos por sí mismos.
>
> >✅ **Solución**:
> >Delegar la inyección de las dependencias (objetos que un objeto necesita para funcionar) a otra parte del programa.
>
> 
> ![DI](./../../resources/images/20-design-patterns/dependency-injection.png)

### Ventajas
- **Desacoplamiento**: Los objetos no conocen los detalles de implementación de sus dependencias.
- **Flexibilidad**: Facilita el cambio de implementaciones sin modificar el código dependiente.
- **Reusabilidad**: Las clases pueden ser fácilmente reutilizadas.

---

### DI mediante constructor
- Las dependencias se pasan a través del constructor.
- Se utiliza para las dependencias obligatorias.

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



Es una buena práctica utilizar inyección por constructor por las siguientes razones:
- **Dependencias explícitas**: Los argumentos que requiere el constructor son evidentes.
- **Inmutabilidad**: Los campos de la clase pueden ser marcados como `final`, asegurando que no cambien tras la construcción del objeto.
- **Pruebas unitarias**: Facilita la creación manual de las dependencias (mocks) en las pruebas unitarias.
