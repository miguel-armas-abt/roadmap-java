# PALABRA RESERVADA STATIC

[← Regresar a notas](../../README.md) <br>

---

> - La palabra reservada `static` se utiliza para definir miembros que le pertenecen a la clase y no a las instancias de la clase.
> - Permite acceder a los miembros sin necesidad de instanciar objetos.
> - Mejora el uso de recursos, ya que los miembros estáticos se cargan en memoria una sola vez.

> #### Variable estática
> Se utiliza principalmente para almacenar un dato común entre todas las instancias.
> 
> ```java
>   public class Accumulator {
>     public static int count = 0; // Variable estática
> 
>     public Accumulator() {
>       count++;
>     }
>   }
> ```

> #### Método estático
> - Los método estáticos solo pueden acceder a miembros estáticos de la clase.
> - Se utiliza comúnmente para utilidades o funciones que no dependen del estado de un objeto.
> 
> ```java
>   public class MathUtils {
> 
>     public static double average(double[] numbers) {
>       double sum = 0;
>       for (double num : numbers) {
>         sum += num;
>       }
>       return average(sum, numbers.length);
>     }
> 
>     public static double average(double sum, double length) {
>       return sum / length;
>     }
>   }
> ```

> #### Bloque estático
> - Un bloque estático se ejecuta cuando la clase es cargada por primera vez.
> - Se utiliza para inicializar datos estáticos o ejecutar código de configuración relacionado con la clase.
> 
> ```java
> public class Configuration {
>   public static String config;
> 
>   static {
>     config = "initialized";
>   }
> }
> ```