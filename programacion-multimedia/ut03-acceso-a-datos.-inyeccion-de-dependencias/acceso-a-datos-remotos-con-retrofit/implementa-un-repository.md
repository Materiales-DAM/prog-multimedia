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

# Implementa un repository

Crear un repositorio basado en un cliente Retrofit es muy sencilo, basta con inyectar el cliente de retrofit y hacer las llamadas correspondientes:

```kotlin
package com.example.tasksapp.data.repository

import com.example.tasksapp.data.model.CreateTaskDto
import com.example.tasksapp.data.source.remote.TaskServiceClient
import com.example.tasksapp.domain.model.Task
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.delay
import kotlinx.coroutines.flow.Flow
import kotlinx.coroutines.flow.flow
import kotlinx.coroutines.flow.flowOn

class TaskRestRepository(val taskServiceClient: TaskServiceClient) {

    fun getTasks(): Flow<List<Task>> =
        observeQuery(retryTime = 2000) {
            taskServiceClient
                .getTasks()
                .map { it.toTask() }
        }

    /**
     * Esta funcion sirve para hacer consultas a un servicio de manera continua
     */
    fun <T> observeQuery(retryTime: Long = 5000, query: suspend () -> List<T>): Flow<List<T>> = flow {
        var lastResult: List<T> = emptyList()
        while (true) {
            try {
                val newResult = query()
                if (newResult != lastResult) {
                    lastResult = newResult
                    emit(newResult)
                }
            } catch (e: Exception) {
                println("Error al obtener datos: ${e.message}")
            }
            delay(retryTime) // Consulta cada 5 segundos
        }
    }.flowOn(Dispatchers.IO)

    suspend fun save(task: Task) {
        taskServiceClient.createTask(CreateTaskDto.fromTask(task))
    }

    suspend fun remove(taskId: Int) {
        taskServiceClient.removeTask(taskId)
    }
}
```

Tan solo nos queda añadir TaskRepository al appModule

```kotlin
val appModule = module {
    // Otros componentes aquí
    
    // Singleton del TaskRepository
    single { TaskRestRepository(get()) }

    // UseCases y viewmodel aquí
}
```
