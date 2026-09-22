---
cover: ../.gitbook/assets/Kotlin-Vs-Java.png
coverY: 103.88286969253295
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

# Estructuras de control

En esta sección vamos a repasar las estructuras de control que son diferentes a Java

## Bucle for

La sintaxis del bucle for en Kotlin es muy similar a la del for-each  en Java

En Kotlin desaparece los tipos primitivos, lo cual simplifica considerablemente el sistema de tipos, ya que en este lenguaje todos los valores son objetos.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java"><strong>List&#x3C;Integer> numbers = List.of(1, 2, 3);
</strong><strong>for(Integer number: numbers) {
</strong><strong>    System.out.println(number);
</strong><strong>}
</strong></code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">val numbers = listOf(1, 2, 3)
for(number in numbers) {
    println(number)
}
</code></pre></td></tr></tbody></table>

## Bucle fori

El bucle fori no existe en Kotlin de manera explícita, podemos hacer algo similar usando el bucle `for` y el campo `indices`.

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java"><strong>List&#x3C;Integer> numbers = List.of(1, 2, 3);
</strong><strong>for(int i = 0; i&#x3C; numbers.size(); i++) {
</strong><strong>    System.out.println(numbers.get(i));
</strong><strong>}
</strong></code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">val numbers = listOf(1, 2, 3);
for(i in numbers.indices) {
    println(numbers.get(i));
}
</code></pre></td></tr></tbody></table>

## Switch / when

La estructura de control `switch` de Java se traduce en la estructura `when` en Kotlin

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th></tr></thead><tbody><tr><td><strong>Java</strong></td><td><pre class="language-java"><code class="lang-java">int dayAsInt = 1;
switch (dayAsInt) {
    case 1:
        System.out.println("Sunday");
        break;
    case 2:
        System.out.println("Monday");
        break;
    case 3:
         System.out.println("Tuesday");
        break;
    case 4:
        System.out.println("Wednesday");
        break;
    case 5:
        System.out.println("Thursday");
        break;
    case 6:
        System.out.println("Friday");
        break;
    case 7:
        System.out.println("Saturday");
        break;
    default:
        System.out.println("invalid day");
}
</code></pre></td></tr><tr><td><strong>Kotlin</strong></td><td><pre class="language-kotlin"><code class="lang-kotlin">val dayAsInt = 1

when (dayAsInt) {
    1 -> println("Sunday")
    2 -> println("Monday")
    3 -> println("Tuesday")
    4 -> println("Wednesday")
    5 -> println("Thursday")
    6 -> println("Friday")
    7 -> println("Saturday")
    else -> {
        // notice you can use a block
        println("invalid day")
    }
}
</code></pre></td></tr></tbody></table>
