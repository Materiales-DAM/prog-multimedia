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

# Checkbox

Un `Checkbox` es un componente que permite a los usuarios seleccionar o deseleccionar una opción.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Para añadir un componente de este tipo hace falta definir:

* Un estado booleano (`true` para seleccionado, `false` para no seleccionado).
* Un evento de cambio (`onCheckedChange`), que se dispara cuando el usuario hace clic en el `Checkbox`.

Aquí tienes un ejemplo básico:

```kotlin
@Composable
fun BasicCheckbox() {
    // Estado del checkbox
    var isChecked by remember { mutableStateOf(false) }
    
    // Checkbox con un cambio de estado
    Checkbox(
        checked = isChecked,
        onCheckedChange = { isChecked = it }
    )
}
```

* `checked`: define si el `Checkbox` está marcado.
* `onCheckedChange`: actualiza el estado cada vez que el usuario selecciona o deselecciona el `Checkbox`.

Es común querer añadir texto junto al `Checkbox` para identificar su propósito. Para ello, vamos a aliniear dentro de un `Row` el `Checkbox` y un `Text`.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>@Composable
</strong>fun LabeledCheckbox() {
    var isChecked by remember { mutableStateOf(false) }

    Row(
        verticalAlignment = Alignment.CenterVertically
    ) {
        Checkbox(
            checked = isChecked,
            onCheckedChange = { isChecked = it }
        )
        Spacer(modifier = Modifier.width(8.dp))
        Text(text = if (isChecked) "Checked" else "Unchecked")
    }
}
</code></pre>

### Colores

Puedes cambiar los colores del `Checkbox` para adaptarlo al estilo de tu aplicación. Aquí se usa `colors` para personalizar los colores en diferentes estados.

```kotlin
@Composable
fun ColoredCheckbox() {
    var isChecked by remember { mutableStateOf(false) }

    Checkbox(
        checked = isChecked,
        onCheckedChange = { isChecked = it },
        colors = CheckboxDefaults.colors(
            checkedColor = Color.Green,
            uncheckedColor = Color.Red,
            checkmarkColor = Color.White
        )
    )
}
```

### Estado indeterminado

Un `Checkbox` indeterminado es útil en casos donde el estado no es ni seleccionado ni deseleccionado, como en selecciones parciales.

```kotlin
@Composable
fun LabeledCheckbox() {
    var state by remember { mutableStateOf(ToggleableState.Indeterminate) }

    Row(
        modifier = Modifier.padding(5.dp),
        verticalAlignment = Alignment.CenterVertically
    ) {
        TriStateCheckbox(
            state = state,
            onClick = {
                state = when (state) {
                    ToggleableState.On -> ToggleableState.Off
                    ToggleableState.Off -> ToggleableState.Indeterminate
                    ToggleableState.Indeterminate -> ToggleableState.On
                }
            }
        )
        Text(text = "Indeterminado")
    }
}
```

**ToggleableState** tiene tres valores: `On`, `Off`, y `Indeterminate`.
