# CONDICIONALES (IF ELSE)

[← Regresar a notas](../../README.md) <br>

---

> #### Condición
> Es una expresión que se evalúa como verdadera (`true`) o falsa (`false`). 
> Las condiciones son fundamentales para tomar decisiones dentro del código, permitiendo que el programa realice diferentes acciones según ciertos criterios.

La estructura condicional `if-else` es útil cuando se quiere tomar decisiones según una condición específica.

## Ejemplos

> El bloque `if` ejecuta un conjunto de instrucciones solo si una condición es verdadera.
> ```java
> if (age >= 18) {
>   System.out.println("El usuario es mayor de edad.");
> }
> ```
> 
> El bloque `if-else` ejecuta un bloque si la condición es verdadera, y otro si es falsa.
> ```java
> if (age >= 18) {
>   System.out.println("El usuario es mayor de edad.");
> } else {
>   System.out.println("El usuario es menor de edad.");
> }
> ```
> 
> Cuando la lógica es simple, puedes usar un `if` en una sola línea, sin llaves.
> ```java
> if (age >= 18) 
>   System.out.println("El usuario es mayor de edad.");
> ```
> 
> El operador ternario permite una forma más concisa de escribir una expresión `if-else`.
> ```java
> String message = (age >= 18) 
>   ? "El usuario es mayor de edad." 
>   : "El usuario es menor de edad.";
> System.out.println(message);
> ```

## Anidamiento excesivo de `if-else`
El anidamiento de `if-else` puede hacer que el código sea difícil de leer y mantener.

> Mala práctica:
> ```java
> String vipCategory;
> if (accountBalance > 100000) {
>   vipCategory = "PLATINUM";
> } else if (accountBalance > 50000) {
>   vipCategory = "GOLD";
> } else if (accountBalance > 10000) {
>   vipCategory = "SILVER";
> } else {
>   throw new IllegalArgumentException("El cliente no tiene una categoría VIP");
> }
> ```
> 
> Mejor práctica:
> ```java
> String vipCategory;
> if (accountBalance > 100000) {
>   vipCategory = "PLATINUM";
> }
> 
> if (accountBalance > 50000 && accountBalance <= 100000) {
>   vipCategory = "GOLD";
> }
> 
> if (accountBalance > 10000 && accountBalance <= 50000) {
>   vipCategory = "SILVER";
> }
> 
> if (accountBalance <= 10000) {
>   throw new IllegalArgumentException("El cliente no tiene una categoría VIP");
> }
> ```

## Negación de condiciones
Negar condiciones en lugar de usar `else` puede hacer que el código sea más directo y fácil de entender.

> ```java
> if (!isValid) {
>   throw new IllegalArgumentException("El dato ingresado no es válido");
> }
> 
> // Continuar con el flujo normal si la condición es válida
> ```
