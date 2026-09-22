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

# Otros modificadores

## Transformaciones

### **Rotación**

Rota el componente en los grados especificados.

```kotlin
Modifier.rotate(45f) // Rota el componente 45 grados
```

### **Escalado**

Escala (cambia el tamaño) el componente en los ejes X e Y.

```kotlin
Modifier.scale(1.5f) // Escala el componente un 50% más grande
```

### **Transparencia / opacidad**

Controla la opacidad del componente.

```kotlin
Modifier.alpha(0.5f) // 50% de opacidad
```

## **Animación**

### **Animación del cambio de tamaño**

Anima el cambio de tamaño del componente suavemente.

```kotlin
Modifier.animateContentSize() // Cambios de tamaño con animación suave
```

## **Scroll**

Permiten que el componente sea desplazable vertical u horizontalmente.

```kotlin
Modifier
    .verticalScroll(rememberScrollState()) // Habilita desplazamiento vertical
    .horizontalScroll(rememberScrollState()) // Habilita desplazamiento vertical
```
