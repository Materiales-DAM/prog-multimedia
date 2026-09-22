---
cover: ../../.gitbook/assets/jetpack.png
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

# ViewModel con data classes

En muchas ocasiones, vamos a quere crear ventanas que sirven para rellenar los datos de una determinada entidad y al pulsar un botón se guardará en una base de datos. Para este tipo de ventanas vinculadas a una instancia de una entidad, vamos a usar un objeto de una data class como estado del ViewModel.

Cuando queramos modificar algún campo de dicho objeto utilizaremos el método copy de las data classes para modificar solo ese campo.

### Ejemplo&#x20;

Por ejemplo, podemos crear una aplicación para gestionar tareas (Task). Esta aplicación tendrá una ventana CreateTaskScreen (sirve para crear una nueva tarea)

Cada tarea la reprsentaremos con la data class Task

{% code title="com.example.myApp.domain.model.Task.kt" %}
```kotlin
data class Task(val id: Int, val title: String, val description: String)
```
{% endcode %}

#### CreateTaskScreen

Primer creamos el ViewModel que gestiona los datos de una tarea

```kotlin
import androidx.lifecycle.ViewModel
import com.example.tasksapp.domain.model.Task
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow

class CreateTaskViewModel : ViewModel() {
    // Estado mutable que almacena el listado de tareas
    private val _task = MutableStateFlow<Task>(
        Task(0, "", "")
    )
    // Version inmutable del estado anterior, es el estado que va a leer el UI
    val task: StateFlow<Task> = _task
    
    
    fun setTitle(title: String) {
        _task.value = _task.value.copy(title = title)
    }
    
    fun setDescription(description: String) {
        _task.value = _task.value.copy(description = description)
    }
    
    
    fun save() {
        // TODO Aquí va la lógica para guardar la tarea
        // Veremos qué se hace en el próximo tema
    }
}
```

Ahora ya podemos usarlo en la ventana CreateTaskScreen

```kotlin
package com.example.tasksapp.presentation.ui.screens.tasks

import CreateTaskViewModel
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.material3.Button
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Text
import androidx.compose.material3.TextField
import androidx.compose.runtime.Composable
import androidx.compose.runtime.collectAsState
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import androidx.lifecycle.viewmodel.compose.viewModel
import androidx.compose.runtime.getValue


@Composable
fun CreateTaskScreen(createTaskViewModel: CreateTaskViewModel = viewModel()) {
    val task by createTaskViewModel.task.collectAsState()

    Scaffold(
        topBar = {
            Text("Crear tarea")
        }
    ) { innerPadding ->
        Column(Modifier.padding(innerPadding)) {
            TextField(
                modifier = Modifier.fillMaxWidth(),
                value = task.title,
                onValueChange = {
                    createTaskViewModel.setTitle(it)
                }
            )
            Spacer(modifier = Modifier.height(16.dp))

            TextField(
                modifier = Modifier.fillMaxWidth(),
                value = task.description,
                onValueChange = {
                    createTaskViewModel.setDescription(it)
                }
            )
            Spacer(modifier = Modifier.height(16.dp))

            Button(
                modifier = Modifier.align(Alignment.CenterHorizontally),
                onClick = { createTaskViewModel.save() }
            ) {
                Text("Guardar")
            }
        }
    }
}
```
