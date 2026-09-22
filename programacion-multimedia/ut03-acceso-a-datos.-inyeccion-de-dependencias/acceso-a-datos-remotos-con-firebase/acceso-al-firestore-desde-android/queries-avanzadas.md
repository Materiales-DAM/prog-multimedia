---
cover: ../../../.gitbook/assets/firestores.png
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

# Queries avanzadas

Firestore soporta varias operaciones avanzadas como filtros múltiples, ordenamiento, paginación y operaciones en arrays. Veamos cómo implementarlas.

## **Consulta Básica**

```kotlin
firestore.collection("users")
    .whereEqualTo("age", 25)
    .get()
    .addOnSuccessListener { documents ->
        for (document in documents) {
            Log.d("Firestore", "${document.id} => ${document.data}")
        }
    }
    .addOnFailureListener { e ->
        Log.e("Firestore", "Error fetching documents", e)
    }
```

## **Filtros Múltiples**

Es posible combinar varios filtros en una consulta usando `where`:

```kotlin
firestore.collection("users")
    .whereEqualTo("country", "USA")
    .whereGreaterThan("age", 18)
    .get()
    .addOnSuccessListener { documents ->
        for (document in documents) {
            Log.d("Firestore", "${document.id} => ${document.data}")
        }
    }
```

**Nota**: Todos los filtros deben cumplir las restricciones de índices compuestos en Firestore.

## **Ordenar Resultados**

Usa `orderBy` para ordenar los datos por un campo:

```kotlin
firestore.collection("users")
    .orderBy("age", Query.Direction.DESCENDING)
    .get()
    .addOnSuccessListener { documents ->
        for (document in documents) {
            Log.d("Firestore", "${document.id} => ${document.data}")
        }
    }
```

## **Paginación**

La paginación permite manejar grandes conjuntos de datos:

```kotlin
var lastVisibleDocument: DocumentSnapshot? = null

fun fetchFirstPage() {
    firestore.collection("users")
        .orderBy("age")
        .limit(10)
        .get()
        .addOnSuccessListener { documents ->
            if (documents.size() > 0) {
                lastVisibleDocument = documents.documents.last()
                for (document in documents) {
                    Log.d("Firestore", "${document.id} => ${document.data}")
                }
            }
        }
}

fun fetchNextPage() {
    lastVisibleDocument?.let {
        firestore.collection("users")
            .orderBy("age")
            .startAfter(it)
            .limit(10)
            .get()
            .addOnSuccessListener { documents ->
                if (documents.size() > 0) {
                    lastVisibleDocument = documents.documents.last()
                    for (document in documents) {
                        Log.d("Firestore", "${document.id} => ${document.data}")
                    }
                }
            }
    }
}
```

## **Operaciones con Arrays**

Firestore permite consultar elementos en arrays con:

* **`array-contains`**: Para buscar un valor específico.
* **`array-contains-any`**: Para buscar valores dentro de un conjunto.

Ejemplo:

```kotlin
firestore.collection("posts")
    .whereArrayContains("tags", "kotlin")
    .get()
    .addOnSuccessListener { documents ->
        for (document in documents) {
            Log.d("Firestore", "${document.id} => ${document.data}")
        }
    }
```

```kotlin
firestore.collection("posts")
    .whereArrayContainsAny("tags", listOf("kotlin", "firebase"))
    .get()
    .addOnSuccessListener { documents ->
        for (document in documents) {
            Log.d("Firestore", "${document.id} => ${document.data}")
        }
    }
```

## **Combinar Filtros y Orden**

Cuando usas múltiples filtros con `orderBy`, asegúrate de que todos los campos estén indexados:

```kotlin
firestore.collection("products")
    .whereGreaterThanOrEqualTo("price", 10)
    .orderBy("price", Query.Direction.ASCENDING)
    .get()
    .addOnSuccessListener { documents ->
        for (document in documents) {
            Log.d("Firestore", "${document.id} => ${document.data}")
        }
    }
```

## Optimización de Queries

1. **Usa índices compuestos**: En el panel de Firebase, agrega índices para consultas complejas.
2. **Evita consultas que descarguen muchos documentos**: Usa límites con `.limit(n)`.
3.  **Minimiza los campos devueltos**: Usa `.select()` para seleccionar solo los campos necesarios:

    ```kotlin
    firestore.collection("users")
        .select("name", "age")
        .get()
    ```
