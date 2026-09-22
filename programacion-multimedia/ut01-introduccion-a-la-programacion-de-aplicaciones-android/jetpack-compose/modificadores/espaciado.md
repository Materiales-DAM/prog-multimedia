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

# Espaciado

## **Padding**

El padding es el espacio entre el contenido de un elemento y su borde. Empuja el contenido hacia adentro, alejándolo de los bordes del elemento.

Para configurar el padding usaremos el modifier `padding` después del resto de modificadores. Por ejemplo

```kotlin
Modifier
        .fillMaxSize()
        .background(MaterialTheme.colorScheme.primaryContainer)
        .padding(16.dp)
```

## Margin

El margin es el espacio fuera del borde del elemento. Crea espacio entre el elemento y los elementos adyacentes.

Para configurar el margin también usaremos el modifier `padding`, pero esta vez lo haremos antes del resto de modificadores. Por ejemplo:

```kotlin
Modifier
        .padding(16.dp)
        .fillMaxSize()
        .background(MaterialTheme.colorScheme.primaryContainer)
```

## Padding y margin

Es posible combinar padding y margin de manera sencilla

```kotlin
Modifier
        .padding(16.dp)
        .fillMaxSize()
        .background(MaterialTheme.colorScheme.primaryContainer)
        .padding(16.dp)
```
