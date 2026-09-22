---
cover: ../../../../.gitbook/assets/image (5).png
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

# Implementación de los casos de uso de la aplicación

En la **Arquitectura Clean**, un **UseCase** (Caso de Uso) representa una operación o acción específica que la aplicación puede realizar desde la perspectiva del negocio o dominio. Los UseCases encapsulan la lógica de negocio y actúan como intermediarios entre la capa de presentación (UI/ViewModel) y la capa de datos (repositorios).

**Características principales de un UseCase:**

1. **Independencia del framework:** No depende de Android ni de ninguna biblioteca externa.
2. **Reutilización:** Es un componente reutilizable para manejar la lógica de negocio.
3. **Testabilidad:** Al estar aislado, es más fácil de probar.
4. **Orquestación:** Coordina las interacciones entre repositorios y otras dependencias para cumplir un propósito específico.

Por ejemplo, un UseCase podría ser: _"Obtener la lista de usuarios del sistema."_

## **Implementación de un UseCase en Clean Architecture**

Para implentar un caso de uso debemos crear una clase que tenga como dependencias aquellos repositorios que sean necesario para llevar a cabo el caso de uso.

Estas clases la crearemos en el paquete **`domain.usecase`** de nuestro proyecto. El nombre de la clase describirá el caso de uso y acabará en `UseCase`.&#x20;

La lógica del caso de uso se implementa dentro del método **`invoke`**, se hace de esta forma para que los objetos de este caso de uso puedan ser llamados como una función (lo veremos en la siguiente página).

Por ejemplo, si quisiéramos obtener la lista de usuarios del sistema

```kotlin
import kotlinx.coroutines.flow.Flow

class GetUsersUseCase(private val userRepository: UserRepository) {
    // Implementamos la lógica del caso de uso dentro de este método
    operator fun invoke(): Flow<List<User>> {
        // Lógica del caso de uso
        return userRepository.list() 
    }
}
```

O si quiéramos eliminar un usuario

```kotlin
class DeleteUserUseCase(private val userRepository: UserRepository) {
    // Aquí es necesario suspend porque no devuelve un Flow
    suspend operator fun invoke(id: String): Boolean {
        // Lógica del caso de uso
        return userRepository.delete(id) 
    }
}
```
