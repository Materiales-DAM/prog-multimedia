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

# Herencia

## Clases open y herencia básica

La **herencia** es un mecanismo que permite a una clase (llamada **subclase** o **clase derivada**) heredar propiedades y métodos de otra clase (llamada **superclase** o **clase base**). Esto facilita la reutilización del código y permite que una clase hija extienda o modifique el comportamiento de la clase padre.

En Kotlin, todas las clases son **final** por defecto, lo que significa que no se pueden heredar a menos que se marquen explícitamente con la palabra clave `open`. Para crear una clase que pueda ser heredada, debes marcarla como `open`.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>// Clase base (superclase)
</strong>open class Animal {
    open fun sonido() {
        println("El animal hace un sonido")
    }
}

// Clase derivada (subclase) que hereda de Animal
class Perro : Animal() {
    override fun sonido() {
        println("El perro ladra")
    }
}

fun main() {
    val miPerro = Perro()
    miPerro.sonido()  // Salida: "El perro ladra"
}
</code></pre>

En este ejemplo, la clase `Perro` hereda de `Animal` y sobrescribe el método `sonido` usando la palabra clave `override`.

## Clases abstractas

Las **clases abstractas** son clases que no se pueden instanciar directamente. Sirven como plantillas para que otras clases las hereden. Una clase abstracta puede contener métodos abstractos (sin implementación) y métodos concretos (con implementación).

```kotlin
// Clase abstracta
abstract class Animal {
    // Método concreto con implementación
    fun dormir() {
        println("El animal está durmiendo")
    }

    // Método abstracto, sin implementación
    abstract fun sonido()
}

// Subclase que hereda de Animal y debe implementar el método abstracto
class Perro : Animal() {
    override fun sonido() {
        println("El perro ladra")
    }
}

fun main() {
    val miPerro = Perro()
    miPerro.dormir()  // Salida: "El animal está durmiendo"
    miPerro.sonido()  // Salida: "El perro ladra"
}
```

## Herencia múltiple con interfaces

Kotlin no permite herencia múltiple de clases, pero se puede simular utilizando **interfaces**. Una **interface** puede contener métodos abstractos y métodos con implementación predeterminada, y una clase puede implementar múltiples interfaces.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>interface Movible {
</strong>    fun mover()
}

interface Volable {
    fun volar() {
        println("Volando...")
    }
}

// Implementando múltiples interfaces
class Avion : Movible, Volable {
    override fun mover() {
        println("El avión se mueve por la pista")
    }
}

fun main() {
    val avion = Avion()
    avion.mover()  // Salida: "El avión se mueve por la pista"
    avion.volar()  // Salida: "Volando..."
}
</code></pre>
