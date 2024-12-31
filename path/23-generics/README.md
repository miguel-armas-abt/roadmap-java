# Genéricos en Java

[← Regresar a notas](../../README.md) <br>

---

## 1. Conceptos clave

> #### Genéricos
> Los genéricos en Java permiten escribir clases, interfaces y métodos que funcionan con diferentes tipos de datos, definidos de manera flexible, es decir, sin especificar el tipo exacto hasta el momento de su uso.

> #### Parámetros de tipo
> Representan un tipo genérico y se definen con el operador diamante `<T>` en el nombre de la clase, interfaz o método.
>
> ```java
> public class Box<T> {
>     private T content;
>     public void setContent(T content) { this.content = content; }
>     public T getContent() { return content; }
> }
> ```

---

## 2. Aplicaciones comunes

> #### Clases genéricas
> ```java
> public class Stack<T> {
>     private List<T> elements = new ArrayList<>();
>     public void push(T element) { elements.add(element); }
>     public T pop() { return elements.remove(elements.size() - 1); }
> }
> ```

> #### Métodos genéricos
> ```java
> public static <T> void printArray(T[] array) {
>     for (T element : array)
>         System.out.println(element);
> }
> ```

> #### Interfaces genéricas
> ```java
> public interface Repository<T, ID> {
>   void save(T entity);
>   T findById(ID id);
>   List<T> findAll();
>   void deleteById(ID id);
> }
> ```

---

## 3. Restricciones de tipos

> #### Bounded types
> Acotan los tipos permitidos mediante el uso de la palabra clave `extends`.
> ```java
> public class Calculator<T extends Number> {
>   public double sum(List<T> numbers) {
>     double total = 0.0;
>     for (T number : numbers)
>       total += number.doubleValue();  // Convertimos a double para manejar diferentes tipos numéricos
>     return total;
>   }
> }
> ```

> #### Wildcards (`?`)
> Representan un tipo desconocido:
> - `? extends T`: Permite cualquier tipo que sea una subclase de `T`.
> - `? super T`: Permite cualquier tipo que sea una superclase de `T`.
> - `?`: Permite cualquier tipo.
> ```java
> public void process(List<? extends Number> numbers) {
>     numbers.forEach(System.out::println);
> }
> ```

---

📌 Evita el uso excesivo de genéricos que complique la legibilidad.