# EXCEPCIONES

[← Regresar a notas](../../README.md) <br>

---

> #### Happy path
> Se refiere al escenario ideal en el que un programa o sistema funciona como se espera, sin errores.

> #### Unhappy path (casos alternos)
> Se refiere a los escenarios en los que ocurren errores en un programa .

> #### Excepción
> Evento que ocurre durante la ejecución de un programa y que interrumpe su flujo normal.
> Las excepciones permiten controlar errores y tomar decisiones sobre cómo reaccionar ante condiciones inesperadas, mejorando así la robustez y la experiencia del usuario.

```java
    if(id == null)
      throw new IllegalArgumentException("Id must not be null");
```

```java
    if(age < 18)
      throw new IllegalArgumentException("The user is not of legal age");
```