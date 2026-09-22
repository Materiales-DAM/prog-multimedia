---
cover: ../../../../.gitbook/assets/jetpack.png
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

# Tamaño y dimensiones

## Tamaño

Establece tanto el ancho como la altura de un componente.

```kotlin
Modifier.size(100.dp) // Tamaño de 100 dp por lado (cuadrado)
```

## **Anchura y altura**

Establecen el ancho y la altura de un componente de forma independiente.

```kotlin
Modifier.width(150.dp) // Ancho de 150 dp
Modifier.height(50.dp) // Altura de 50 dp
```

## Expandir tamaño

### **Ocupar todo el ancho**

Ocupan el 100% del ancho disponible.

```kotlin
Modifier.fillMaxWidth() // Ocupar todo el ancho disponible
```

### **Ocupar todo el alto**

Ocupan el 100% de la altura disponible.

```kotlin
Modifier.fillMaxHeight() // Ocupar toda la altura disponible
```

### **Ocupar todo la anchura y altura**

Ocupa el 100% tanto del ancho como de la altura disponibles.

```kotlin
Modifier.fillMaxSize() // Ocupar todo el espacio disponible
```

### **Ocupar solo ancho necesario**

Hace que el componente se ajuste al tamaño de su contenido, sin ocupar más ancho del necesario.

```kotlin
Modifier.wrapContentWidth() // Ancho ajustado al contenido
```

### **Ocupar solo altura necesaria**

Hace que el componente se ajuste al tamaño de su contenido, sin ocupar más altura del necesario.

```kotlin
Modifier.wrapContentHeight() // Altura ajustada al contenido
```

### **Aspect ratio**

Establece una proporción matemática entre el ancho y el alto de un componente.&#x20;

Por ejemplo:

* Un **aspect ratio de 1:1** significa que el componente será cuadrado (ancho igual a alto).
* Un **aspect ratio de 16:9** es la proporción común para videos widescreen (pantalla ancha).
* Un **aspect ratio de 4:3** es común en formatos de fotografía.

```kotlin
Modifier.aspectRatio(1f) // Mantiene una proporción 1:1 (cuadrado)
```
