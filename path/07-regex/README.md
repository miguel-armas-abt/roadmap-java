# REGEX

[← Regresar a notas](../../../../../../../../README.md) <br>

---

https://regexr.com/

> - Una expresión regular (REGEX) es una secuencia de caracteres que forma un patrón de búsqueda.
> - Con ayuda de las REGEX podemos verificar si una cadena de texto cumple con un patrón específico.

| Operador           | Descripción                                                                                       | 
|--------------------|---------------------------------------------------------------------------------------------------|
| `{} () []`         | Operadores de agrupación.                                                                         |
| `^`                | El inicio de la cadena.                                                                           |
| `$`                | El final de la cadena.                                                                            |
| `[abc]`            | Carácter `a`, `b` o `c`.                                                                          |
| `[a-z]`            | Desde a hasta z.                                                                                  |
| `?`                | Cero o una vez del elemento previo.                                                               |
| `*`                | Cero o más veces del elemento previo.                                                             |
| `+`                | Uno o más veces del elemento previo.                                                              |
| `{m,n}`            | Entre m y n veces del elemento previo.                                                            |
| `{n}`              | Exactamente n veces del elemento previo.                                                          |
| `{n,}`             | n o más veces del elemento previo.                                                                |
| `.`                | Cualquier carácter excepto nueva línea \n.                                                        |
| `aa \| bb`         | Cualquiera entre `aa` o `bb`.                                                                     |
| `\D, \W, \S`       | Cualquiera excepto un dígito, carácter o espacio.                                                 |
| `[^abc]`           | Cualquier carácter excepto `a`, `b` o `c`.                                                        |
| `\.`               | Escapar un símbolo. Por ejemplo, punto `\.`, asterisco `\*`, slash `\\`, etc.                     |
| `\d, \w, \s`       | Un dígito, carácter `[A-Za-z0-9]`, o espacio.                                                     |
| `??, *?, +?, {n}?` | Igual que lo anterior, pero tan poco como sea posible.                                            |
| `(expr)`           | Captura lo que está en paréntesis como un grupo para su posterior referencia con `\1`, `\2`, etc. |
| `(?:expr)`         | Agrupa una expresión sin que se capture.                                                          |
| `(?=expr)`         | Seguido por la expresión.                                                                         |
| `(?!expr)`         | No seguido por la expresión.                                                                      |

## Ejemplos


> > **Validar que una cadena solo contenga dígitos** `^\d+$`
> - `Inicio` de cadena.
> - `Una o más` dígitos.
> - `Fin` de cadena.
>
> ```java
> if(!string.matches("^\\d+$"))
>   throw new IllegalArgumentException("The string doesn't contain only digits");
> ```

---

> > **Validar que una cadena solo contenga letras** `^[a-zA-Z]+$`
> - `Inicio` de cadena.
> - `Una o más` letras entre la a y la z, sin distinción entre mayúsculas o minúsculas.
> - `Fin` de cadena.
>
> ```java
> if(!string.matches("^[a-zA-Z]+$"))
>   throw new IllegalArgumentException("The string doesn't contain only letters");
> ```

---

> > **Validar un número de celular** `^9\d{8}$`
> - `Inicio` de cadena
> - El primer caracter es el número 9.
> - Seguido de exactamente ocho `dígitos`
> - `Fin` de cadena.
> 
> ```java
> if(!cellphoneNumber.matches("^9\\d{8}$"))
>   throw new IllegalArgumentException("Invalid phone format");
> ```

---

> > **Validar una dirección de correo electrónico** `^[\w\.-]+@[a-zA-Z\.]+\.[a-zA-Z]{2,3}$`
> - `Inicio` de cadena
> - `Uno o más` caracterers `o` puntos `o` guiones.
> - Seguido de exactamente un @
> - Seguido de `una o más` letras entre la a y la z `o` puntos
> - Seguido de exactamente un punto
> - Seguido de entre 2 a 3 letras entre la a y la z.
> - `Fin` de cadena.
>
> ```java
> if(!email.matches("^[\\w\\.-]+@[a-zA-Z\\.]+\\.[a-zA-Z]{2,3}$"))
>   throw new IllegalArgumentException("Invalid email format");
> ```

---

> > **Validar una fecha con el formato día / mes / año** `^(0[1-9]|[12][0-9]|3[01])/(0[1-9]|1[0-2])/\d{4}$`
> - `Inicio` de cadena
> - Seguido de uno de los siguientes casos:
>   - Número 0 seguido de un dígito del 1 al 9 `o`
>   - Número 1 o 2 seguido de un dígito del 0 al 9 `o`
>   - Número 3 seguido del número 0 o 1.
> - Seguido de exactamente un /
> - Seguido de uno de los siguientes casos:
>   - Número 0 seguido de un dígito del 1 al 9 `o`
>   - Número 1 seguido del número 1 o 2.
> - Seguido de exactamente un /
> - Seguido de cuatro `dígitos`.
> - `Fin` de cadena.
>
> ```java
> if(!date.matches("^(0[1-9]\|[12][0-9]\|3[01])/(0[1-9]\|1[0-2])/\d{4}$"))
>   throw new IllegalArgumentException("Invalid date format");
> ```

---
