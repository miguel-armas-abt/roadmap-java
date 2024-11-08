# BUCLES (FOREACH, FOR, WHILE)

[← Regresar a notas](../../README.md) <br>

---

> Los bucles permiten iterar un bloque de código varias veces según sea una condición o colección de elementos.

## Foreach
El bucles `foreach` se utiliza para recorrer los elementos de una colección o arreglo.

> Recorrer una lista
>```java
> List<String> nameList = Arrays.asList("Fabian", "Omar", "Jhunior");
> for (String name : nameList) {
>   System.out.println(name);
> }
>```
>
> Recorrer un arreglo
>```java
> int[] numberArray = {1, 2, 3, 4, 5};
> for (String number : numberArray) {
>   System.out.println(number);
> }

## For
El bucle `for` es útil cuando se necesita controlar el número de iteraciones.

> - **Variable contadora**: `i` se inicializa en `0`
> - **Condición de parada**: El bucle se ejecutará siempre y cuando el valor de `i` sea menor que `n`
> - **Incremento**: En cada iteración `i` aumentará su valor en uno gracias a `i++`
>```java
> int n = 5;
> for (int i = 0; i < n; i++) {
>   System.out.println("Iteración número " + i);
> }
>```

## While
El bucle `while` se ejecuta mientras una condición sea verdadera.

>```java
> Scanner = new Scanner(System.in);
> boolen isValid = true;
>
> while (isValid) {
>   System.out.print("¿Desea continuar en el bucle?: (true/false)");
>   isValid = scanner.nextBoolean();
> }
>```
>
> Un bucle infinito ocurre cuando la condición de un while nunca se vuelve falsa, causando que el bucle se ejecute indefinidamente.
>```java
> while (true) {
>   System.out.println("Este bucle se ejecutará por siempre");
> }
>```
>
> - Un menú es una lista de opciones que se presenta al usuario para que elija entre diferentes acciones. 
> - Con `while` podemos presentarle al usuario el menú repetidamente hasta que decida salir. 
>```java
> Scanner scanner = new Scanner(System.in);
> int option = 0;
> while (option != 3) {
>   System.out.println("1. Opción 1");
>   System.out.println("2. Opción 2");
>   System.out.println("3. Salir");
>   option = scanner.nextInt();
>
>   if (option == 1) {
>     System.out.println("Seleccionaste Opción 1");
>   }
>
>   if (option == 2) {
>     System.out.println("Seleccionaste Opción 2");
>   }
>
>   if (option == 3) {
>     System.out.println("Saliendo...");
>   }
>
>   if (option != 1 && option != 2 && option != 3) {
>     System.out.println("Opción inválida");
>   }
> }
>```

