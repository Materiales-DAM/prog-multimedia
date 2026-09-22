---
cover: ../../../../.gitbook/assets/image (5).png
coverY: -187.27466666666663
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

# Implementación Repositories

Como ya habréis estudiado en Acceso a datos, el patrón Repository es ideal para abstraer el acceso a Firestore y proporcionar una interfaz limpia para interactuar con los datos. Para implementar un Repository que se conecte a Firestore seguiremos los siguientes pasos:

## **1. Crear la data class**

Define una `data class` para representar la estructura de los documentos en Firestore. Estas clases deben contar con un constructor sin parámetros para que funcione la deserialización.&#x20;

```kotlin
import com.google.firebase.firestore.DocumentId
import com.google.firebase.firestore.PropertyName
import com.google.firebase.firestore.ServerTimestamp
import java.util.Date

data class User(
    @DocumentId val id: String = "",
    @PropertyName("user_name") val name: String,
    val email: String,
    val age: Int,
    @ServerTimestamp val createdAt: Date? = null // Fecha generada automáticamente
) {
    // Constructor vacío necesario para la deserialización
    constructor() : this(name = "", email = "", age = 0)
}
```

#### Las anotaciones que se pueden usar son:

### **@DocumentId**

La anotación `@DocumentId` se utiliza para mapear el ID del documento Firestore (que no es un campo del documento) a una propiedad en tu clase de datos.

### **@PropertyName**

La anotación `@PropertyName` se utiliza para mapear un nombre de campo en Firestore a una propiedad de tu clase que tiene un nombre diferente.

Esta anotación es útil si necesitas que los nombres en tu clase sean diferentes de los nombres en la base de datos.

### **@ServerTimestamp**

La anotación `@ServerTimestamp` se utiliza para que Firestore asigne automáticamente una marca de tiempo del servidor (`Timestamp`) al campo. Si el campo está configurado con esta anotación, Firestore asignará un valor de marca de tiempo cuando se cree o actualice el documento. Es útil para rastrear cuándo se creó o actualizó un documento sin tener que hacerlo manualmente.

### **@Exclude**

La anotación `@Exclude` se utiliza para evitar que una propiedad específica de tu clase sea almacenada o leída desde Firestore.

```kotlin
import com.google.firebase.firestore.Exclude

// Esta data class nos permite almacenar los intentos de login que ha habido en el sistema
data class LoginAttempt(
    val name: String = "",
    val email: String = "",
    // Excluimos el password para que no quede almacenado en la base de datos
    @Exclude val password: String = "" // Esta propiedad no se almacena en Firestore
)
```

Sirve para evitar almacenar datos sensibles (como contraseñas) y para propiedades temporales o calculadas que no deben ser parte del documento en Firestore.

## **2. Crear el Repositorio**

Creamos una implementación del repositorio basada en Firestore. Se debe crear en el paquete `data.repository`

```kotlin
import com.google.firebase.firestore.FirebaseFirestore
import com.google.firebase.firestore.Query
import kotlinx.coroutines.channels.awaitClose
import kotlinx.coroutines.flow.Flow
import kotlinx.coroutines.flow.callbackFlow
import kotlinx.coroutines.tasks.await

class UserFirestoreRepository(val firestore: FirebaseFirestore) {

    private val usersCollection = firestore.collection("users")

    // Obtener un usuario por ID
    suspend fun getById(id: String): User? {
        return try {
            val documentSnapshot = usersCollection.document(id).get().await()
            documentSnapshot.toObject(User::class.java)
        } catch (e: Exception) {
            e.printStackTrace()
            null
        }
    }
    
    fun list(): Flow<List<User>> {
        // Esta implementación crea un Flow que actualiza la lista de usuarios
        // cada vez que hay un cambio en la base de datos
        return queryForList(
                usersCollection,
                User::class.java
        )     
    }

    // Agregar un nuevo usuario
    suspend fun save(user: User): Boolean {
        return try {
            usersCollection.add(user).await()
            true
        } catch (e: Exception) {
            e.printStackTrace()
            false
        }
    }
    
    suspend fun update(user: User): Boolean {
        return try {
            usersCollection.document(user.id).update(
                "name", user.name,
                "email", user.email,
                "age", user.age,
            ).await()
            true
        } catch (e: Exception) {
            e.printStackTrace()
            false
        }
    }


    // Eliminar un usuario por ID
    suspend fun delete(id: String): Boolean {
        return try {
            usersCollection.document(id).delete().await()
            true
        } catch (e: Exception) {
            e.printStackTrace()
            false
        }
    }
    
    // Este método es siempre igual para cualquier repository
    private fun <T> queryForList(query: Query, clazz: Class<T>): Flow<List<T>> {
        return callbackFlow {

            val listener = query
                .addSnapshotListener { snapshots, error ->
                    if (error != null) {
                        close(error)
                        return@addSnapshotListener
                    }

                    val items = snapshots?.documents?.mapNotNull { doc ->
                        doc.toObject(clazz)

                    } ?: emptyList()

                    trySend(items)
                }

            awaitClose() { listener.remove() }
        }
    }
    
    // Este método es siempre igual para cualquier repository
    private fun <T> queryForSingle(query: Query, clazz: Class<T>): Flow<T?> {
        return callbackFlow {
            val listener = query
                .addSnapshotListener { snapshots, error ->
                    if (error != null) {
                        close(error)
                        return@addSnapshotListener
                    }

                    val item = snapshots?.documents?.firstOrNull()?.toObject(clazz)

                    trySend(item)
                }
            awaitClose() { listener.remove() }
        }
    }
}
```
