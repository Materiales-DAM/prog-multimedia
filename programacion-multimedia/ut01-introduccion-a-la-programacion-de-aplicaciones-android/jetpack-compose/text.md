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

# Text

El componente `Text` se utiliza para mostrar texto en la pantalla. Su uso más simple es pasarle un texto como argumento:

```kotlin
@Composable
fun SimpleText() {
    Text(text = "Hola, Jetpack Compose!")
}

```

## **Estilizar texto: `TextStyle` y sus propiedades**

El componente `Text` permite aplicar diferentes estilos como tamaño de fuente, color, peso de la fuente, etc., a través de `TextStyle`.

### **Cambiar tamaño de fuente**

Puedes cambiar el tamaño de la fuente usando `fontSize`.

```kotlin
@Composable
fun LargeText() {
    Text(
        text = "Texto grande",
        fontSize = 24.sp
    )
}
```

### **Color de texto**

Para cambiar el color del texto, usa el parámetro `color`.

```kotlin
@Composable
fun ColoredText() {
    Text(
        text = "Texto en rojo",
        color = Color.Red
    )
}
```

### **Fuente en negrita**

Puedes hacer el texto en negrita usando `fontWeight`.

```kotlin
@Composable
fun BoldText() {
    Text(
        text = "Texto en negrita",
        fontWeight = FontWeight.Bold
    )
}
```

### **Aplicar múltiples estilos a la vez**

Es posible combinar varios estilos usando `TextStyle`.

```kotlin
@Composable
fun StyledText() {
    Text(
        text = "Texto estilizado",
        style = TextStyle(
            color = Color.Blue,
            fontSize = 20.sp,
            fontWeight = FontWeight.SemiBold
        )
    )
}
```

### **Alineación del texto**

Puedes alinear el texto dentro del componente con el modificador `textAlign`.

```kotlin
@Composable
fun CenteredText() {
    Text(
        text = "Texto centrado",
        textAlign = TextAlign.Center,
        modifier = Modifier.fillMaxWidth()  // Necesitas esto para que se centre en el espacio disponible
    )
}
```

### **Decoraciones del texto**

También puedes aplicar decoraciones como subrayado o tachado con el modificador `textDecoration`.

```kotlin
@Composable
fun UnderlinedText() {
    Text(
        text = "Texto subrayado",
        style = TextStyle(
            textDecoration = TextDecoration.Underline
        )
    )
}

@Composable
fun StrikethroughText() {
    Text(
        text = "Texto tachado",
        style = TextStyle(
            textDecoration = TextDecoration.LineThrough
        )
    )
}
```

### **LineHeight y Multilínea**

Puedes ajustar la altura de las líneas para texto multilínea con `lineHeight`.

```kotlin
@Composable
fun MultilineText() {
    Text(
        text = "Esto es un texto\nque ocupa varias líneas.",
        lineHeight = 24.sp
    )
}
```

### **Ajustar overflow del texto**

El texto que es demasiado largo para el área asignada puede manejarse con `overflow` y `maxLines`.

```kotlin
@Composable
fun OverflowText() {
    Text(
        text = "Este es un texto muy largo que no cabe en una sola línea y se truncará.",
        maxLines = 1,
        overflow = TextOverflow.Ellipsis
    )
}
```
