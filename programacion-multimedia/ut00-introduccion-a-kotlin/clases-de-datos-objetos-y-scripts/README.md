---
cover: ../../.gitbook/assets/Kotlin-Vs-Java.png
coverY: 91.16251830161055
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

# Clases de datos, objetos y scripts

En Kotlin, las **data classes**, las **object classes** y los **companion objects** son conceptos que proporcionan diferentes formas de estructurar y organizar el código de manera más eficiente, cada uno con su propia utilidad.

## Clases de datos

Las **data classes** son clases especiales cuyo propósito principal es contener datos. Kotlin simplifica la creación de clases de datos mediante las `data classes`, proporcionando automáticamente métodos comunes como `toString()`, `equals()`, `hashCode()` y `copy()`, basándose en los atributos de la clase.

**Características de las `data classes`:**

* Deben tener al menos un parámetro en el constructor primario.
* Kotlin genera automáticamente funciones como `toString()`, `equals()`, `hashCode()` y `copy()`.
* Los parámetros del constructor primario se usan para las propiedades de la clase (val o var).

```kotlin
data class Persona(val nombre: String, val edad: Int)

val persona1 = Persona("Juan", 30)
val persona2 = Persona("Juan", 30)

// `equals()` es generado automáticamente
println(persona1 == persona2)  // Imprime: true

// `toString()` también está implementado automáticamente
println(persona1)  // Imprime: Persona(nombre=Juan, edad=30)

// `copy()` permite copiar un objeto con algunas propiedades modificadas
val persona3 = persona1.copy(edad = 31)
println(persona3)  // Imprime: Persona(nombre=Juan, edad=31)
```

Las `data classes` son muy útiles para modelar datos y simplifican mucho el código necesario para trabajar con ellos, ya que no tienes que escribir manualmente los métodos básicos.

Estas clases son el equivalente de los POJOs de Java, que son las clases de datos en las que debíamos generar manualmente constructores, getter, setters, hashCode, equals y toString.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java" data-title="Persona.java"><code class="lang-java">import java.util.Objects;

public class Persona {
    private String nombre;
    private String apellidos;
    private int edad;

    public Persona(String nombre, String apellidos, int edad) {
        this.nombre = nombre;
        this.apellidos = apellidos;
        this.edad = edad;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getApellidos() {
        return apellidos;
    }

    public void setApellidos(String apellidos) {
        this.apellidos = apellidos;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Persona persona = (Persona) o;
        return edad == persona.edad &#x26;&#x26; Objects.equals(nombre, persona.nombre) &#x26;&#x26; Objects.equals(apellidos, persona.apellidos);
    }

    @Override
    public int hashCode() {
        return Objects.hash(nombre, apellidos, edad);
    }

    @Override
    public String toString() {
        return "Persona{" +
                "nombre='" + nombre + '\'' +
                ", apellidos='" + apellidos + '\'' +
                ", edad=" + edad +
                '}';
    }
}

</code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin" data-title="Persona.kt"><code class="lang-kotlin">data class Persona(
    val nombre: String, 
    val apellidos:String, 
    val edad: Int
)
</code></pre></td></tr></tbody></table>

## **Object Classes**

Un **object class** en Kotlin se usa para crear **objetos singleton**, es decir, clases de las cuales solo puede existir **una única instancia**. Esto es útil para casos donde necesitas tener una única instancia compartida por todo el programa, como en patrones de diseño como Singleton o para almacenar constantes y funciones relacionadas.

Algunas de sus características son:

* Se inicializa de manera **perezosa** (lazy), es decir, solo cuando se accede por primera vez.
* Puede contener propiedades, métodos y bloques de inicialización.
* No puedes crear múltiples instancias, ya que es un **singleton**.

```kotlin
object Contador {
    var valor: Int = 0

    fun incrementar() {
        valor++
    }
}

Contador.incrementar()
println(Contador.valor)  // Imprime: 1

Contador.incrementar()
println(Contador.valor)  // Imprime: 2
```

En este ejemplo, `Contador` es un singleton, por lo que siempre se accede a la misma instancia.

## **Companion Object**

Un **companion object** es una manera de definir métodos y propiedades estáticas dentro de una clase. Los **companion objects** son objetos que actúan como miembros estáticos de una clase, y puedes acceder a ellos sin necesidad de crear una instancia de la clase.

Algunas de sus características son:

* Solo puede haber **un companion object** por clase.
* Permite definir miembros (funciones o propiedades) a nivel de clase (similares a los estáticos en otros lenguajes como Java).
* Se puede acceder directamente por el nombre de la clase o mediante el nombre del companion object (si se define).
* Es el lugar para declarar constantes y métodos que en Java serían estáticos

```kotlin
class Calculadora {
    fun areaCirculo(r: Double): Double {
        return PI * r * r
    }
    
    companion object {
        // Constante PI
        val PI = 3.1416
        // Este método es estático
        fun sumar(a: Int, b: Int): Int {
            return a + b
        }
    }
}

// Llamada a la función del companion object sin crear una instancia de la clase
val resultado = Calculadora.sumar(10, 20)
println(resultado)  // Imprime: 30

// No compila porque es un método no estático
// val area = Calculadora.areaCirculo(5.5) 
val calculadora = Calculadora()
val area = calculadora.areaCirculo(5.5) 
println(area)
```

## Scripts

Un **script** es un conjunto de instrucciones o código que se ejecuta en un entorno de interpretación o compilación. Los scripts suelen ser utilizados para realizar tareas automatizadas, ejecutar procesos sencillos o probar funcionalidades sin necesidad de crear una aplicación completa.

En **Kotlin**, además de las aplicaciones completas, también es posible escribir scripts. Un script de Kotlin se ejecuta sin tener que crear una clase o una función principal explícita como en otros lenguajes, lo que facilita escribir pequeños fragmentos de código de manera rápida.



1. **Extensión del archivo**: Los scripts en Kotlin tienen la extensión `.kts` en lugar de `.kt`. Esto indica que es un archivo de script y no un archivo estándar de Kotlin que necesita ser compilado como parte de un proyecto.
2. **Estructura de un script**: A diferencia de un archivo Kotlin típico que necesita una clase y una función `main`, en un script de Kotlin puedes escribir directamente las instrucciones que quieres ejecutar.

Por ejemplo, podríamos crear el siguiente script llamado `ejemplo.kts`

{% code title="ejemplo.kts" %}
```kotlin
// Imprimir un mensaje
println("Hola, Kotlin Script!")

// Definir una variable
val nombre = "Juan"
println("Hola, $nombre!")

// Realizar operaciones
val suma = 5 + 3
println("La suma es: $suma")
```
{% endcode %}
