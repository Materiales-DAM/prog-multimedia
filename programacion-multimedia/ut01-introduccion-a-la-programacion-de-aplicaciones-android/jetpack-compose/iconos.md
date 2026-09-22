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

# Iconos

Un icono es un elemento gráfico que representa una acción, estado o sección en la interfaz de usuario. Se utilizan para ayudar al usuario a reconocer rápidamente funciones o categorías. Los iconos pueden ser simples imágenes o gráficos vectoriales que transmiten visualmente el propósito de un botón, enlace, u otro elemento.

<figure><img src="../../.gitbook/assets/image (29).png" alt="" width="375"><figcaption></figcaption></figure>

En Jetpack Compose, los iconos se implementan mediante el componente `Icon`, que permite mostrar tanto los iconos predeterminados de Material Design como iconos personalizados que agregues a tu proyecto.&#x20;

```kotlin
@Composable
fun BasicIconExample() {
    Icon(
        imageVector = Icons.Default.Home, // Icono predeterminado de "Home"
        contentDescription = "Icono de Inicio" // Descripción para accesibilidad
    )
}
```

Vamos a usar la biblioteca de iconos de Material Design de Google, para ello debemos añadir la siguiente línea a la sección `dependencies` en el archivo `build.gradle.kts (Module :app)`

```gradle
implementation("androidx.compose.material:material-icons-extended:1.7.8")
```

## Biblioteca Material Design

Los iconos de Material Design incluyen una amplia colección de imágenes vectoriales estándar (como `Home`, `Favorite`, `Share`, etc.) que están listos para usarse y mantienen una apariencia coherente en la aplicación.

<figure><img src="../../.gitbook/assets/image (30).png" alt="" width="375"><figcaption></figcaption></figure>

Puedes consultar la biblioteca de iconos [aquí](https://fonts.google.com/icons)

## Estilos de iconos

En Material Design, los iconos son fundamentales para comunicar acciones, conceptos y estados de manera visual. Existen diferentes estilos de iconos que se utilizan para mantener la coherencia en la interfaz de usuario. A continuación, te explico los principales estilos de iconos en Material Design:

### **Filled Icons (iconos rellenos)**

Estos iconos tienen una forma sólida y son completamente rellenos, lo que les da un aspecto más prominente. Se utilizan para representar acciones principales y elementos interactivos, como botones o iconos de navegación. Son ideales para destacar acciones importantes.

```kotlin
Icon(imageVector = Icons.Filled.Favorite, contentDescription = "Favorito")
```

### **Outlined Icons (iconos contorneados)**

Estos iconos tienen un contorno delgado y no están rellenos, lo que les da un aspecto más sutil y ligero.

Se utilizan en contextos donde se desea un enfoque más ligero, o cuando se requieren varias opciones visuales similares. Ideal para acciones secundarias o menos prominentes.

```kotlin
Icon(imageVector = Icons.Outlined.Favorite, contentDescription = "Favorito sin relleno")
```

### **Rounded Icons (iconos tedondeados)**

* **Descripción**: Estos iconos presentan esquinas redondeadas, lo que les da un aspecto más amigable y accesible.
* **Uso**: Se utilizan en interfaces donde se busca un estilo más suave o amigable. Se pueden utilizar en aplicaciones con un diseño más moderno y casual.
* **Ejemplo**: Un icono de "Estrella" redondeado.

```kotlin
Icon(imageVector = Icons.Rounded.Star, contentDescription = "Estrella redondeada")
```

### **Sharp Icons (iconos agudos)**

* **Descripción**: Estos iconos tienen bordes afilados y un diseño más geométrico.
* **Uso**: Se utilizan en aplicaciones que requieren un diseño más elegante y moderno. Se pueden usar para representar acciones o estados que requieren claridad y definición.
* **Ejemplo**: Un icono de "Casa" con bordes agudos.

```kotlin
Icon(imageVector = Icons.Sharp.Home, contentDescription = "Casa aguda")
```

### **Two-Tone Icons (iconos bicolor)**

* **Descripción**: Estos iconos utilizan dos colores diferentes para crear un efecto de profundidad y dimensionalidad.
* **Uso**: Se utilizan para agregar interés visual y se pueden aplicar en iconos donde el contraste ayuda a la legibilidad o la identificación.
* **Ejemplo**: Un icono que tiene un contorno de un color y un relleno de otro color.

## IconButton para iconos interactivos

Cuando necesitas que el icono sea clicable, puedes usar `IconButton` o `IconToggleButton`.

```kotlin
@Composable
fun IconButtonExample() {
    IconButton(onClick = { /* Acción cuando se presiona */ }) {
        Icon(
            imageVector = Icons.Default.Share,
            contentDescription = "Icono de Compartir"
        )
    }
}
```

Esto crea un botón con icono que es clicable y usa el icono que especifiques.

## IconToggleButton para estados de icono

Para iconos con dos estados (por ejemplo, "Me gusta" activado/desactivado), usa `IconToggleButton`.

```kotlin
@Composable
fun ToggleIconButtonExample() {
    var isFavorite by remember { mutableStateOf(false) }

    IconToggleButton(
        checked = isFavorite,
        onCheckedChange = { isFavorite = it }
    ) {
        Icon(
            imageVector = if (isFavorite) Icons.Filled.Favorite else Icons.Outlined.FavoriteBorder,
            contentDescription = "Icono de Favorito",
            tint = if (isFavorite) Color.Red else Color.Gray
        )
    }
}
```

Aquí, `IconToggleButton` permite que el icono cambie su estado y apariencia en función del valor `isFavorite`.
