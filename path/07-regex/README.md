# REGEX

[← Regresar a notas](../../../../../../../../README.md) <br>

---

https://regexr.com/

> - Una expresión regular (REGEX) es una secuencia de caracteres que forma un patrón de búsqueda.
> - Con ayuda de las REGEX podemos verificar si una cadena de texto cumple con un patrón específico.

| Operador           | Descripción                                                                                | 
|--------------------|--------------------------------------------------------------------------------------------|
| `{} () []`         | Operadores de agrupación                                                                   |
| `.`                | Cualquier carácter excepto nueva línea \n                                                  |
| `[abc]`            | Carácter `a`, `b` o `c`                                                                    |
| `[a-z]`            | Desde a hasta z                                                                            |
| `?`                | Cero o uno del elemento precedente                                                         |
| `*`                | Cero o más del elemento precedente                                                         |
| `+`                | Uno o más del elemento precedente                                                          |
| `aa \| bb`         | Cualquiera aa o bb                                                                         |
| `{m,n}`            | Entre m y n del elemento precedente                                                        |
| `\.`               | Escapar un símbolo (por ejemplo \*, \(, \\, etc)                                           |
| `^`                | El inicio de la cadena                                                                     |
| `$`                | El final de la cadena                                                                      |
| `\d, \w, \s`       | Un dígito, carácter `[A-Za-z0-9]`, o espacio                                               |
| `\D, \W, \S`       | Cualquiera excepto un dígito, carácter o espacio                                           |
| `[^abc]`           | Cualquier carácter excepto `a`, `b` o `c`                                                  |
| `{n}`              | Exactamente más del elemento precedente                                                    |
| `{n,}`             | n o más del elemento precedente                                                            |
| `??, *?, +?, {n}?` | Igual que lo anterior, pero tan poco como sea posible                                      |
| `(expr)`           | Captura lo uqe está en paréntesis como un grupo para su posterior uso con `\1`, `\2`, etc. |
| `(?:expr)`         | Agrupa una expresión sin que se capture                                                    |
| `(?=expr)`         | Seguido por la expresión                                                                   |
| `(?!expr)`         | No seguido por la expresión                                                                |

### 🔍 Ejemplos

| Descripción                                 | Ejemplo                                       | REGEX                                                 |
|---------------------------------------------|-----------------------------------------------|-------------------------------------------------------|
| Número de teléfono celular                  | `938817321`                                   | `^9\d{8}$`                                            |
| Número de documento de identidad (DNI Perú) | `76527360`                                    | `^\d{8}$`                                             |
| Solo letras                                 | `HolaMundo`                                   | `^[a-zA-Z]+$`                                         |
| Solo dígitos                                | `123456`                                      | `^\d+$`                                               |
| Dirección de correo electrónico             | `email.user@email.com`, `email_user@email.es` | `^[\w\.-]+@[a-zA-Z\d\.-]+\.[a-zA-Z]{2,6}$`            |
| Fecha en formato día/mes/año                | `14/02/2024`                                  | `^(0[1-9]\|[12][0-9]\|3[01])/(0[1-9]\|1[0-2])/\d{4}$` |