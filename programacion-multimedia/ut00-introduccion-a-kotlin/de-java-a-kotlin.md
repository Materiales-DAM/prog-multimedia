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

# De Java a Kotlin

Kotlin son dos lenguajes clave en el ecosistema de desarrollo de Android, y aunque ambos se ejecutan en la **Java Virtual Machine (JVM)** y tienen compatibilidad mutua, presentan diferencias significativas en su enfoque y características.

## Sintaxis básica

### Punto y coma

En Kotlin no es necesario usar el símbolo ; al final de las sentencias

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java"><strong>System.out.println("hola");
</strong></code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">print("hola")
</code></pre></td></tr></tbody></table>

### Declaración de variables

La sintaxis de declaración de variables en Kotlin favorece el uso de la inferencia de tipos

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java"><strong>// Normalmente en Java se pone el tipo
</strong><strong>String s = "Hola";
</strong><strong>// También es posible la inferencia de tipos
</strong><strong>var s2 = "mundo";
</strong></code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">// Esta variable es de tipo String
var s = "Hola"
// Declaración con el tipo explícito
var s2: String = "mundo"
</code></pre></td></tr></tbody></table>

### Declaración de constantes

La sintaxis de declaración de constantes en Kotlin es más concisa

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java"><strong>// Se usa la palabara reservada final
</strong><strong>final String s = "Hola";
</strong>
</code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">// Se utiliza val en lugar de var
val s = "Hola"

</code></pre></td></tr></tbody></table>

### Verboso vs conciso

La sintaxis de Java se considera verbosa, es decir que para expresar algo hace falta escribir más código del que sería necesario en otros lenguajes concisos (como Kotlin).

Por ejemplo, veamos el clásico ejemplo Hello world

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java" data-title="HelloWorld.java"><code class="lang-java">public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello world!");
    }
}
</code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin" data-title="HelloWorld.kt"><code class="lang-kotlin">fun main(args : Array&#x3C;String>) {
    println("Hello, World!")
}
</code></pre></td></tr></tbody></table>

### Instanciar objetos

En Kotlin ya no se utiliza la palabra reservada `new`

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java">Person person = new Person("Bob", "Esponja");
</code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">val person = Person("Bob", "Esponja");
</code></pre></td></tr></tbody></table>

### Tipos básicos / primitivos

En Kotlin desaparece los tipos primitivos, lo cual simplifica considerablemente el sistema de tipos, ya que en este lenguaje todos los valores son objetos.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java"><strong>int num1 = 3;
</strong><strong>Integer num2 = 2;
</strong><strong>
</strong><strong>int res = num1 + num2;
</strong></code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">// num1 es de tipo Int
val num1 = 3
// num2 es de tipo Int
val num2 = 2
// res es de tipo Int
val res = num1 + num2;
</code></pre></td></tr></tbody></table>

#### Números enteros

| Tipo    | Tamaño (bits) | Valor mínimo                      | Valor máximo                        |
| ------- | ------------- | --------------------------------- | ----------------------------------- |
| `Byte`  | 8             | -128                              | 127                                 |
| `Short` | 16            | -32768                            | 32767                               |
| `Int`   | 32            | -2,147,483,648 (-231)             | 2,147,483,647 (231 - 1)             |
| `Long`  | 64            | -9,223,372,036,854,775,808 (-263) | 9,223,372,036,854,775,807 (263 - 1) |

#### Números reales

| Tipo     | Tamaño | Mantisa | Exponente | Precisión (digitos) |
| -------- | ------ | ------- | --------- | ------------------- |
| `Float`  | 32     | 24      | 8         | 6-7                 |
| `Double` | 64     | 53      | 11        | 15-16               |

#### Booleanos

El tipo **`Boolean`** sirve para representar valores booleanos

#### Caracteres

El tipo **`Char`** sirve para representar caracteres y **`String`** para cadenas de caracteres

## Interpolacion de texto

La interpolación de texto en Kotlin es una forma conveniente de construir cadenas de texto dinámicamente, insertando valores de variables o expresiones directamente en una cadena. En lugar de concatenar con operadores como `+`, Kotlin permite insertar variables o expresiones dentro de las cadenas usando el símbolo `$`.

Para insertar una variable dentro de una cadena de texto, simplemente antepones el símbolo `$` a la variable dentro de la cadena. Si necesitas evaluar una expresión más compleja, puedes utilizar `${}`.

```kotlin
val nombre = "Ana"
val saludo = "Hola, $nombre!"
println(saludo) // Salida: Hola, Ana!
```

**Interpolación con una expresión**

```kotlin
val x = 5
val y = 10
val resultado = "La suma de $x y $y es ${x + y}"
println(resultado) // Salida: La suma de 5 y 10 es 15
```
