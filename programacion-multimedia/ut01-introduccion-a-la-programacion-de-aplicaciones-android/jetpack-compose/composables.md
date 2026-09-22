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

# Composables

El componente básico de este framework son las funciones **Composable**, que son las que permiten construir bloques de interfaz reutilizables.

Una función `@Composable` es el bloque básico que define una parte de la interfaz. Para crear uno, solo necesitas anotar una función con `@Composable`.

```kotlin
import androidx.compose.material.Text
import androidx.compose.runtime.Composable

@Composable
fun Greeting(name: String) {
    Text(text = "Hola, $name!")
}
```

Esta función `Greeting` recibe un parámetro `name` y muestra un `Text` que saluda con ese nombre.

Para usar Compose en una actividad, debes usar `setContent` dentro de `onCreate` para especificar qué función Composable se debe renderizar.

```kotlin
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.material.MaterialTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MaterialTheme {
                Greeting("Mundo")
            }
        }
    }
}
```

En este ejemplo, dentro de `setContent`, se llama a la función `Greeting`, que mostrará el texto "Hola, Mundo!".

## Previsualizar un Composable

Android Studio te permite previsualizar tus funciones Composable sin necesidad de ejecutar la app. Para habilitar esta vista previa, hay que añadir la anotación `@Preview` al método `Composable`.

```kotlin
import androidx.compose.ui.tooling.preview.Preview

@Preview
@Composable
fun PreviewGreeting() {
    Greeting("Android")
}
```

Esto mostrará una vista previa de cómo se verá el Composable directamente en Android Studio.
