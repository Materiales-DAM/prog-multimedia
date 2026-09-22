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

# RadioButton

Un **RadioButton** es un elemento de interfaz de usuario que permite seleccionar una opción entre un conjunto de alternativas exclusivas, es decir, en un grupo de RadioButtons solo puedes seleccionar una opción a la vez. Al seleccionar uno, cualquier otro previamente seleccionado se deselecciona automáticamente. Este tipo de botón es común en formularios o encuestas, donde se necesita una elección única, como seleccionar un género, un método de pago, o cualquier decisión donde solo una opción puede ser válida.

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

En Jetpack Compose, puedes crear un `RadioButton` individual utilizando el componente `RadioButton`.

```kotlin
@Composable
fun SimpleRadioButton() {
    // Estado para almacenar si el RadioButton está seleccionado
    var isSelected by remember { mutableStateOf(false) }

    // Cambia el estado cuando se hace clic
    Row(
        verticalAlignment = Alignment.CenterVertically
    ) {
        RadioButton(
            selected = isSelected,
            onClick = { isSelected = !isSelected }
        )
        Text(text = "Opción 1", modifier = Modifier.clickable { isSelected = !isSelected })
    }
}
```

Aquí, `selected` indica si el `RadioButton` está activo y `onClick` se utiliza para actualizar su estado. Este código crea un único `RadioButton` que cambia de estado cada vez que se hace clic.

## Grupo de RadioButtons

Para gestionar varios `RadioButton` y permitir solo una selección a la vez (comportamiento típico de un grupo de botones de radio), necesitamos un estado que identifique cuál opción está seleccionada. Este valor se puede manejar mediante un `remember` y cambiarse cuando uno de los `RadioButton` se selecciona.

```kotlin
@Composable
fun RadioButtonGroup() {
    // Lista de opciones
    val options = listOf("Opción 1", "Opción 2", "Opción 3")

    // Estado para almacenar la opción seleccionada
    var selectedOption by remember { mutableStateOf(options[0]) }

    Column {
        // Este foreach crea una Row por cada option en options
        options.forEach { option ->
            Row(verticalAlignment = Alignment.CenterVertically) {
                RadioButton(
                    // Comprueba si option es la opción seleccionada
                    selected = (option == selectedOption),
                    // Si se hace click option pasa a ser la opción seleccionada
                    onClick = { selectedOption = option }
                )
                Text(
                    text = option,
                    // Añadimos un listener al label para que se pueda seleccionar la opción
                    // haciendo click en el texto
                    modifier = Modifier.clickable { selectedOption = option }
                )
            }
        }
    }
}
```

Este código muestra tres opciones en una `Column`. Al hacer clic en cualquiera de los `RadioButton`, el estado `selectedOption` se actualiza y refleja el botón seleccionado.

### Colores

Puedes personalizar el color del `RadioButton` usando el parámetro `colors` y asignando un `RadioButtonDefaults.colors` para especificar el color cuando esté seleccionado o no.

```kotlin
@Composable
fun CustomStyledRadioButton() {
    val opciones = listOf("Rojo", "Azul", "Verde")
    var selectedOption by remember { mutableStateOf(opciones[0]) }

    Column {
        opciones.forEach { opcion ->
            Row(verticalAlignment = Alignment.CenterVertically) {
                RadioButton(
                    selected = (opcion == selectedOption),
                    onClick = { selectedOption = opcion },
                    colors = RadioButtonDefaults.colors(
                        selectedColor = Color.Red, // Color cuando está seleccionado
                        unselectedColor = Color.Gray // Color cuando no está seleccionado
                    )
                )
                Text(
                    text = opcion,
                    modifier = Modifier.clickable { selectedOption = opcion }
                )
            }
        }
    }
}
```

En este ejemplo, el color cambia a rojo cuando está seleccionado y a gris cuando no lo está.
