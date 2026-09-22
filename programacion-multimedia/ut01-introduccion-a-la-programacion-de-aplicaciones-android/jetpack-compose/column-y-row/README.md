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

# Column y Row

En Jetpack Compose, los componentes **`Row`** y **`Column`** son contenedores que permiten organizar otros elementos en una disposición horizontal (fila) o vertical (columna). Estos contenedores nos permiten construir layouts más complejos al apilar o alinear múltiples elementos.

## **Column**

El componente `Column` organiza los elementos hijos verticalmente, es decir, uno debajo del otro. Por ejemplo, si queremos mostrar tres textos uno debajo del otro:

```kotlin
@Composable
fun MyColumnExample() {
    Column {
        Text(text = "Elemento 1")
        Text(text = "Elemento 2")
        Text(text = "Elemento 3")
    }
}
```

### **Parámetros**

* **modifier**: Permite aplicar modificaciones como tamaño, padding, o bordes a la columna.
* **verticalArrangement**: Define cómo se distribuyen los elementos a lo largo del eje vertical.
* **horizontalAlignment**: Alinea todos los elementos hijos a lo largo del eje horizontal.

```kotlin
@Composable
fun MyColumnExample() {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.SpaceAround,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(text = "Elemento 1")
        Text(text = "Elemento 2")
        Text(text = "Elemento 3")
    }
}
```

En este ejemplo:

* **`modifier.fillMaxSize()`**: Hace que la columna ocupe todo el espacio disponible.
* **`verticalArrangement = Arrangement.SpaceAround`**: Distribuye los elementos verticalmente con un espacio similar antes, entre y después de los elementos.
* **`horizontalAlignment = Alignment.CenterHorizontally`**: Alinea los elementos al centro horizontal de la columna.

## **Row**

El componente `Row` organiza los elementos hijos horizontalmente, es decir, uno al lado del otro.

```kotlin
@Composable
fun MyRowExample() {
    Row {
        Text(text = "Elemento 1")
        Text(text = "Elemento 2")
        Text(text = "Elemento 3")
    }
}
```

En este ejemplo, los tres textos se colocan uno al lado del otro en una fila.

### **Parámetros**

* **modifier**: Similar a `Column`, permite aplicar modificaciones al `Row`.
* **horizontalArrangement**: Controla cómo se distribuyen los elementos a lo largo del eje horizontal.
* **verticalAlignment**: Alinea los elementos hijos a lo largo del eje vertical.

Ejemplo con más control sobre la alineación y el espaciado:

```kotlin
@Composable
fun MyRowExample() {
    Row(
        modifier = Modifier.fillMaxWidth(),
        horizontalArrangement = Arrangement.SpaceBetween,
        verticalAlignment = Alignment.CenterVertically
    ) {
        Text(text = "Elemento 1")
        Text(text = "Elemento 2")
        Text(text = "Elemento 3")
    }
}
```

En este ejemplo:

* **`modifier.fillMaxWidth()`**: Hace que la fila ocupe todo el ancho disponible.
* **`horizontalArrangement = Arrangement.SpaceBetween`**: Coloca los elementos distribuidos equitativamente con el mismo espacio entre ellos.
* **`verticalAlignment = Alignment.CenterVertically`**: Alinea los elementos al centro vertical de la fila.

## **Combinando Row y Column**

Puedes combinar `Row` y `Column` para crear layouts más complejos. Aquí tienes un ejemplo donde combinamos una columna con una fila dentro:

```kotlin
@Composable
fun MyComplexLayout() {
    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.SpaceAround,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(text = "Este es un título")

        Row(
            modifier = Modifier.fillMaxWidth(),
            horizontalArrangement = Arrangement.SpaceEvenly
        ) {
            Text(text = "Elemento 1")
            Text(text = "Elemento 2")
            Text(text = "Elemento 3")
        }

        Text(text = "Este es un pie de página")
    }
}
```

## Valores de Arrangements

**Arrangements (`verticalArrangement` / `horizontalArrangement`)**: Controlan cómo se distribuyen los elementos dentro de la fila o columna. Algunos valores comunes son:

* **`Arrangement.Start`**: Alinea los elementos al inicio.
* **`Arrangement.End`**: Alinea los elementos al final.
* **`Arrangement.SpaceBetween`**: Distribuye los elementos equitativamente, dejando el mayor espacio entre los elementos.
* **`Arrangement.SpaceEvenly`**: Coloca los elementos con espacios iguales entre sí y los bordes.
* **`Arrangement.SpaceAround`**: Similar a `SpaceEvenly`, pero con algo de espacio antes del primer elemento y después del último.

## **Valores de Alignments**

**Alignments (`horizontalAlignment` / `verticalAlignment`)**: Definen cómo se alinean los elementos dentro de la fila o columna en el eje opuesto al que se distribuyen.

* **`Alignment.Top`**: Alinea los elementos al borde superior.
* **`Alignment.Bottom`**: Alinea los elementos al borde inferior.
* **`Alignment.CenterHorizontally`**: Alinea los elementos al centro horizontal.
* **`Alignment.CenterVertically`**: Alinea los elementos al centro vertical.
