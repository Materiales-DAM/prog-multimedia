---
cover: ../../../.gitbook/assets/jetpack.png
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

# Image

Es el componente más básico de Jetpack Compose para trabajar con imágenes. Para mostrar una imagen, puedes utilizar las imágenes almacenadas en tu carpeta de recursos `drawable`.

```kotlin
@Composable
fun BasicImage() {
    Image(
        painter = painterResource(id = R.drawable.sample_image),
        contentDescription = "Imagen de ejemplo"
    )
}
```

* **painterResource**: Carga una imagen desde los recursos.
* **contentDescription**: Una descripción de la imagen que es útil para accesibilidad (por ejemplo, lectores de pantalla).

### Controlar el Tamaño y Ajuste de la Imagen

Puedes ajustar cómo la imagen se adapta al tamaño que le proporcionas usando el parámetro `contentScale`. Las opciones comunes son:

* `ContentScale.Crop`: Recorta la imagen para llenar el espacio disponible.
* `ContentScale.Fit`: Escala la imagen para que encaje en el espacio, sin recortar.
* `ContentScale.FillBounds`: Deforma la imagen para llenar el espacio disponible.

```kotlin
@Composable
fun ScaledImage() {
    Image(
        painter = painterResource(id = R.drawable.sample_image),
        contentDescription = "Imagen escalada",
        modifier = Modifier
            .width(200.dp)
            .height(200.dp),
        contentScale = ContentScale.Crop // Cambia según tus necesidades
    )
}
```

### Modificadores de imagen

Es posible aplicar modificadores a la imagen, veamos un ejemplo:

```kotlin
@Composable
fun RoundedImage() {
    Image(
        painter = painterResource(id = R.drawable.sample_image),
        contentDescription = "Imagen con esquinas redondeadas",
        modifier = Modifier
            .size(200.dp)
            .clip(RoundedCornerShape(16.dp)) // Redondear las esquinas
            .border(2.dp, Color.Gray) // Agregar un borde
    )
}
```

### Efectos y Filtros

Puedes aplicar varios efectos visuales utilizando los modificadores de Compose, como transparencia, rotación y escalado.

```kotlin
@Composable
fun ImageWithEffects() {
    Image(
        painter = painterResource(id = R.drawable.sample_image),
        contentDescription = "Imagen con efectos",
        modifier = Modifier
            .size(200.dp)
            .graphicsLayer(
                rotationZ = 45f, // Rotación
                alpha = 0.7f     // Transparencia
            )
    )
}
```
