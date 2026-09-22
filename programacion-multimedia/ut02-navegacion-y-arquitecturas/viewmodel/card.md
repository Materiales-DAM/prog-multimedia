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

# Card

El componente `Card` es una estructura contenedora que permite mostrar elementos visuales con un estilo destacado. Es una forma común de organizar contenido en aplicaciones, ofreciendo un aspecto profesional y fácil de usar. En este tutorial, exploraremos cómo usar el componente `Card` para crear interfaces atractivas.

<figure><img src="../../.gitbook/assets/image (18).png" alt="" width="328"><figcaption></figcaption></figure>

El componente `Card` se puede usar para contener texto, imágenes y otros componentes de la UI. Puedes ajustar el estilo, el contenido y la interacción.

```kotlin
@Composable
fun SimpleCard() {
    Card(
        modifier = Modifier.padding(16.dp),
        elevation = CardDefaults.cardElevation(defaultElevation = 4.dp) // Elevación que da un efecto de sombra
    ) {
        Text(
            text = "Contenido dentro de una Card",
            modifier = Modifier.padding(16.dp)
        )
    }
}
```

* **modifier**: Permite modificar el diseño de la `Card`, como agregar padding.
* **elevation**: Define la sombra de la tarjeta, dando una sensación de profundidad.

## Bordes y forma

El parámetro `shape` en la tarjeta permite ajustar las esquinas redondeadas o incluso hacer la tarjeta completamente circular.

```kotlin
@Composable
fun RoundedCard() {
    Card(
        shape = RoundedCornerShape(16.dp), // Define las esquinas redondeadas
        modifier = Modifier.padding(16.dp),
        elevation = CardDefaults.cardElevation(defaultElevation = 8.dp)
    ) {
        Text(
            text = "Card con esquinas redondeadas",
            modifier = Modifier.padding(16.dp)
        )
    }
}
```

Ejemplo de Card cirular

```kotlin
@Composable
fun CircularCard() {
    Card(
        shape = CircleShape, // Hace la tarjeta completamente circular
        modifier = Modifier.size(100.dp),
        elevation = CardDefaults.cardElevation(defaultElevation = 4.dp)
    ) {
        Text(
            text = "Circular Card",
            modifier = Modifier.padding(16.dp),
            textAlign = TextAlign.Center
        )
    }
}
```

## Dentro de una Card

Puedes combinar imágenes y texto dentro de una `Card` para crear una UI más rica.

```kotlin
@Preview
@Composable
fun ImageCard() {
    Card(
        shape = RoundedCornerShape(8.dp),
        modifier = Modifier
            .padding(16.dp)
            .fillMaxWidth(),
        elevation = CardDefaults.cardElevation(defaultElevation = 8.dp)
    ) {
        Column(
            modifier = Modifier.padding(16.dp)
        ) {
            Image(
                painter = painterResource(id = R.drawable.ic_launcher_background),
                contentDescription = "Imagen dentro de una Card",
                modifier = Modifier
                    .height(150.dp)
                    .fillMaxWidth(),
                contentScale = ContentScale.Crop
            )
            Spacer(modifier = Modifier.height(8.dp))
            Text(
                text = "Este es el título de la Card", 
                style = MaterialTheme.typography.headlineSmall
            )
            Text(
                text = "Descripción de la imagen mostrada en la Card.", 
                style = MaterialTheme.typography.bodyMedium
            )
        }
    }
}
```

<figure><img src="../../.gitbook/assets/image (20).png" alt="" width="279"><figcaption></figcaption></figure>

* Se utiliza una `Column` dentro de la `Card` para colocar la imagen y el texto verticalmente.
* `Spacer` añade un espacio entre los elementos.
* `painterResource` carga una imagen desde los recursos.

## Efectos visuales

Usando `Modifier.graphicsLayer`, puedes aplicar efectos visuales como rotación, escala o transparencia a la `Card`.

<pre class="language-kotlin"><code class="lang-kotlin">@Composable
fun ImageCard() {
    Card(
        shape = RoundedCornerShape(8.dp),
        modifier = Modifier
            .padding(16.dp)
            .fillMaxWidth()
            .graphicsLayer {
                rotationZ = 15f
                // rotationX / rotationY for 3D effects
<strong>            },
</strong>        elevation = CardDefaults.cardElevation(defaultElevation = 8.dp)
    ) {
        Column(
            modifier = Modifier.padding(16.dp)
        ) {
            Image(
                painter = painterResource(id = R.drawable.sample_image),
                contentDescription = "Imagen dentro de una Card",
                modifier = Modifier
                    .height(150.dp)
                    .fillMaxWidth(),
                contentScale = ContentScale.Crop
            )
            Spacer(modifier = Modifier.height(8.dp))
            Text(
                text = "Este es el título de la Card", 
                style = MaterialTheme.typography.headlineSmall
            )
            Text(
                text = "Descripción de la imagen mostrada en la Card.", 
                style = MaterialTheme.typography.bodyMedium
            )
        }
    }
}
</code></pre>

<figure><img src="../../.gitbook/assets/image (19).png" alt="" width="181"><figcaption><p>Card con rotación</p></figcaption></figure>
