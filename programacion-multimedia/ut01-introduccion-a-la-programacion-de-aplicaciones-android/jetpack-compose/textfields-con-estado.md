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

# TextFields con estado

En el contexto de los `TextField` vamos a usar los estados para almacenar el texto que vaya introduciendo el usuario. Por tanto, vamos a necesitar declarar un estado por cada `TextField` de nuestra ventana.

```kotlin
@Composable
fun BasicTextField() {
    // Estado para almacenar el texto
    var text by remember { mutableStateOf("") }  
    TextField(
        value = text,
        onValueChange = { newText -> text = newText },
        label = { Text("Ingresa tu nombre") }
    )
}
```

La lambda `onValueChange` es la que se encarga de actualizar el estado `text` a partir de lo que va tecleando el usuario.

## **TextField con contraseña (ocultar texto)**

Para crear un campo de contraseña, usa el modificador `visualTransformation=PasswordVisualTransformation()`.

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

```kotlin
var password by remember { mutableStateOf("")}

TextField(
    value = password,
    onValueChange = { newPassword -> password = newPassword },
    label = { Text("Contraseña") },
    visualTransformation = PasswordVisualTransformation()
)
```

## **TextField con contraseña con opción mostrar/ocultar texto**

Además, es posible configurar un icono al final del TextField que permita que se muestre/oculte la contraseña eque ha introducido el usuario

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption><p>TextField de contraseña</p></figcaption></figure>

```kotlin
var passwordVisible by remember { mutableStateOf(false) }
var password by remember { mutableStateOf("")}

TextField(
    value = password,
    onValueChange = { newPassword -> password = newPassword },
    label = { Text("Contraseña") },
    visualTransformation = if (passwordVisible) VisualTransformation.None else PasswordVisualTransformation(),
    // Permite agregar un ícono para alternar la visibilidad de la contraseña.
    trailingIcon = {
        val image = if (passwordVisible) Icons.Default.Visibility else Icons.Default.VisibilityOff
        IconButton(onClick = { passwordVisible = !passwordVisible }) {
            Icon(imageVector = image, contentDescription = null)
        }
    }
)
```

## TextField numérico

Es posible hacer que un TextField solo acepte números establenciendo un teclado numérico y haciendo que la lambda onValueChange impida que cambie el estado cuando el nuevo texto no es un número

```kotlin
@Composable
fun NumericTextField() {
    var number by remember { mutableStateOf(1) }

    TextField(
        value = number.toString(),
        // Modificamos el teclado del usuario de forma que solo haya números
        keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Number),
        // La lambda se encarga de evitar que meta letras en el campo
        onValueChange = { newText ->
            number = if (newText.isBlank()) 0 else newText.toIntOrNull() ?: number
        })
}
```
