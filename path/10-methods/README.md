# MÉTODOS (FUNCIONES Y PROCEDIMIENTOS)

[← Regresar a notas](../../README.md) <br>

---

> - Los métodos son bloques de código que realizan una tarea específica y pueden ser llamados desde otras partes del programa.
> - Los métodos se utilizan para organizar y reutilizar código, facilitando el mantenimiento y mejorando la legibilidad.

![Methods](../resources/images/methods/method.jpg)

| Elemento                  | Descripción                                                                                                                                  |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| **Parámetros de entrada** | Son los valores que se pasan al método para que realice su tarea, y pueden usarse dentro del cuerpo del método.                              |
| **Tipo de retorno**       | Es el tipo de dato que devuelve el método después de completar su tarea. Si un método no devuelve ningún valor, su tipo de retorno es `void` |
| **Nombre del método**     | El nombre del método debe ser descriptivo y representar claramente lo que hace el método, facilitando su comprensión de uso.                 |

> Ejemplo de una función
>```java
> public double calculateInterest(double balance, double interestRate) {
>   double interest = balance * interestRate;
>   return interest;
> }
>```
>
> Ejemplo de un procedimiento
>```java
> public void printMessage(String name) {
>   System.out.println("Hello " + name);
> }
>```

## Principio DRY
El principio DRY (Don't Repeat Yourself) sugiere evitar la duplicación de código mediante la creación de métodos reutilizables.

> > Imagina un sistema bancario que ofrece dos productos diferentes: cuentas de ahorro y cuentas de inversión.
> > Ambos productos requieren cálculos de intereses, pero con diferentes tasas de interés.
> 
> El siguiente código repite la lógica de cálculo de interés, lo cual lo hace difícil de mantener.
> 
> ```java
> public static void main(String[] args) {
>   Scanner scanner = new Scanner(System.in);
>   System.out.println("Ingrese el saldo de la cuenta de ahorros: ");
>   double savingsBalance = scanner.nextDouble();
> 
>   System.out.println("Ingrese el saldo de la cuenta de inversión: ");
>   double investmentBalance = scanner.nextDouble();
> 
>   //calculo del interés para la cuenta de ahorro
>   double savingsInterest = savingsBalance * 0.03;
>   savingsBalance += savingsInterest;
>   System.out.println("Saldo actualizado: " + savingsBalance);
> 
>   //calculo del interés para la cuenta de inversión
>   double investmentInterest = investmentBalance * 0.07;
>   investmentBalance += investmentInterest;
>   System.out.println("Saldo actualizado: " + investmentBalance);
> }
> ```
> 
> El siguiente código elimina la duplicación de código mediante la reutilización de un método.
> 
> ```java
> public static void main(String[] args) {
>   double savingsBalance = requestBalance("ahorros");
>   double updatedSavingsBalance = calculateUpdatedBalance(savingsBalance, 0.03);
>   printMessage(updatedSavingsBalance);
> 
>   double investmentBalance = requestBalance("inversión");
>   double updatedInvestmentBalance = calculateUpdatedBalance(savingsBalance, 0.07);
>   printMessage(updatedInvestmentBalance);
> }
> 
> public static double requestBalance(String accountType) {
>   Scanner scanner = new Scanner(System.in);
>   System.out.println("Ingrese el saldo de la cuenta de " + accountType + ": ");
>   return scanner.nextDouble();
> }
> 
> public static doube calculateUpdatedBalance(double balance, double interestRate) {
>   double interest = balance * interestRate;
>   balance += interest;
>   return balance;
> }
> 
> public static void printMessage(double updatedBalance) {
>   System.out.println("Saldo actualizado " + updatedBalance);
> }
> ```