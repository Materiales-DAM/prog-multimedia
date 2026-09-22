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

# Activity

En Jetpack Compose, una **Activity** actúa como un contenedor para tu interfaz de usuario declarativa. En lugar de inflar un archivo XML (como se hacía tradicionalmente con `setContentView`),  la UI se define directamente dentro de la `Activity` usando el método `setContent`. Este método es el punto de entrada para que Compose maneje la interfaz.

Ejemplo básico de una **Activity** en Jetpack Compose:

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Text(text = "Hola, Jetpack Compose")
        }
    }
}
```
