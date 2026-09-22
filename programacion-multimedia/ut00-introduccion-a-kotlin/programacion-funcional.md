---
cover: ../.gitbook/assets/Kotlin-Vs-Java.png
coverY: 93.28257686676427
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

# Programación funcional

## Lambdas

Una **lambda** es una función anónima, es decir, una función que no tiene un nombre, y que puede ser tratada como una expresión. En esencia, es una función "en línea" que puede ser pasada como argumento a otras funciones o asignada a variables. Las lambdas son fundamentales en la programación funcional, ya que permiten manejar funciones como si fueran valores, facilitando la creación de código más modular y reutilizable.

La sintaxis de las **lambdas** en Kotlin es una de las características que la hacen muy flexible y concisa en comparación con otros lenguajes de programación.&#x20;

### **Sintaxis**

La sintaxis general de una lambda en Kotlin es la siguiente:

```kotlin
val nombreLambda: (TipoArgumento1, TipoArgumento2) -> TipoRetorno = { argumento1: TipoArgumento1, argumento2: TipoArgumento2 -> cuerpoDeLaLambda }
```

* **Parte izquierda**: Se define el tipo de la lambda `(TipoArgumento1, TipoArgumento2) -> TipoRetorno`, donde se indica el número de argumentos, sus tipos y el tipo de retorno.
* **Parte derecha**: Se escribe la implementación de la lambda, es decir, cómo va a operar con los argumentos `{ argumento1, argumento2 -> expresión }`.

Por ejemplo, una lambda que sirve para sumar dos enteros se podría definir así:

```kotlin
val suma: (Int, Int) -> Int = { a: Int, b: Int -> a + b }
```

La sintaxis anterior es la forma más explícita de expresar una función lambda, pero es posible hacerlo de forma más concisa gracias a los siguiente mecanismos:

#### **Inferencia de tipos**:

#### Si Kotlin puede inferir el tipo de los argumentos a partir del contexto, no es necesario especificarlos dentro de la lambda.

```kotlin
val suma: (Int, Int) -> Int = { a, b -> a + b }
```

En este caso, los tipos `Int` se han inferido a partir de la declaración de tipo de la variable `suma`, por lo que no es necesario volver a escribirlos dentro de la lambda.

#### **Uso del parámetro implícito `it`**

Si la lambda tiene un solo argumento, puedes omitir su nombre y usar el identificador implícito `it`.

```kotlin
val cuadrado: (Int) -> Int = { it * it }
```

Aquí, `it` representa el único argumento de tipo `Int`.

#### **Lambdas sin return explícito**

Si la lambda tiene un solo bloque de código, no es necesario usar `return`, ya que la última expresión evaluada dentro de la lambda es lo que se retorna automáticamente.

```kotlin
val multiplicar: (Int, Int) -> Int = { a, b -> a * b }
```

La lambda anterior retorna automáticamente el valor de `a * b`.

#### **Lambdas multilinea**

Si una lambda tiene múltiples expresiones, puedes usar un bloque `{}` y cada línea se ejecutará en secuencia. La última expresión del bloque será el valor de retorno.

```kotlin
val operaciones: (Int, Int) -> Int = { a, b ->
    println("Operando con $a y $b")
    a + b
}
println(operaciones(5, 3))  // Resultado: 8
```

En este caso, la lambda realiza una operación de suma después de imprimir un mensaje. La suma de `a + b` es el valor de retorno.

## Funciones de orden superior

Las **funciones de orden superior** son funciones que pueden:

1. **Recibir una o más funciones como parámetros**.
2. **Retornar una función como resultado**.

En otras palabras, las funciones de orden superior tratan a las funciones como "ciudadanos de primera clase", lo que significa que pueden ser pasadas y manipuladas como cualquier otro tipo de dato (como enteros, cadenas, etc.). Esto es un concepto clave en la **programación funcional**.

Aquí un ejemplo donde usamos una lambda en una función `operar`, que toma dos enteros y una lambda para realizar la operación entre ellos:

```kotlin
fun operar(a: Int, b: Int, operacion: (Int, Int) -> Int): Int {
    // Aplicamos la operación a los valores a y be y devolvemos el resultado
    return operacion(a, b)
}

val resultado = operar(3, 4) { x, y -> x + y }  // Lambda que suma dos valores
println(resultado)  // Resultado: 7
```

En este ejemplo, pasamos la lambda `{ x, y -> x + y }` directamente como argumento de la función `operar`.
