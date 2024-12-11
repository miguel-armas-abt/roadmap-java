# ESTRUCTURAS DE DATOS

[← Regresar a notas](../../README.md) <br>

---

[1. Arreglos (arrays)](#1-arreglos-arrays) <br>
[2. Colecciones](#2-colecciones) <br>
[2.1. Listas](#21-listas) <br>
[2.2. Sets](#22-sets) <br>
[3. Mapas](#3-mapas) <br>

---

## 1. Arreglos (arrays)
> - Estructura de datos que permite almacenar múltiples elementos. 
> - No puede cambiar su tamaño una vez que ha sido definido (<u>tamaño fijo</u>).
> - Puede almacenar datos primitivos y objetos.
> - No proporciona métodos.
> 
> **Ej.** Declarar un arreglo y asignarle un valor a sus índices
> ```java
> String[] names = new String[5];   // declarar un arreglo de cadenas con 5 elementos
> names[0] = "Jhon";                // asignar valor al primer elemento
> names[1] = "Will";                // asignar valor al segundo elemento
> ```
>
> **Ej.** Recorrer un arreglo
> ```java
> for(String i: names) {
>   System.out.println(i);
> }
> ```

---

## 2. Colecciones
> - Estructura de datos que permite almacenar múltiples elementos.
> - Puede cambiar su tamaño según se añadan o eliminen elementos. (<u>tamaño dinámico</u>).
> - Solo puede almacenar objetos.
> - Proporciona métodos útiles como `add(), remove(), get(), size()`, etc.
> - Los tipos de colecciones más populares son las <u>listas</u> y los <u>sets</u>.
> 
> ![Collections](../resources/images/08-data-sctructures/arrays.jpg)

### 2.1. Listas
> - Se implementan a partir de la interface `java.util.List`.
> - Permite elementos duplicados.
> - Sus elementos son agregados y ordenados por la posición del índice.
> - Las implementaciones más comunes son `ArrayList`, `Vector` y `LinkedList`.
> 
> > #### `ArrayList`
> > Almacena y accede a elementos consecutivos.
> 
> > #### `Vector`
> > Tiene las mismas características de ArrayList, pero añade seguridad de hilo, lo cual generalmente genera impacto en el rendimiento.
>
> > #### `LinkedList`
> > Es una implementación de lista doblemente enlazada, con lo cual es mejor para insertar y eliminar elementos.
>
> ---
> 
> **Ej.** Declarar un ArrayList y añadir elementos
> ```java
> List<String> names = new ArrayList<>();  // declarar una lista
> names.add("Jhon");                       // añadir un elemento
> names.add("Will");                       // añadir otro elemento
> names.remove(0);                         // remover el elemento de la pisición 0
> ```
>
> **Ej.** Recorrer una lista
> ```java
> for(String i: names) {
>   System.out.println(i);
> }
> ```
> **Ej.** Convertir array en lista
> ```java
> String[] namesArray = {"Mark", "Elon", "Linus"};
> List<String> namesList = new ArrayList<>(Arrays.asList(namesArray));
> ```

---

### 2.2. Sets
> - Se implementan a partir de la interface `java.util.Set`.
> - <u>No permite</u> elementos duplicados.
> - Si es que se intenta añadir un elemento duplicado, retorna `false`.
> - Las implementaciones más comunes son `HashSet`, `TreeSet` y `LinkedHashSet`.
>
> > #### `HashSet`
> > - Almacena los elementos en <u>desorden</u>.
> > - Permite agregar elementos nulos.
>
> > #### `TreeSet`
> > - Almacena los elementos en <u>orden</u>.
> > - <u>No permite</u> agregar elementos nulos.
> > - Tiene impacto en el rendimiento.
>
> > #### `LinkedHashSet`
> > - Almacena los elementos en <u>orden</u>.
> > - Es una implementación de lista doblemente enlazada.

---

## 3. Mapas
> - Estructuras de datos que permiten almacenar pares de clave-valor. 
> - Cada clave en el mapa es única.
> - Se implementan a partir de la interface `java.util.Map`.
> - Las implementaciones más comunes son `HashMap`, `HashTable`, `TreeMap` y `LinkedHashMap`.
>
> ![Maps](../resources/images/08-data-sctructures/maps.png)
>
> > #### HashMap
> > - Almacena los elementos en <u>desorden</u>.
> > - Permite una clave nula.
> > - Permite valores nulos.
>
> > #### HashTable
> > - Almacena los elementos en <u>desorden</u>.
> > - <u>No permite</u> clave ni valores nulos.
> > - Tiene seguridad de hilo (impacto en el rendimiento).
>
> > #### TreeMap
> > - Almacena los elementos en <u>orden ascendente</u> en función de la clave.
>
> **Ej.** Declarar un HashMap y añadir elementos
> ```java
> Map<Integer, String> usersDniMap = new HashMap<>();  // declarar un HashMap
> usersDniMap.put(76517360, "Mark Zuckerberg");        // añadir un par clave-valor
> ```
> 
> **Ej.** Acceder a un valor por su clave
> ```java
> String name = usersDniMap.get(76517360);              // obtener el valor asociado con la clave 76517360
> System.out.println("El dueño del DNI es: " + name);   // imprimir el nombre asociado al DNI
> ```
>
> **Ej.** Recorrer los elementos del mapa
> ```java
> for (Map.Entry<Integer, String> entry : usersDniMap.entrySet()) {
>   System.out.println("clave:" + entry.getKey() + ", valor: " + entry.getValue());
> }
> ```
> 
> **Ej.** Verificar si existe una clave en el mapa
> ```java
> boolean containsDni = usersDniMap.containsKey(76517360);
> if (!containsDni) {
>   throw new IllegalArgumentException("El DNI provisto no está en el mapa");
> }
> ```
