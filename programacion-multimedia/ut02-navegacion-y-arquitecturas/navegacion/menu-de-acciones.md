---
cover: ../../.gitbook/assets/navigation.png
coverY: 0
layout:
  width: default
  cover:
    visible: true
    size: full
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

# Menú de acciones

En Jetpack Compose, un menú de acciones (por ejemplo, el típico menú desplegable que aparece en la parte superior derecha de una **AppBar**) se puede implementar utilizando un **DropdownMenu**.&#x20;

#### Para implementar un menú de este tipo es necesario:

1. **Preparar el estado**: es necesario declarar un estado para controlar si el menú está desplegado o no.
2. **Agregar botones de acción (IconButton)**: Normalmente, se usa un `IconButton` en la `TopAppBar` para activar el menú.
3. **Definir el DropdownMenu**: Usa el componente `DropdownMenu` para mostrar el menú.
4. **Agregar los elementos del menú**: Usa `DropdownMenuItem` para los elementos del menú.

#### Ejemplo completo

```kotlin
import androidx.compose.material.icons.Icons

import androidx.compose.material.icons.filled.Menu
import androidx.compose.material3.DropdownMenu
import androidx.compose.material3.DropdownMenuItem
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.HorizontalDivider
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.Text
import androidx.compose.material3.TopAppBar
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.setValue
import androidx.navigation.NavController
import com.example.librarynavigation.presentation.navigation.Screen

@Composable
@OptIn(ExperimentalMaterial3Api::class)
fun MenuDeAcciones(navController: NavController) {
    // Estado para controlar la visibilidad del menú
    var expanded by remember { mutableStateOf(false) }

    // Barra de herramientas (TopAppBar)
    TopAppBar(
        title = { Text("Menú de acciones") },
        actions = {
            // Botón de menú
            IconButton(onClick = { expanded = true }) {
                Icon(
                    imageVector = Icons.Default.Menu,
                    contentDescription = "Menú"
                )
            }

            // Menú desplegable
            DropdownMenu(
                expanded = expanded,
                onDismissRequest = { expanded = false }
            ) {
                DropdownMenuItem(
                    text = { Text("Home") },
                    onClick = {
                        // Acción 1
                        expanded = false
                        navController.navigate(Screen.Home.route)
                    }
                ) 
                DropdownMenuItem(
                    text = {
                        Text("Back")
                    },
                    onClick = {
                        // Acción 2
                        expanded = false
                        navController.popBackStack()
                    }
                )
                // Línea divisoria entre elementos
                HorizontalDivider() 
                DropdownMenuItem(
                    text = {
                        Text("Other action")
                    },
                    onClick = {
                        // Simplemente cierra el menú desplegable
                        expanded = false
                    }
                )
            }
        }
    )
}
```

Aplicar el menú a un Screen

<pre class="language-kotlin"><code class="lang-kotlin">@Composable
fun Screen1(
    navController: NavController
) {
    Scaffold(
<strong>        topBar = {
</strong><strong>            MenuDeAcciones(navController)
</strong><strong>        }
</strong>    ) { innerPadding ->
        // Elementos de la ventana
    }
}
</code></pre>
