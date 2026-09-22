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

# Button

<figure><img src="../../.gitbook/assets/image (16).png" alt="" width="371"><figcaption></figcaption></figure>

El componente `Button` en Jetpack Compose se utiliza para crear botones interactivos. La estructura básica de un botón es muy sencilla:

```kotlin
@Composable
fun BasicButton() {
    Button(onClick = { /* Acción al hacer clic */ }) {
        Text("Presióname")
    }
}
```

## **Propiedades principales de `Button`**

### **onClick**

El parámetro `onClick` es una lambda que se ejecuta cuando se hace clic en el botón. Aquí puedes manejar la lógica o la acción que deseas ejecutar cuando el usuario interactúa con el botón.

```kotlin
Button(onClick = { println("Botón presionado") }) {
    Text("Click aquí")
}
```

## **Personalización de colores y formas**

Puedes personalizar los colores y las formas del botón utilizando los parámetros `colors` y `shape`.

### **Colores**

Puedes definir los colores para diferentes estados del botón, como `backgroundColor`, `contentColor` (color del texto), `disabledBackgroundColor`, etc.

```kotlin
@Composable
fun CustomColorButton() {
    Button(
        onClick = { /* Acción */ },
        colors = ButtonColors(
            containerColor = Color.Green,
            contentColor = Color.White,
            disabledContentColor = Color.Gray,
            disabledContainerColor = Color.Black
        )
    ) {
        Text("Botón Verde")
    }
}
```

### **Forma**

Puedes cambiar la forma del botón aplicando un valor a la propiedad `shape`. Por ejemplo, hacer el botón redondeado.

```kotlin
@Composable
fun RoundedButton() {
    Button(
        onClick = { /* Acción */ },
        shape = RoundedCornerShape(50)  // Bordes redondeados
    ) {
        Text("Botón Redondeado")
    }
}
```

### **Iconos**

Puedes agregar íconos antes o después del texto dentro del botón utilizando composables como `Icon`. Jetpack Compose proporciona un conjunto de íconos predeterminados que puedes usar.

```kotlin
@Composable
fun IconButtonExample() {
    Button(onClick = { /* Acción */ }) {
        Icon(Icons.Default.Favorite, contentDescription = null)
        Spacer(modifier = Modifier.width(8.dp))  // Espacio entre el ícono y el texto
        Text("Favorito")
    }
}
```

### Habilitar / deshabilitar

Puedes deshabilitar el botón configurando el parámetro `enabled` en `false`.

```kotlin
@Composable
fun DisabledButton() {
    Button(onClick = { /* Acción */ }, enabled = false) {
        Text("Botón deshabilitado")
    }
}
```

## **Estilos de botones**

Jetpack Compose incluye diferentes estilos de botones, como `Button`, `OutlinedButton`, y `TextButton`. A continuación, exploraremos cada uno de ellos.

### **Button (Botón con fondo elevado)**

Este es el estilo predeterminado de los botones, con un fondo sólido y un efecto elevado.

```kotlin
@Composable
fun ElevatedButton() {
    Button(onClick = { /* Acción */ }) {
        Text("Botón Elevado")
    }
}
```

### **OutlinedButton (Botón con borde)**

El `OutlinedButton` muestra solo el contorno del botón, sin fondo.

```kotlin
@Composable
fun OutlinedButtonExample() {
    OutlinedButton(onClick = { /* Acción */ }) {
        Text("Botón con borde")
    }
}
```

### **TextButton (Botón de solo texto)**

El `TextButton` es un botón de texto plano, sin fondo ni borde visible.

```kotlin
@Composable
fun TextButtonExample() {
    TextButton(onClick = { /* Acción */ }) {
        Text("Botón de solo texto")
    }
}
```
