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

# Null

En Kotlin, el manejo de valores nulos (null) está diseñado para evitar los errores comunes asociados con los nulos, como las famosas **NullPointerException** (NPE) en otros lenguajes como Java. Kotlin introduce una serie de características que permiten gestionar los valores nulos de manera segura.

## Tipos nulos y no nulos

Kotlin diferencia claramente entre tipos que **pueden** contener un valor nulo y tipos que **no pueden**. Por defecto, las variables no pueden ser nulas. Si intentas asignar un valor `null` a una variable que no puede ser nula, obtendrás un error en tiempo de compilación.

**Ejemplo de variable no nula**

```kotlin
var nombre: String = "Kotlin"
nombre = null  // Error de compilación
```

Si quieres permitir que una variable pueda ser nula, tienes que declarar explícitamente que puede contener un valor nulo utilizando el tipo nullable. Esto se hace añadiendo `?` al tipo.

**Ejemplo de variable nullable**

```kotlin
var nombre: String? = "Kotlin"
nombre = null  // Esto es permitido
```

## Operador de llamada segura (`?.`)

Cuando tienes un valor que puede ser nulo, debes manejarlo de forma segura. Una forma de hacerlo es utilizando el **operador de llamada segura** `?.`. Este operador ejecuta una operación solo si la variable no es nula, de lo contrario devuelve `null`.

```kotlin
var longitud: Int? = nombre?.length  // Si nombre es nulo, longitud será null
```

## Operador Elvis (`?:`)

El operador Elvis (`?:`) te permite proporcionar un valor predeterminado en caso de que la expresión a la izquierda del operador sea `null`.

```kotlin
var longitud: Int = nombre?.length ?: 0  // Si nombre es null, longitud será 0
```

## Operador de afirmación no nula (`!!`)

Si estás absolutamente seguro de que una variable no es nula y quieres forzar a Kotlin a tratarla como no nula, puedes usar el operador de afirmación no nula (`!!`). Sin embargo, si la variable resulta ser `null` en tiempo de ejecución, obtendrás una excepción `NullPointerException`.

```kotlin
var longitud: Int = nombre!!.length  // Si nombre es null, lanzará una excepción
```

Debemos evitar utilizar este operador.

## Funciones para trabajar con nulos

Kotlin ofrece varias funciones útiles para trabajar con valores nulos de manera segura, como `let`, `apply`, `run`, entre otras. Estas funciones son muy útiles para manejar variables nulas de forma fluida y concisa.

### **Let**

La función let se utiliza en combinación con el operador de llamada segura para conseguir que un bloque de código se ejecute solo en caso de que el valor nullable no sea null.

```kotlin
nombre?.let { nombre ->
    // Este código se ejecuta solo si nombre no es null
    println("El nombre tiene ${nombre.length} caracteres")
}
```

### Apply

La función `apply` **siempre** devuelve el objeto receptor (incluso si es `null`), y se utiliza principalmente para modificar el objeto. En el caso de objetos nulos, si el objeto es `null`, el bloque no se ejecuta, pero igual devuelve `null`.

**Ejemplo:**

```kotlin
val persona: Persona? = null

persona?.apply {
    nombre = "Juan"
    edad = 30
}
```

En este caso, si `persona` es `null`, el bloque de código dentro de `apply` no se ejecuta, y `persona` permanece `null`. Si no fuera `null`, el bloque se ejecutaría y permitiría modificar el objeto.

### Run

La función `run` es ideal cuando necesitas trabajar con un objeto nulo y obtener un resultado específico (que no necesariamente es el objeto). Si el objeto es `null`, el bloque de código no se ejecuta, y devuelve directamente `null`.

```kotlin
val longitudNombre: Int? = persona?.run {
    nombre.length  // Retorna la longitud del nombre
}
```

En este ejemplo, si `persona` es `null`, la expresión `run` no se ejecuta y `longitudNombre` también será `null`. Si `persona` no es `null`, entonces `run` ejecuta el bloque de código y retorna el resultado de `nombre.length`.

**Uso típico:** Se utiliza cuando quieres transformar el objeto o realizar una operación sobre él y obtener un resultado diferente, pero sin ejecutar nada si el objeto es nulo.
