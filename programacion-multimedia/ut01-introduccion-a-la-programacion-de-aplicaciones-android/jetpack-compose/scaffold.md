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

# Scaffold

`Scaffold` es un componente clave en Jetpack Compose que te ayuda a estructurar y organizar la UI de tu aplicación de manera eficiente. Proporciona una estructura básica para la pantalla, permitiendo organizar componentes como barras de aplicación (`TopAppBar`), botones flotantes de acción (`FAB`), menús de navegación, y más. Es un contenedor de diseño de alto nivel que proporciona una estructura visual coherente, facilitando el uso de componentes comunes como una barra superior, botones flotantes y menús laterales. Proporciona una forma consistente y estandarizada de estructurar la pantalla de una aplicación.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

## Componentes principales

* **TopBar**: Generalmente es un `TopAppBar` que aparece en la parte superior de la pantalla.
* **BottomBar**: Puede ser una barra de navegación o cualquier otro contenido que quieras anclar en la parte inferior.
* **FloatingActionButton (FAB)**: Un botón flotante que típicamente realiza una acción principal.
* **DrawerContent**: Un menú lateral que puede deslizarse desde el borde izquierdo de la pantalla.
* **SnackbarHost**: Muestra mensajes temporales (snackbars).
* **BodyContent**: Es el contenido principal de la pantalla que puede ser cualquier composición.

```kotlin
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.material3.*
import androidx.compose.runtime.Composable
import androidx.compose.ui.Modifier
import com.example.myapplication.ui.theme.MyApplicationTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            MyApplicationTheme {
                MyScaffoldApp()
            }
        }
    }
}

@Composable
fun MyScaffoldApp() {
    // Estructura básica de Scaffold
    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("Scaffold Demo") }
            )
        },
        floatingActionButton = {
            FloatingActionButton(onClick = { /* Acción del FAB */ }) {
                Text("FAB")
            }
        },
        content = { paddingValues ->
            // Contenido principal de la pantalla
            Text(
                text = "Contenido del cuerpo",
                modifier = Modifier
                    .fillMaxSize()
                    .padding(paddingValues) // Aplica padding proveniente del Scaffold
            )
        }
    )
}
```

#### Explicación del código:

1. **`Scaffold`** define la estructura de la pantalla.
2. **`TopAppBar`**: Se utiliza como una barra superior con un título simple.
3. **`FloatingActionButton` (FAB)**: Un botón flotante que realiza una acción cuando es presionado.
4. **`content`**: Es el cuerpo principal de la pantalla. El contenido del cuerpo se envuelve en el `paddingValues` para respetar el espacio reservado por el `TopAppBar` y otros componentes.

### `TopAppBar` y un `FloatingActionButton`

Vamos a mejorar nuestro `Scaffold` añadiendo más detalles a la barra superior y al botón flotante de acción.

```kotlin
@Composable
fun MyScaffoldApp() {
    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text("Scaffold con FAB") },
                navigationIcon = {
                    IconButton(onClick = { /* Acción de icono de navegación */ }) {
                        Icon(Icons.Default.Menu, contentDescription = "Menú")
                    }
                },
                actions = {
                    IconButton(onClick = { /* Acción de buscar */ }) {
                        Icon(Icons.Default.Search, contentDescription = "Buscar")
                    }
                }
            )
        },
        floatingActionButton = {
            FloatingActionButton(onClick = { /* Acción del FAB */ }) {
                Icon(Icons.Default.Add, contentDescription = "Agregar")
            }
        },
        floatingActionButtonPosition = FabPosition.End, // Posición del FAB (End, Center)
        content = { paddingValues ->
            Text(
                text = "Este es el contenido principal de la pantalla",
                modifier = Modifier
                    .fillMaxSize()
                    .padding(paddingValues)
            )
        }
    )
}
```

**Detalles adicionales:**

* **`navigationIcon`**: Añade un ícono de navegación en la barra superior, como el típico ícono de hamburguesa para abrir un menú lateral.
* **`actions`**: Añade botones de acción a la derecha de la barra superior, como el ícono de búsqueda.
* **`floatingActionButtonPosition`**: Controla la posición del `FAB`, que puede estar centrado o alineado a la derecha (`End`).

### Menú lateral (`Drawer` )

Ahora, vamos a agregar un menú lateral (`Drawer`), que aparece cuando el usuario desliza desde el borde izquierdo o al tocar el ícono de menú.

```kotlin
import androidx.compose.material3.DrawerValue
import androidx.compose.material3.rememberDrawerState
import androidx.compose.material3.ModalDrawer
import androidx.compose.material3.ModalDrawerSheet
import androidx.compose.material3.DrawerContent
import androidx.compose.foundation.layout.Column

@Composable
fun MyScaffoldWithDrawer() {
    val drawerState = rememberDrawerState(initialValue = DrawerValue.Closed)

    ModalDrawer(
        drawerState = drawerState,
        drawerContent = {
            ModalDrawerSheet {
                Column {
                    Text("Opción 1")
                    Text("Opción 2")
                }
            }
        },
        content = {
            Scaffold(
                topBar = {
                    TopAppBar(
                        title = { Text("Scaffold con Drawer") },
                        navigationIcon = {
                            IconButton(onClick = { /* Acción del drawer */ }) {
                                Icon(Icons.Default.Menu, contentDescription = "Menú")
                            }
                        }
                    )
                },
                floatingActionButton = {
                    FloatingActionButton(onClick = { /* Acción del FAB */ }) {
                        Icon(Icons.Default.Add, contentDescription = "Agregar")
                    }
                },
                content = { paddingValues ->
                    Text(
                        text = "Contenido principal",
                        modifier = Modifier
                            .fillMaxSize()
                            .padding(paddingValues)
                    )
                }
            )
        }
    )
}
```

**Explicación:**

* **`ModalDrawer`**: Crea un menú lateral deslizante que contiene varias opciones.
* **`drawerContent`**: Aquí defines el contenido del menú lateral. En este caso, se agregan dos opciones como texto.
* **`drawerState`**: Se utiliza para controlar el estado abierto/cerrado del drawer.

### Barra inferior (BottomBar)

Si quieres añadir una barra inferior, es muy simple con el `Scaffold`:

```kotlin
Scaffold(
    topBar = {
        TopAppBar(title = { Text("AppBar") })
    },
    floatingActionButton = {
        FloatingActionButton(onClick = { /* Acción del FAB */ }) {
            Icon(Icons.Default.Add, contentDescription = "Agregar")
        }
    },
    bottomBar = {
        BottomAppBar {
            Text("Este es un BottomBar")
        }
    },
    content = { paddingValues ->
        Text(
            text = "Contenido con BottomBar",
            modifier = Modifier
                .fillMaxSize()
                .padding(paddingValues)
        )
    }
)
```
