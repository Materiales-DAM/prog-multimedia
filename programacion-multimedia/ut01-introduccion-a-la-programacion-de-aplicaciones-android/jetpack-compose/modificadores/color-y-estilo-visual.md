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

# Color y estilo visual

## **Color de fondo**

Establece un color de fondo para un componente.

```kotlin
Modifier.background(Color.Red) // Fondo rojo
```

## **Borde**

Añade un borde alrededor del componente.

```kotlin
Modifier.border(2.dp, Color.Black) // Borde negro de 2 dp de ancho
```

## **Recortado**

Recorta el contenido de un componente según una forma especificada (por ejemplo, círculo, rectángulo redondeado).

```kotlin
Modifier.clip(RoundedCornerShape(8.dp)) // Recorta con esquinas redondeadas de 8 dp
```

## **Sombra**

Añade una sombra detrás del componente.

```kotlin
Modifier.shadow(elevation = 8.dp) // Sombra con una elevación de 8 dp
```
