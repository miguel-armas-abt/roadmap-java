# EXCEPCIONES

[← Regresar a notas](../../README.md) <br>

---

## Conceptos clave

> #### Excepciones
> Son subclases de `java.lang.Exception`, utilizadas para <u>reaccionar</u> ante condiciones inesperadas de manera controlada.

> #### Error
> Problema grave que no puede ser controlado en tiempo de ejecución. Por ejemplo, desbordamiento de la memoria.

---

## Tipos de excepciones

### 1. Checked exception
> Se verifican en **<u>tiempo de compilación</u>**, ya que el `javac` obliga a declararlas con `throws` o controlarlas con `try-catch`. 
> Por ejemplo, `IOException`, `SQLException`, etc.
> 
> ```java
> /**
>   * Este método utiliza "throws" para declarar que no manejará la "checked exception",
>   * delegando la responsabilidad al método que lo invoque.
>   */
>   private static void readFile(String fileName) throws FileNotFoundException {
>     File file = new File(fileName);
>     FileReader fileReader = new FileReader(file);
>   }
> ```
>
> ```java
>  /**
>   * Este método utiliza "try" para envolver el código que puede producir una "checked exception",
>   * y usa "catch" para controlarla y transformarla en una "unchecked exception".
>   */
>  private static void readFile(String fileName) {
>    try {
>
>      File file = new File(fileName);
>      FileReader fileReader = new FileReader(file);
>
>    } catch (FileNotFoundException exception) {
>      throw new RuntimeException("File " + fileName + " not found", exception);
>    }
>  }
> ```

### 2. Unchecked exception
> Ocurren en **<u>tiempo de ejecución</u>** y no es necesario manejarlas explícitamente.
> Por ejemplo, `NullPointerException`, `ArithmeticException`, etc.
> 
> ```java
>   int result = 10 / 0; // Unchecked exception: ArithmeticException
> ```

<img src="../resources/images/04-exceptions/exceptions.png" width="700" height="280">

## 3. Stack trace
> - La pila de errores permite rastrear el origen de un error en la aplicación.
> - Ofrece trazabilidad de los métodos que fueron llamados antes de que ocurriera la excepción.
> <br>
>
> <img src="../resources/images/04-exceptions/stack-trace.png" width="600" height="200">

## 4. Excepciones personalizadas
> - Se utilizan para distinguir errores del sistema con errores relacionados a la lógica de la aplicación.
> - Se pueden crear extendiendo la clase `RuntimeException` (unchecked exceptions).
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
