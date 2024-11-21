# EXCEPCIONES

[← Regresar a notas](../../README.md) <br>

---

## 1. Conceptos clave

> #### Excepciones
> - Son subclases de `java.lang.Exception`. 
> - Se utilizan para <u>reaccionar</u> ante condiciones inesperadas de manera controlada.

> #### Error
> Problema grave que no puede ser controlado en tiempo de ejecución. Por ejemplo, fallo de memoria.

## 2. Tipos de excepciones

> ### checked exception
> - Se verifican en <u>tiempo de compilación</u>.
> - El compilador `javac` obliga a declararlas con `throws` o manejarlas con un bloque `try-catch`. 
> - **Ej.** `IOException`, `SQLException`
> 
> ```java
>   try {
> 
>     File file = new File("data.txt");
>     FileReader fr = new FileReader(file); // Checked exception
> 
>   } catch(IOException exception) {
>     e.printStackTrace();
>   }
> ```

> ### unchecked exception
> - Ocurren en <u>tiempo de ejecución</u>.
> - No es necesario declararlas, ni manejarlas explícitamente.
> - **Ej.** `NullPointerException`, `ArithmeticException`
> 
> ```java
>   int result = 10 / 0; // Unchecked exception: ArithmeticException
> ```

<img src="../resources/images/exceptions/exceptions.png" width="700" height="280">

## 3. Stack trace
> - La pila de errores permite rastrear el origen de un error en el programa.
> - Ofrece trazabilidad de los métodos que fueron llamados antes de que ocurriera la excepción.
> <br> <br>
>  <img src="../resources/images/exceptions/stack-trace.gif" width="600" height="450">

## 4. Excepciones personalizadas
> - Se pueden crear excepciones personalizadas extendiendo la clase `RuntimeException`.
> - Son útiles para representar condiciones inesperadas específicas de la aplicación.
> 
> ```java
> public class BusinessException extends RuntimeException {
>   public BusinessException(String message) {
>     super(message);
>   }
> }
> ```
>
> ```java
> if(id == null)
>   throw new BusinessException("Id must not be null");
> ```
>
> ```java
> if(age < 18)
>   throw new BusinessException("The user is not of legal age");
> ```
>
> ```java
> if (amount > balance)
>   throw new BusinessException("Insufficient balance for withdrawal.");
> ```