# TRATAMIENTO DE CADENAS

[← Regresar a notas](../../README.md) <br>

---

> ### Cadena
> Una cadena es una secuencia de caracteres utilizada para representar texto. 
> En Java, las cadenas son objetos de la clase String y proporcionan múltiples métodos para manipular y tratar texto.

## Métodos comunes para el tratamiento de cadenas

> ### Trim
> Se utiliza para eliminar los espacios en blanco al inicio y al final de una cadena.
> 
> ```java
> String message = "   Hello, world!   ";
> String trimmedMessage = message.trim();
> System.out.println(trimmedMessage); // "Hello, world!"
> ```

> ### ToLowerCase
> Convierte todos los caracteres de una cadena a minúsculas. Su contraparte es el `toUpperCase`.
>
> ```java
> String message = "Hello, world!";
> String lowerCaseMessage = message.toLowerCase();
> System.out.println(lowerCaseMessage); // "hello, world!"
> ```

> ### Repeat
> Devuelve una nueva cadena que consiste en la concatenación de la cadena original repetida un número específico de veces.
>
> ```java
> String message = "Hello!";
> String repeatedMessage = message.repeat(3);
> System.out.println(repeatedMessage); // "hello! hello! hello!"
> ```

> ### CharAt
> Devuelve el carácter en la posición especificada de la cadena.
>
> ```java
> String message = "Hello!";
> String firstCharacter = message.charAt(0);
> System.out.println(firstCharacter); // 'H'
> ```

> ### Contains
> Verifica si la cadena contiene la secuencia de caracteres especificada.
>
> ```java
> String message = "Hello, world!";
> boolean containsHello = message.contains("Hello");
> System.out.println(containsHello); // true
> ```

> ### Substring
> Devuelve una nueva cadena que es una subcadena de la cadena original, desde el índice inicial hasta el índice final.
>
> ```java
> String message = "Hello, world!";
> String substringMessage = message.substring(0, 5);
> System.out.println(substringMessage); // "Hello"
> ```

> ### Length
> Devuelve la longitud de la cadena, es decir, el número de caracteres que contiene.
>
> ```java
> String message = "Hello";
> int lengthMessage = message.length();
> System.out.println(substringMessage); // 5
> ```

> ### Matches
> Comprueba si una cadena coincide con una expresión regular específica.
>
> ```java
> String phone = "123-456-7890";
> boolean isValidPhone = phone.matches("\\d{3}-\\d{3}-\\d{4}");
> System.out.println(isValidPhone); true
> ```