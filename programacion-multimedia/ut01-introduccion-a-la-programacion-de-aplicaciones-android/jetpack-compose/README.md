---
cover: ../../.gitbook/assets/jetpack.png
coverY: 0
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

# Jetpack Compose

En este curso vamos a estudiar el desarrollo de aplicaciones Android con **Jetpack Compose,** se trata de un moderno **kit de herramientas declarativo** de Android que permite crear interfaces de usuario completamente en código, sin necesidad de XML. Lanzado oficialmente por Google en 2020, Jetpack Compose está escrito en Kotlin y simplifica la creación de interfaces gracias a un enfoque declarativo, inspirado por frameworks como React o SwiftUI.

```kotlin
@Composable
fun Greeting() {
    Column {
        Text(text = "Hola, Mundo!")
        Button(onClick = { /* Acción al presionar */ }) {
            Text(text = "Presionar")
        }
    }
}
```

Las principales características son:

* **Declarativo completo**: La interfaz se construye mediante código declarativo. Se describe el estado de la UI y Jetpack Compose se encarga de renderizar los cambios cuando el estado subyacente cambia.
* **UI Reactiva**: La interfaz está vinculada al estado de los datos. Si el estado cambia, la UI se actualiza automáticamente, sin necesidad de manipular manualmente las vistas.
* **Menos fragmentación**: Todo, desde el diseño de la UI hasta la lógica, puede estar en el mismo archivo, lo que facilita el manejo del código.
* **Optimización del rendimiento**: Jetpack Compose utiliza menos jerarquías de vistas que el enfoque basado en XML, lo que puede mejorar el rendimiento en términos de memoria y procesamiento.
* **Compatibilidad con vistas heredadas**: Aunque es un enfoque moderno, Compose es compatible con vistas tradicionales de Android, lo que permite mezclar ambas técnicas si es necesario.
