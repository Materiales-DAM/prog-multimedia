---
cover: ../../.gitbook/assets/firestores.png
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

# Firestore

Firestore es una base de datos NoSQL en tiempo real de Firebase que organiza datos en colecciones y documentos. Puedes trabajar con objetos en Kotlin utilizando **data classes**, que proporcionan una forma estructurada y tipada de manejar datos.

## Modelo de datos de Firestore

Cloud Firestore es una base de datos **NoSQL orientada a documentos**. A diferencia de una base de datos SQL, no hay tablas ni filas. En su lugar, almacenas los datos en _documentos_, que se organizan en _colecciones_.

Cada _documento_ contiene un conjunto de pares clave-valor. Cloud Firestore está optimizado para almacenar grandes colecciones de documentos pequeños.

Todos los documentos se deben almacenar en colecciones, y pueden contener _subcolecciones_ y objetos anidados. Además, ambos pueden incluir campos primitivos, como strings, o tipos de objetos complejos, como listas.

Las colecciones y los documentos se crean de manera implícita en Cloud Firestore. solo debes asignar datos a un documento dentro de una colección. Si la colección o el documento no existen, Cloud Firestore los crea.

### Documentos

La unidad de almacenamiento es el documento. Un documento es un registro liviano que contiene campos con valores asignados. Cada documento se identifica con un nombre.

Un documento que representa a un usuario `userId1` puede tener el siguiente aspecto:

```
userId1 (documento)
  └─ name: "Bob Esponja"
  └─ age: 30
  └─ active: true
```

Tal vez te parezca que los documentos son muy similares a JSON; de hecho, básicamente son **JSON**. Existen algunas diferencias (por ejemplo, los documentos admiten tipos de datos adicionales y su tamaño se limita a 1 MB), pero en general, puedes tratar los documentos como registros JSON livianos.

### **Colecciones**

Los documentos viven en colecciones, que simplemente son contenedores de documentos.&#x20;

Por ejemplo, podrías tener una colección llamada `users` con los distintos usuarios de tu app, en la que haya un documento que represente a cada uno:

```plaintext
users (colección)
  └─ userId1 (documento)
    └─ name: "Bob Esponja"
    └─ age: 30
    └─ active: true
  └─ userId2 (documento) 
    └─ name: "Peppa Pig"
    └─ age: 24
    └─ active: true
```

Características de las colecciones:

* **No hay un esquema fijo**, por lo que tienes libertad total sobre los campos que pones en cada documento y los tipos de datos que almacenas en esos campos. Los documentos dentro de una misma colección pueden contener campos diferentes o almacenar distintos tipos de datos en esos campos. Sin embargo, se recomienda usar los mismos campos y tipos de datos en varios documentos, de manera que puedas consultarlos con mayor facilidad.
* Una colección contiene solo documentos.
* El nombre (o identificador) de un documento es único  dentro de una colección.
* No es necesario crear o eliminar colecciones manualmente, estas se crean al insertar el primer documento.

### Referencias

Cada documento en Cloud Firestore se identifica de forma única por su ubicación dentro de la base de datos. El ejemplo anterior mostraba un documento `userId1` dentro de la colección `users` . Para hacer referencia a esta ubicación en su código, puede crear una _referencia_ a ella.

<pre class="language-kotlin"><code class="lang-kotlin"><strong>// De esto forma obtenemos la referencia al documento userId1 en la colección users
</strong><strong>val userId1DocumentRef = firestore.collection("users").document("userId1")
</strong></code></pre>

Una referencia es un objeto liviano que simplemente apunta a una ubicación en su base de datos. Puede crear una referencia independientemente de que existan datos allí o no, y la creación de una referencia no realiza ninguna operación de red.

### Datos jerárquicos (subcolecciones)

Una **subcolección** es una colección que está anidada dentro de un documento. Este modelo jerárquico permite estructurar datos relacionados de forma lógica.

**Características:**

* Una subcolección es independiente de su colección padre, y define su es una estructura completamente diferente.
* No existe un límite directo en el número de niveles de subcolecciones que puedes anidar.
* Los documentos de la subcolección tienen IDs únicos dentro de esa subcolección, pero no necesitan coincidir con el ID del documento padre.

Por ejemplo, supongamos que queremos almacenar los pedidos de un usuario específico como una subcolección de su documento:

```plaintext
users (colección)
  └─ userId1 (documento)
       └─ name: "Bob Esponja"
       └─ orders (subcolección)
            └─ orderId1 (documento)
                └─ product: "Laptop"
                └─ price: 1500
            └─ orderId2 (documento)
                └─ product: "Phone"
                └─ price: 800
```

## Reglas de seguridad

Asegúrate de que las reglas de Firestore permitan operaciones adecuadas según tu caso de uso. Por ejemplo:

```json
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null;
    }
  }
}
```
