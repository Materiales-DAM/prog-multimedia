---
cover: .gitbook/assets/kotlin.png
coverY: 0
---

# Introducción

Kotlin es un lenguaje de programación moderno, diseñado principalmente para compilarse sobre la plataforma Java Virtual Machine (JVM), aunque también puede compilarse a JavaScript y código nativo. Fue desarrollado por JetBrains y lanzado oficialmente en 2011.&#x20;

Algunas de sus características clave son:

* **Interoperabilidad con Java**: Kotlin es 100% interoperable con Java, lo que significa que puede usarse junto con código Java existente sin problemas. Esto lo hace ideal para proyectos grandes que buscan modernizarse gradualmente.
* **Sintaxis concisa y expresiva**: Kotlin reduce significativamente la cantidad de código boilerplate en comparación con Java, lo que lo hace más fácil de leer y escribir. Ofrece una sintaxis más limpia y moderna, similar a otros lenguajes como Swift o Python.
* **Seguridad frente a nulabilidad**: Kotlin incluye un sistema de tipos que previene errores relacionados con `null`. Las variables son no-null por defecto, y es necesario especificar explícitamente si una variable puede ser nula, ayudando a evitar el clásico problema del "NullPointerException".
* **Funciones de orden superior y lambdas**: Kotlin soporta programación funcional, lo que permite trabajar con funciones como ciudadanos de primera clase. Las funciones lambda y las funciones de orden superior permiten escribir código más expresivo y modular.
* **Corutinas**: Kotlin introduce un modelo de concurrencia más sencillo mediante las corutinas, lo que permite manejar operaciones asíncronas de manera más eficiente y con menos complejidad que los hilos tradicionales.
* **Compatibilidad multiplataforma**: Aunque Kotlin se usa principalmente para Android y JVM, también permite escribir código que puede ser compilado para múltiples plataformas, incluidos sistemas nativos como iOS, lo que lo convierte en una opción atractiva para el desarrollo multiplataforma.

En resumen, Kotlin es un lenguaje que busca ser más seguro, conciso y moderno que Java, con un enfoque en la interoperabilidad, la seguridad y la facilidad de uso, especialmente en entornos móviles como Android.

## ¿Por qué Kotlin?

Kotlin se ha consolidado como el lenguaje oficial para el desarrollo de aplicaciones Android, respaldado por Google desde 2017. Su diseño moderno y su interoperabilidad con Java lo hacen ideal para esta plataforma, ofreciendo una alternativa más concisa y eficiente al tradicional Java.

### Jetpack Compose

**Jetpack Compose** es un **framework declarativo** desarrollado por Google para construir interfaces de usuario en Android. A diferencia del enfoque tradicional basado en XML y vistas imperativas, Compose permite diseñar interfaces de forma más intuitiva y eficiente usando código Kotlin puro.

Kotlin, como lenguaje de programación oficial para Android, es la base sobre la cual se construye **Jetpack Compose**. Con su sintaxis concisa y moderna, Kotlin facilita la escritura de código más limpio y expresivo. Muchas de las ventajas de Kotlin, como la seguridad frente a `null` y las funciones de alto orden, son claves para el éxito de Jetpack Compose, permitiendo que los desarrolladores creen interfaces más robustas y menos propensas a errores.

En lugar de describir el diseño de una interfaz en archivos XML y luego vincularlos con el código Java o Kotlin, en Compose las interfaces se construyen directamente en el código usando funciones. Esto hace que la creación, actualización y personalización de la UI sea más directa y sencilla.
