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

# Navegación con parámetros

En ocasiones vamos a querer definir una navegación a una ventana pasando un parámetro, para ello debemos seguir los siguientes pasos

{% stepper %}
{% step %}
## **Definir un Screen con una ruta dinámica**

Creamos un Screen cuya route tiene una variable (se declara entre llaves). Además, añadimos un método createRoute que sustituye el valor de un parámetro en la ruta final.

<pre class="language-kotlin"><code class="lang-kotlin">// Dentro de la sealed class definimos un object por cada ruta existenten
sealed class Screen(val route: String) {
    
    data object Home : Screen("home")
    data object Login : Screen("login")
    
    // Definimos la ruta Details, esta pantalla tiene una parámetro id
<strong>    data object Details : Screen("details/{id}") {
</strong><strong>        fun createRoute(id: String) = "details/$id"
</strong><strong>    }
</strong>}
</code></pre>
{% endstep %}

{% step %}
## Especifica el valor del parámetro al hacer la navegación

<pre class="language-kotlin"><code class="lang-kotlin">import androidx.compose.runtime.Composable
import androidx.compose.foundation.clickable
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*

@Composable
fun HomeScreen(navController: NavController) {
    Column(
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
<strong>            onClick = { navController.navigate(Screen.Details.createRoute("123")) }
</strong>        ) {
            Text("Go to Details")
        }
        
        Spacer(modifier = Modifier.height(16.dp))
        
        Button(
            onClick = { navController.navigate(Screen.Login.route) }
        ) {
            Text("Logout")
        }
    }
}
</code></pre>

Y la pantalla de detalles podría ser

<pre class="language-kotlin"><code class="lang-kotlin">import androidx.compose.runtime.Composable
import androidx.compose.foundation.layout.*
import androidx.compose.material3.*

@Composable
<strong>fun DetailsScreen(navController: NavController, id: String?) {
</strong>    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
    ) {
        Text(
            text = "Details Screen for ID: $id",
            style = MaterialTheme.typography.headlineMedium
        )
        Button(
            onClick = { navController.popBackStack() }
        ) {
            Text("Go Back")
        }
    }
}
</code></pre>
{% endstep %}

{% step %}
## **Añade la nueva ventana al grafo de navegación**

Registramos la ruta dinámica en navHost y obtenemos el valor del parámetro a partir del backStackEntry

<pre class="language-kotlin"><code class="lang-kotlin">import androidx.compose.runtime.Composable
import androidx.navigation.NavHost
import androidx.navigation.compose.NavHost
import androidx.navigation.compose.composable
import androidx.navigation.compose.rememberNavController

// El startDestination define la pantalla que se cargará cuando se abre la aplicación
@Composable
fun NavGraph(startDestination: String = Screen.Home.route) {
    val navController = rememberNavController()

    NavHost(navController = navController, startDestination = startDestination) {
        composable(Screen.Home.route) {
            HomeScreen(navController)
        }
        
       composable(Screen.Login.route) {
            LoginScreen(navController)
        }
        
        // Definimos que para la ruta Screen.Details se cargue el composable DetailsScreen(navController, id)
<strong>        composable(Screen.Details.route) { backStackEntry ->
</strong><strong>            // Como esta ruta tiene parámetro puedo obtenerlo así, el nombre 
</strong><strong>            // de este parámetro debe coincidir con el declarado en Screen.Details.route
</strong><strong>            val id = backStackEntry.arguments?.getString("id")
</strong><strong>            // Crea la screen DetailsScreen con los parámetros 
</strong><strong>            DetailsScreen(navController, id)
</strong><strong>        }
</strong>    }
}

@Preview(showBackground = true)
@Composable
fun NavGraphPreview() {
    NavGraph()
}
</code></pre>
{% endstep %}
{% endstepper %}
