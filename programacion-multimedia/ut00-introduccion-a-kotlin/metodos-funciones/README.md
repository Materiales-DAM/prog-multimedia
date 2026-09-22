---
cover: ../../.gitbook/assets/Kotlin-Vs-Java.png
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

# Métodos / funciones

&#x20;En **Kotlin**, un método se define como una **función** que puede pertenecer a una clase o ser una función global (también llamada función de nivel superior). La sintaxis para definir una función es clara y concisa.

La palabra clave para definir una función en Kotlin es `fun`, seguida del nombre de la función, los parámetros (si los hay), el tipo de retorno (si lo hay) y el cuerpo de la función.

```kotlin
fun nombreDeLaFuncion(parametros): TipoDeRetorno {
    // Cuerpo de la función
}
```

## **Función sin parámetros y sin retorno**

Esta función no recibe ningún parámetro ni devuelve un valor. En Kotlin, si no se especifica un tipo de retorno, se asume que es `Unit` (similar a `void` en otros lenguajes).

```kotlin
fun saludar(): Unit {
    println("Hola, Mundo!")
}

fun saludar2() {
    println("Hola, Mundo!")
}
```

Llamada de la función:

```kotlin
saludar() // Salida: Hola, Mundo!
```

## **Función con parámetros**

Puedes definir una función con uno o más parámetros. Debes especificar el tipo de cada parámetro.

```kotlin
fun saludarConNombre(nombre: String) {
    println("Hola, $nombre!")
}
```

Llamada de la función:

```kotlin
saludarConNombre("Juan") // Salida: Hola, Juan!
```

## **Función con un valor de retorno**

Si una función devuelve un valor, debes especificar el tipo de retorno después de los parámetros.

```kotlin
fun sumar(a: Int, b: Int): Int {
    return a + b
}
```

Llamada de la función:

```kotlin
val resultado = sumar(3, 4)
println(resultado) // Salida: 7
```

## **Funciones de una sola línea**

Si una función solo tiene una expresión, puedes usar la **sintaxis de expresión** para simplificar la definición. No es necesario usar las llaves ni la palabra clave `return`.

```kotlin
fun multiplicar(a: Int, b: Int): Int = a * b
```

Llamada de la función:

```kotlin
val resultado = multiplicar(3, 5)
println(resultado) // Salida: 15
```

## **Funciones con valores por defecto**

Puedes asignar valores por defecto a los parámetros de una función. Si no se pasa un argumento, se utilizará el valor predeterminado.

```kotlin
fun saludarConOpcional(nombre: String = "Desconocido") {
    println("Hola, $nombre!")
}
```

Llamada de la función:

```kotlin
saludarConOpcional("María")  // Salida: Hola, María!
saludarConOpcional()         // Salida: Hola, Desconocido!
```

## **Métodos dentro de una clase (Funciones miembro)**

Las funciones también pueden estar dentro de clases. En este caso, las llamamos **métodos**. Se accede a ellos a través de una instancia de la clase.

```kotlin
class Persona(val nombre: String) {

    fun saludar() {
        println("Hola, mi nombre es $nombre")
    }
}
```
