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

# Implementar la navegación

Para poder definir la navegación en nuestra aplicación vamos a seguir los siguientes pasos



{% stepper %}
{% step %}
## **Definición las rutas de navegación**

Crea una sealed class en `presentation.navigation.Screen.kt` para centralizar las rutas.

```kotlin
// Dentro de la sealed class definimos un object por cada ruta existenten
sealed class Screen(val route: String) {
    // Definimos la pantalla Home en la ruta home
    data object Home : Screen("home")
    //  Definimos la pantalla Login en la ruta login
    data object Login : Screen("login")
}
```
{% endstep %}

{% step %}
## **Inyecta el NavController en las pantallas**

Las pantallas que vayan a realizar navegación deben añadir un parámetro NavController que les permita navegar

Por ejemplo, la HomeScreen podría ser

<pre class="language-kotlin"><code class="lang-kotlin">import androidx.compose.runtime.Composable
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*

@Composable
fun HomeScreen(navController: NavController) {
    Column(
        verticalArrangement = Arrangement.Center,
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        Text(
            text = "Home Screen",
            style = MaterialTheme.typography.headlineMedium
        )
        
        Spacer(modifier = Modifier.height(16.dp))
        
        Button(
            // Al pulsar en el botón abre la ventana de Detalles con el parámetro 123 
<strong>            onClick = { navController.navigate(Screen.Login.route) }
</strong>        ) {
            Text("Logout")
        }
    }
}
</code></pre>

Y la pantalla de detalles podría ser

<pre class="language-kotlin"><code class="lang-kotlin">@Composable
fun LoginScreen(navController: NavController, loginScreenViewModel: LoginScreenViewModel = viewModel()) {
    val username by loginScreenViewModel.username.collectAsState()
    val password by loginScreenViewModel.password.collectAsState()
    Surface(
        modifier = Modifier
            .fillMaxSize()
            .statusBarsPadding()
    ) {
        Column(
            verticalArrangement = Arrangement.Center,
            modifier = Modifier.fillMaxSize()
        ) {
            TextField(
                modifier = Modifier.fillMaxWidth(),
                value = username,
                onValueChange = { loginScreenViewModel.setUsername(it) },
                placeholder = { Text("Username") }
            )
            Spacer(modifier = Modifier.height(16.dp))
            TextField(
                modifier = Modifier.fillMaxWidth(),
                value = password,
                onValueChange = { loginScreenViewModel.setPassword(it) },
                placeholder = { Text("Password") },
                visualTransformation = PasswordVisualTransformation()
            )
            Spacer(modifier = Modifier.height(16.dp))
            Row(modifier = Modifier.fillMaxWidth(),
                horizontalArrangement = Arrangement.Center) {
                Button(onClick = {
                    loginScreenViewModel.setUsername("")
                    loginScreenViewModel.setPassword("")
                }) {
                    Text("Limpiar")
                }
                Spacer(modifier = Modifier.width(16.dp))
                Button(onClick = {
<strong>                    navController.navigate(Screen.Home.route)
</strong>                }
                ) {
                    Text("Login")
                }
            }
        }
    }
}
</code></pre>
{% endstep %}

{% step %}
## **Configura el grafo de navegación**

Crea una función `presentation.navigation.NavGraph` que registre las rutas y establezca una pantalla inicial.  Para registrar las rutas utilizaremos el objeto NavHost

```kotlin
import androidx.compose.runtime.Composable
import androidx.navigation.NavHost
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController

// El startDestination define la pantalla que se cargará cuando se abre la aplicación
@Composable
fun NavGraph(startDestination: String = Screen.Home.route) {
    // Cargamos el navController
    val navController = rememberNavController()

    // Creamos un NavHost que arranque con la pantalla de inicio
    NavHost(navController = navController, startDestination = startDestination) {
        // Definimos que para la ruta Screen.Home.route se cargue el composable HomeScreen(navController)
        composable(Screen.Home.route) {
            HomeScreen(navController)
        }
        // Definimos que para la ruta Screen.Login.route se cargue el composable LoginScreen(navController)
        composable(Screen.Login.route) {
            LoginScreen(navController)
        }
    }
}

@Preview(showBackground = true)
@Composable
fun NavGraphPreview() {
    NavGraph()
}
```
{% endstep %}

{% step %}
## **Carga el NavGraph en la actividad**

Finalmente, llama a `NavGraph` desde `MainActivity`.

<pre class="language-kotlin"><code class="lang-kotlin">import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import com.example.app.presentation.navigation.NavGraph

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
<strong>            MyApplicationTheme {
</strong><strong>                NavGraph()
</strong><strong>            }
</strong>        }
    }
}        
</code></pre>
{% endstep %}
{% endstepper %}
