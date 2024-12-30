# JAVA 8

[← Regresar a notas](../../README.md) <br>

---

## 1. Conceptos clave

> #### Programación funcional
> Paradigma de programación donde las funciones pueden ser asignadas como variables, pasadas como parámetros o devueltas como resultados.

> #### Expresiones Lambda
> Es una forma compacta de escribir <u>funciones anónimas</u> (es decir, funciones sin nombre).
> 
> ```java
> (parámetros) -> {cuerpo}
> ```

> #### Método de referencia
> - Forma concisa de referenciar un método ya existente en lugar de usar una expresión lambda.
> - El compilador de Java sugiere su uso.
> ```java
> Clase::método
> ```

## 2. Stream API
> - Herramienta para procesar una secuencia de datos de manera funcional a partir de una colección.
> - Ofrece operadores para manipular la secuencia de datos.
>   - `filter`: Filtrar elementos.
>   - `map`: Transformar elementos.
>   - `forEach`: Iterar sobre los elementos.
>   - `collect`: Recolectar elementos en una colección.
> 
> ```java
> List<String> names = Arrays.asList("Elon Musk", "Mark Zuckerberg", "Linus Torvalds", "");
> List<Employee> employees = names.stream()
>     .filter(name -> !name.isEmpty())
>     .map(name -> name.toUpperCase())
>     .map(name -> new Employee(name))
>     .collect(Collectors.toList());
> ```

## 3. Optional
> - Herramienta para procesar un valor que podría estar presente o no, evitando `NullPointerException`.
> - Ofrece operadores para manipular el valor.
>   - `filter`: Filtrar el elemento.
>   - `map`: Transformar el elemento.
>   - `isPresent`: Verifica si hay un valor.
>   - `ifPresent`: Ejecuta una acción si hay un valor.
>   - `orElse`: Si no hay ningún valor, entonces proporciona un valor por defecto .
>   - `orElseThrow`: Si no hay ningún valor, entonces lanza una excepción.
>   - `get`: Recuperar el valor contenido dentro del Optional. Debe utilizarse con precaución y solo cuando está seguro que el valor está presente. ⚠️
>
> ```java
> String phoneNumber = Optional.ofNullable(phone)
>     .filter(number -> number.matches("^9\\d{8}$"))
>     .map(number -> "+51" + number)
>     .orElseThrow(() -> new RuntimeException("Invalid phone"));
> ```

## 4. Interfaces funcionales
> - Una interfaz funcional tiene exactamente un método abstracto.
> - Es la base para trabajar con expresiones lambda y programación funcional en Java.

| Tipo de función    | Método abstracto   | Tipo de retorno | ¿Cuándo usar?                                                                     |
|--------------------|--------------------|-----------------|-----------------------------------------------------------------------------------|
| `Predicate<T>`     | `test(T t)`        | `boolean`       | Condicionales.                                                                    |
| `Function<T,R>`    | `apply(T t)`       | `R`             | Operaciones que reciben un parámetro `T` y devuelven un resultado `R`.            |
| `UnaryOperator<T>` | `apply(T t)`       | `T`             | Operaciones que reciben un parámetro `T` y devuelven un resultado del mismo tipo. |
| `Consumer<T>`      | `accept(T t)`      | `void`          | Operaciones que reciben un parámetro `T`, pero "no" devuelven ningún resultado.   |
| `Supplier<T>`      | `get()`            | `R`             | Operaciones que "no" reciben ningún parámetro y pero devuelven un resultado `T`.  |

```java
//Validate phone
Predicate<String> phoneFormatValidator = phone -> phone.matches("^9\\d{8}$");
boolean isValidPhone = phoneFormatValidator.test("987654321");

//Split string
Function<String,String[]> stringSplitter = string -> string.split(",");
String[] names = stringSplitter.apply("Elon,Mark,Linus");

//Generate a random number
Supplier<Integer> randomNumberGenerator = () -> random.nextInt(100);
int random = randomNumberGenerator.get();
```

Interfaces funcionales que necesitan dos parámetros de entrada:

| Tipo de función     | Método abstracto   | Tipo de retorno | ¿Cuándo usar?                                                      |
|---------------------|--------------------|-----------------|--------------------------------------------------------------------|
| `BiPredicate<T,U>`  | `test(T t, U u)`   | `boolean`       | Útil cuando el `Predicate` necesita dos parámetros de entrada.     |
| `BiFunction<T,U,R>` | `apply(T t, U u)`  | `R`             | Útil cuando el `Function` necesita dos parámetros de entrada.      |
| `BinaryOperator<T>` | `apply(T t, T t)`  | `T`             | Útil cuando el `UnaryOperator` necesita dos parámetros de entrada. |
| `BiConsumer<T, U>`  | `accept(T t, U u)` | `void`          | Útil cuando el `Consumer` necesita dos parámetros de entrada.      |

Java ofrece la posibilidad de crear nuestras propias interfaces funcionales con `@FunctionalInterface`

```java
@FunctionalInterface
interface StringProcessor {
    String process(String str1, String str2);
}

public class Application {
  public static void main(String[] args) {
    StringProcessor processor = (str1, str2) -> (str1 + str2).toUpperCase();
    String result = processor.process("Hello", " world");
  }
}
```