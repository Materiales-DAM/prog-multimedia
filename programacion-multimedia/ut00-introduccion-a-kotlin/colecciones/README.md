---
cover: ../../.gitbook/assets/Kotlin-Vs-Java.png
coverY: 86.92240117130308
layout:
  width: default
  cover:
    visible: true
    size: hero
    mask: none
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
  anchors:
    visible: true
---

# Colecciones

Kotlin proporciona tres tipos principales de colecciones: **Listas (List)**, **Mapas (Map)** y **Sets**. Estas colecciones se dividen en **inmutables** (no pueden modificarse después de su creación) y **mutables** (se pueden modificar).

## **Listas y Set**

Una **Lista** es una colección ordenada que permite duplicados. Puede ser inmutable (`List`) o mutable (`MutableList`).

### **Creación de una lista**

```kotlin
val listaInmutable = listOf(1, 2, 3, 4)
val listaMutable = mutableListOf(1, 2, 3, 4)
```

### **Creación de un set**

```kotlin
val setInmutable = setOf(1, 2, 3, 4)
val setMutable = mutableSetOf(1, 2, 3, 4)
```

### Métodos

#### **`map<B>(A -> B): List<B>`**

Se utiliza para **transformar** los elementos de una lista aplicando una función a cada elemento y devolviendo una nueva `List<B>` con los elementos transformados. El número de elementos de la lista resultante es el mismo que en la lista original, ya que simplemente se aplica una transformación a cada uno de ellos.

Toma como parámetro una función lambda `(A) -> B`, donde `A` es el tipo de los valores de la lista original y `B` el de la lista resultante.

```kotlin
val lista = listOf(1, 2, 3, 4)
// En este caso A es Int y B también es Int
val listaMapeada = lista.map { number -> number * 2 } // [2, 4, 6, 8]
```

#### **`filter(A -> Boolean): List<A>`**

Sirve para quitar de una lista aquellos elementos que no cumplan una condición determinada. Toma como parámetro una lambda de tipo `(A) -> Boolean` que expresa la condición de filtrado. Siendo A el tipo de los valores que contiene la lista&#x20;

```kotlin
val listaFiltrada = lista.filter { number -> number % 2 == 0 } // [2, 4]
```

#### **`flatMap(A -> List<B>): List<B>`**

Este método es de utilidad cuando la transformación que se va a aplicar a cada elemento de la List produce una colección de valores.

Por ejemplo, si queremos obtener los tags de todos los productos de una lista

```kotlin
val products = listOf(
    Product(1, "tornillo", listOf("Ferretería", "Tornillo")),
    Product(2, "tuerca", listOf("Ferretería", "Tuerca")),
    Product(3, "lápiz", listOf("Papelería"))
)

val tags: List<List<String>> = products
    .map{p -> p.tags};
    
println(tags);
```

Como podemos observar, si aplicamos el método map lo que obtenemos es un List de List de tags, habrá un List independiente por cada producto en la lista original. Sin embargo, lo que queremos obtener es un List\<String> con los tags de todos los productos.

Para poder hacer esto necesitamos el método `flatMap` que recibe una lambda (A) -> List\<B> .

```kotlin
val products = listOf(
    Product(1, "tornillo", listOf("Ferretería", "Tornillo")),
    Product(2, "tuerca", listOf("Ferretería", "Tuerca")),
    Product(3, "lápiz", listOf("Papelería"))
)

val tags: List<String> = products
    // Aquí la B es String
    .flatMap{p -> p.getTags()}
    
println(tags);
```

#### **`reduce((A, A) -> A): A`**

Permite combinar los elementos de la lista en un solo valor. Para ello, es necesario pasar una lambda `(A, A) -> A`, dicha función toma dos parámetros del tipo que contiene la colección y devuelve un único resultado del mismo tipo, esta función se aplica una y otra vez reduciendo el número de valores que contiene la lista hasta obtener un único valor

```kotlin
// Esta operación suma todos los elementos de la lista y devuelve un valor
val suma = lista.reduce { acc, i -> acc + i } // 10
```

Este método fallará si se ejecuta sobre una lista vacía. Para evitar este problema, se puede utilizar el método `reduceOrNull` que devolvera null en caso de que la lista esté vacía.

**`get(Int): A`**

Obtiene un elemento en un índice específico. Si intentas acceder a un índice fuera del rango, arrojará una excepción.

```kotlin
val valor = lista.get(2) // 3
```

#### **`remove(Int)`**

Elimina un elemento en una **lista mutable**. Si existen elementos duplicados, solo elimina la primera ocurrencia.

```kotlin
listaMutable.remove(2)
println(listaMutable) // [1, 3, 4]
```

#### **`add(A)`**

Agrega un elemento a una lista mutable.

```kotlin
listaMutable.add(5)
println(listaMutable) // [1, 3, 4, 5]
```

***

## **Mapas**

Un **Mapa** es una colección de pares clave-valor. Cada clave debe ser única, pero los valores pueden repetirse.

#### **Crear un Mapa**

```kotlin
val mapaInmutable = mapOf(1 to "uno", 2 to "dos", 3 to "tres")
val mapaMutable = mutableMapOf(1 to "uno", 2 to "dos", 3 to "tres")
```

### Métodos



| Método     | **Listas**                         | **Mapas**                          | **Sets**                         |
| ---------- | ---------------------------------- | ---------------------------------- | -------------------------------- |
| `map()`    | Transforma cada elemento           | Transforma clave-valor             | Transforma cada elemento         |
| `filter()` | Filtra elementos según condición   | Filtra entradas clave-valor        | Filtra elementos según condición |
| `reduce()` | Reduce elementos a un solo valor   | No aplicable                       | No aplicable                     |
| `get()`    | Accede por índice                  | Accede por clave                   | No aplicable                     |
| `remove()` | Elimina por valor en lista mutable | Elimina por clave en mapa mutable  | Elimina por valor en set mutable |
| `add()`    | Agrega a lista mutable             | Agrega o actualiza en mapa mutable | Agrega a set mutable             |
