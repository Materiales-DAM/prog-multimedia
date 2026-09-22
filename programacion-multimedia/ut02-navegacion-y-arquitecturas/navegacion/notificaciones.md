---
cover: ../../.gitbook/assets/notifications.png
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

# Notificaciones

En Jetpack Compose, puedes crear fácilmente diálogos y Snackbars para mostrar mensajes o notificaciones. A continuación te muestro cómo implementar un `AlertDialog` y un `Snackbar` en una aplicación.

## **AlertDialog**

Es una ventana emergente que solicita la atención del usuario y generalmente ofrece una decisión (aceptar, cancelar, etc.). Para poder hacer esto necesitamos crear un estado booleano que va controlar si el dialogo se muestra o no.

```kotlin
@Composable
fun DialogExample() {
    var showDialog by remember { mutableStateOf(false) }

    // Botón para mostrar el diálogo
    Button(onClick = { showDialog = true }) {
        Text("Mostrar Dialogo")
    }

    // Mostrar AlertDialog
    if (showDialog) {
        AlertDialog(
            onDismissRequest = { showDialog = false },
            title = { Text(text = "Título del Diálogo") },
            text = { Text("Este es un mensaje dentro del diálogo.") },
            confirmButton = {
                Button(onClick = { showDialog = false }) {
                    Text("Aceptar")
                }
            },
            dismissButton = {
                Button(onClick = { showDialog = false }) {
                    Text("Cancelar")
                }
            }
        )
    }
}
```

## **Snackbar**

Un `Snackbar` es una pequeña notificación que aparece en la parte inferior de la pantalla, generalmente para proporcionar comentarios sobre una operación realizada por el usuario. Vamos a configurar este tipo de notificaciones para que se muestren dentro del snackBarHost de un Scaffold.

<pre class="language-kotlin"><code class="lang-kotlin">@Composable
fun SnackbarExample() {
<strong>    val snackbarHostState = remember { SnackbarHostState() }
</strong><strong>    val scope = rememberCoroutineScope()
</strong>
    Scaffold(
<strong>        snackbarHost = { SnackbarHost(snackbarHostState) },
</strong>        content = { innerPadding ->
            Column(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(innerPadding)
                    .padding(16.dp),
                verticalArrangement = Arrangement.Center,
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                Button(onClick = {
<strong>                    scope.launch {
</strong><strong>                        snackbarHostState.showSnackbar("Este es un Snackbar")
</strong><strong>                    }
</strong>                }) {
                    Text("Mostrar Snackbar")
                }
            }
        }
    )
}
</code></pre>
