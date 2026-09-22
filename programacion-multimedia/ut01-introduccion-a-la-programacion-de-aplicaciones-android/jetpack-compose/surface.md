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

# Surface

Una `Surface` es un contenedor que te permite personalizar propiedades como el color de fondo, la elevación, la forma, el contenido y más. Se usa principalmente para encapsular componentes visuales y agregarles propiedades decorativas.

```kotlin
Surface(
    modifier = Modifier.fillMaxSize(), // Tamaño o layout que queremos dar
    color = Color.Gray,                // Color de fondo
    shape = RoundedCornerShape(8.dp),  // Forma de la superficie
    elevation = 4.dp                   // Elevación o sombra
) {
    Text("Hola desde Surface")
}
```

Veamos más en detalle las propiedades de la `Surface`:

* **Modifier**: Permite modificar el layout, por ejemplo, añadir `padding` o `size`.
* **Color**: El color de fondo de la superficie.
* **Shape**: Define la forma de la `Surface`. Puedes usar `RoundedCornerShape` para bordes redondeados.
* **Elevation**: Define la altura visual de la `Surface`, añadiendo sombra.

## `Surface` que ocupe toda la actividad

Puedes usar `Surface` como contendor de toda la actividad

```kotlin
class SurfaceActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            // El tema 
            MyAppTheme {
                SurfacePrincipal()
            }
        }
    }
}

@Composable
fun SurfacePrincipal() {
    Surface(modifier = Modifier
        .fillMaxSize()
        .statusBarsPadding() // Este padding hace que los componentes no se superpongan  a las barras de estado
        ) {
            // Aquí cargamos los conteidos
        }
}
```

## `Surface` con Imagen y Forma

Puedes usar `Surface` para añadir una imagen con bordes redondeados o con formas personalizadas.

```kotlin
@Composable
fun SurfaceConImagen() {
    Surface(
        modifier = Modifier.size(150.dp),   // Tamaño de la Surface
        shape = CircleShape,                // Forma circular
        elevation = 4.dp                    // Elevación para la sombra
    ) {
        Image(
            painter = painterResource(id = R.drawable.tu_imagen), // Reemplazar con tu imagen
            contentDescription = "Imagen dentro de Surface",
            contentScale = ContentScale.Crop                       // Recortar para que encaje en el círculo
        )
    }
}
```
