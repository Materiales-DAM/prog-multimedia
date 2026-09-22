---
cover: ../../../../.gitbook/assets/jetpack.png
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

# Dense Points (dp)

En **Kotlin** y **Jetpack Compose**, la notación `.dp` se utiliza para definir valores de tamaño y espaciamiento en **Density-independent Pixels (dp)**. Esta unidad es independiente de la resolución de pantalla, lo que garantiza que los elementos tengan el mismo tamaño en diferentes dispositivos, independientemente de la densidad de píxeles.

## ¿Qué es `dp`?

`dp` es una unidad de medida utilizada en Android para definir dimensiones como márgenes, rellenos, alturas, anchos, etc. Su principal ventaja es que se ajusta automáticamente a diferentes densidades de pantalla, ofreciendo una apariencia uniforme en dispositivos con distintas resoluciones.

Cuando se trabaja con **Jetpack Compose**, muchas propiedades de los elementos de la interfaz de usuario (UI) como anchos, alturas, paddings y márgenes requieren que se definan dimensiones en `dp`. Para eso, puedes usar la notación `.dp`.

```kotlin
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp

@Composable
fun MyComposable() {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp) // Padding de 16 dp
    ) {
        Button(
            onClick = { /* Acción */ },
            modifier = Modifier
                .height(48.dp) // Altura de 48 dp
                .width(200.dp) // Ancho de 200 dp
        ) {
            Text(text = "Presionar")
        }
    }
}
```

## ¿Por qué usar `dp`?

En Android, los dispositivos tienen diferentes densidades de pantalla, y el uso de `dp` asegura que el tamaño de los elementos de la interfaz de usuario sea consistente entre dispositivos. Sin esta unidad, un elemento podría verse más grande o más pequeño dependiendo de la resolución del dispositivo.

## Scalable Pixels

Para trabajar con tamaños, existen otras unidades como `sp` (para texto, ya que respeta el tamaño de la fuente configurada por el usuario). La principal diferencia es que `dp` se usa para dimensiones visuales, mientras que `sp` es más adecuado para el tamaño de texto.
