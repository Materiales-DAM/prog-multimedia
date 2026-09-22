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

# Alineación y Posicionamiento

## Alineación

Alinea un componente dentro de su padre (solo para `Column` o `Row`).

```kotlin
Modifier.align(Alignment.CenterHorizontally) // Alineado horizontal en el centro
```

## **Desplazamiento**

Desplaza el componente de su posición original en los ejes X y/o Y.

```kotlin
Modifier.offset(x = 10.dp, y = 20.dp) // Desplaza 10 dp en X y 20 dp en Y
```

## Profundidad

Controla el orden en el eje Z (profundidad), permitiendo que un componente se renderice por encima o por debajo de otros.

```kotlin
Modifier.zIndex(1f) // Coloca el componente por encima de otros con un índice menor
```
