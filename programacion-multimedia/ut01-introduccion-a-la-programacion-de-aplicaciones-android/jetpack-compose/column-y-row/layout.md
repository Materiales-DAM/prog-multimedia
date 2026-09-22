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

# Layout

### **Weight**

Asigna una proporción de espacio a un componente dentro de un `Row` o `Column`, lo que hace que ocupe más o menos espacio en comparación con otros componentes.

```kotlin
Modifier.weight(1f) // Ocupa proporcionalmente más espacio
```

### Ocupar el espacio mínimo necesario

Hace que el componente solo ocupe el espacio necesario según su contenido.

```kotlin
Modifier.wrapContentSize(Alignment.Center) // Centra el contenido ajustado al tamaño mínimo necesario
```

### **Ocupar todo el espacio disponible**

Ocupa todo el espacio disponible .

```kotlin
Modifier.fillMaxSize(0.5f) // Ocupa la mitad del espacio del padre
```
