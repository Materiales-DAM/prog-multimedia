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

# TextField

`TextField` es el componente de Jetpack Compose que permite a los usuarios ingresar y editar texto. El uso básico de `TextField` requiere de un estado para almacenar y actualizar el texto.

<figure><img src="../../.gitbook/assets/image (13).png" alt="" width="321"><figcaption><p>Entrada de texto con label</p></figcaption></figure>

```kotlin
@Composable
fun BasicTextField() {
    TextField(
        value = "",
        onValueChange = { // TODO lo implementaremos más adelante },
        label = { Text("Ingresa tu nombre") }
    )
}
```

## **Propiedades comunes de `TextField`**

### **value y onValueChange**

* `value`: Representa el contenido actual del `TextField`.
* `onValueChange`: Se ejecuta cada vez que cambia el texto, y recibe el nuevo valor.

### **label**

La etiqueta es un texto que aparece dentro del campo, indicando al usuario qué debe ingresar.

```kotlin
TextField(
    value = "",
    onValueChange = { // TODO lo implementaremos más adelante  },
    label = { Text("Nombre completo") }
)
```

### **placeholder**

El placeholder es el texto que se muestra mientras el usuario no ha ingresado ningún valor.

```kotlin
TextField(
    value = "",
    onValueChange = { // TODO lo implementaremos más adelante },
    placeholder = { Text("Ejemplo: Juan Pérez") }
)
```

### **maxLines**

Puedes controlar el número máximo de líneas que el usuario puede escribir en un `TextField`.

```kotlin
TextField(
    value = "",
    onValueChange = { // TODO lo implementaremos más adelante },
    label = { Text("Descripción") },
    maxLines = 3  // Limitar a 3 líneas
)
```

### **singleLine**

Si se desea que el `TextField` sea de una sola línea

```kotlin
TextField(
    value = "",
    onValueChange = { // TODO lo implementaremos más adelante },
    label = { Text("Título") },
    singleLine = true
)
```

## TextField m**ultilínea y ajuste de tamaño**

Para permitir un campo multilínea que ajuste su tamaño según el contenido, puedes usar `BasicTextField` o ajustar `TextField` con `maxLines` y `modifier`.

```kotlin
TextField(
    value = text,
    onValueChange = { newText -> text = newText },
    label = { Text("Comentario") },
    modifier = Modifier
        .fillMaxWidth()
        .heightIn(min = 56.dp, max = 200.dp),
    maxLines = 5  // Limitar a 5 líneas
)
```

## **TextField avanzado: BasicTextField**

`BasicTextField` es una versión más personalizable de `TextField`, en la que puedes definir completamente el diseño, aunque requiere más control manual. Aquí tienes un ejemplo:

```kotlin
@Composable
fun CustomBasicTextField() {
    var text by remember { mutableStateOf("Escribe aquí") }

    BasicTextField(
        value = text,
        onValueChange = { newText -> text = newText },
        decorationBox = { innerTextField ->
            Row(
                Modifier
                    .background(Color.LightGray)
                    .padding(16.dp)
                    .fillMaxWidth()
            ) {
                innerTextField()  // Aquí va el contenido editable
            }
        }
    )
}
```
