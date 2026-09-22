---
cover: ../../.gitbook/assets/retrofit.png
coverY: -100.39466666666667
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

# Crea un cliente de una API

Supongamos que existe un servicio REST ejecutándose en  un servidor que provee de los siguientes endpoints:

## **Endpoints**

### 🔹 **1. Obtener todas las tareas**

**📍 Endpoint:** `GET /tasks`\
**📥 Request Body:** ❌ _No requiere body_\
**📤 Response (200 OK):**

{% code title="response-body" %}
```json
[
    {
        "id": 1,
        "title": "Comprar víveres",
        "description": "Leche, huevos, pan"
    },
    {
        "id": 2,
        "title": "Llamar a Juan",
        "description": "Confirmar reunión del martes"
    }
]
```
{% endcode %}

### 🔹 **2. Obtener una tarea por ID**

**📍 Endpoint:** `GET /tasks/{id}`\
**📥 Request Body:** ❌ _No requiere body_\
**📤 Response (200 OK):**

{% code title="response-body" %}
```json
{
    "id": 1,
    "title": "Comprar víveres",
    "description": "Leche, huevos, pan"
}
```
{% endcode %}

**📤 Response (404 Not Found):**

{% code title="response-body" %}
```json
{
    "error": "Tarea no encontrada"
}
```
{% endcode %}

#### 🔹 **3. Crear una nueva tarea**

**📍 Endpoint:** `POST /tasks`\
**📥 Request Body:**

{% code title="body" %}
```json
{
    "title": "Leer un libro",
    "description": "Capítulo 4 de 'El Principito'"
}
```
{% endcode %}

**📤 Response (201 Created):**

{% code title="response-body" %}
```json
{
    "id": 3,
    "title": "Leer un libro",
    "description": "Capítulo 4 de 'El Principito'"
}
```
{% endcode %}

**📤 Response (400 Bad Request) - Si falta algún campo:**

{% code title="response-body" %}
```json
{
    "error": "El campo 'title' es obligatorio"
}
```
{% endcode %}

#### 🔹 **4. Actualizar una tarea existente**

**📍 Endpoint:** `PUT /tasks/{id}`\
**📥 Request Body:**

{% code title="body" %}
```json
{
    "title": "Comprar víveres",
    "description": "Leche, huevos, pan y queso"
}
```
{% endcode %}

**📤 Response (200 OK):**

{% code title="response-body" %}
```json
{
    "id": 1,
    "title": "Comprar víveres",
    "description": "Leche, huevos, pan y queso"
}
```
{% endcode %}

**📤 Response (404 Not Found) - Si la tarea no existe:**

{% code title="response-body" %}
```json
{
    "error": "Tarea no encontrada"
}
```
{% endcode %}

#### 🔹 **5. Eliminar una tarea**

**📍 Endpoint:** `DELETE /tasks/{id}`\
**📥 Request Body:** ❌ _No requiere body_\
**📤 Response (204 No Content):** ❌ _No devuelve contenido_

**📤 Response (404 Not Found) - Si la tarea no existe:**

{% code title="" %}
```json
{
    "error": "Tarea no encontrada"
}
```
{% endcode %}

## DTOs

Debes crear los DTO necesarios para comunicarte con el servicio REST

{% code title="data.model.CreateTaskDto.kt" %}
```kotlin
package com.example.tasksapp.data.model

import com.example.tasksapp.domain.model.Task

data class CreateTaskDto(
    val title: String,
    val description: String
) {
    companion object {
        fun fromTask(task: Task) =
            CreateTaskDto(
                title = task.title,
                description = task.description
            )
    }

    fun toTask(id: Int) =
        Task(
            id = id,
            title = title,
            description = description
        )
}
```
{% endcode %}

{% code title="data.model.TaskDto" %}
```kotlin
package com.example.tasksapp.data.model

import com.example.tasksapp.domain.model.Task

data class TaskDto(
    val id: Int,
    val title: String,
    val description: String
) {

    fun toTask() =
        Task(
            id = id,
            title = title,
            description = description
        )
}
```
{% endcode %}

## Cliente

Para acceder a este servicio tendríamos que implementar un cliente como este

```kotlin
package com.example.tasksapp.data.source.remote

import com.example.tasksapp.data.model.CreateTaskDto
import com.example.tasksapp.data.model.TaskDto
import retrofit2.http.*

// Interfaz de API
interface TaskServiceClient {

    @GET("tasks")
    suspend fun getTasks(): List<TaskDto>

    @POST("tasks")
    suspend fun createTask(@Body task: CreateTaskDto)

    @DELETE("tasks/{id}")
    suspend fun removeTask(@Path("id") taskId: Int)
}
```

Una vez hemos implementado el cliente, hay que instanciarlo en retrofitModule. Es muy importante editar la baseURL poniendo la ip / host donde está corriendo el servicio REST

```kotlin
import com.google.gson.Gson
import com.google.gson.GsonBuilder
import okhttp3.OkHttpClient
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory
import retrofit2.create

val retrofitModule = module {
    // API retrofit
    single {
        Retrofit.Builder()
            // Se configura la URL del servicio REST
            .baseUrl("http://10.0.2.2:8080")
            // Se configura la serialización con JSON
            .addConverterFactory(GsonConverterFactory.create())
            .build()
    }

    single<TaskServiceClient> { get<Retrofit>().create(TaskServiceClient::class.java) }
}
```
