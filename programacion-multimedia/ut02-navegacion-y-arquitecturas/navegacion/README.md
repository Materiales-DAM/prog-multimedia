---
cover: ../../.gitbook/assets/navigation.png
coverY: 0
---

# Navegación

La navegación en **Jetpack Compose** es un sistema que permite manejar y gestionar el flujo entre diferentes pantallas (o composables) dentro de una aplicación Android. Este sistema es parte de la biblioteca **Navigation for Jetpack Compose**, que está diseñada específicamente para trabajar con el paradigma declarativo de Compose.

## **Características principales de la navegación en Jetpack Compose**

1. **Declarativa**:
   * En lugar de trabajar con `Fragments` o `Activities`, defines y administras las rutas directamente en funciones composables.
   * Esto simplifica el flujo de navegación y se adapta al modelo basado en estados de Compose.
2. **Centralización de rutas**:
   * Las rutas (o destinos) se definen de manera centralizada utilizando un **NavGraph**, lo que hace que el manejo de la navegación sea más claro y estructurado.
3. **Control con `NavController`**:
   * El **NavController** es el núcleo del sistema de navegación. Permite realizar acciones como navegar entre pantallas, pasar datos entre ellas y manejar el stack de navegación.
4. **Soporte para argumentos y deep links**:
   * Puedes enviar parámetros entre pantallas o manejar enlaces externos directamente desde el sistema de navegación.

## **Elementos clave del sistema de navegación**

### **NavController**

Es el objeto central que administra la navegación. Permite moverse entre pantallas, regresar a una pantalla previa y limpiar el historial de navegación, entre otras cosas.

Se usa junto con `rememberNavController()` para crear una instancia en Compose.

```kotlin
val navController = rememberNavController()
```

### **NavHost**

Define la estructura de las rutas (pantallas o destinos) de tu aplicación. Cada destino se registra como un `composable`.

```kotlin
NavHost(navController = navController, startDestination = "home") {
    composable("home") { HomeScreen(navController) }
    composable("details/{id}") { backStackEntry ->
        DetailsScreen(navController, backStackEntry.arguments?.getString("id"))
    }
}
```

### **Rutas (Destinos)**

Cada destino es una pantalla o componente específico que defines en el gráfico de navegación. Las rutas pueden incluir argumentos dinámicos como parámetros (por ejemplo, `details/{id}`).

### **Acciones de navegación**

Navegar a otro destino:

```kotlin
navController.navigate("details/123")
```

Volver al destino anterior:

```kotlin
navController.popBackStack()
```
