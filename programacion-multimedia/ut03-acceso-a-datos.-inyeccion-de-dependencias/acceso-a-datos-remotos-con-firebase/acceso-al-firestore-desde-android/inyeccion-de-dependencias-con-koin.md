---
cover: ../../../.gitbook/assets/koin.png
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

# Inyección de dependencias con Koin

La **Inyección de Dependencias (DI)** es un patrón de diseño en el que los objetos (clases) no crean sus propias dependencias, sino que estas se les proporcionan (inyectan) desde el exterior. Esto se hace para:

1. Reducir el acoplamiento entre clases.
2. Facilitar el cambio de implementaciones.
3. Simplificar las pruebas, ya que se pueden proporcionar dependencias simuladas (mocks).

En el contexto de Android, la DI es especialmente útil para administrar dependencias como repositorios, servicios y ViewModels.

## **¿Qué es Koin?**

Koin es un framework ligero para la inyección de dependencias en Kotlin. Diseñado con un enfoque minimalista, Koin permite configurar y gestionar dependencias de manera declarativa y sencilla. Sus principales características son:

1. **Simplicidad:** No requiere generación de código ni anotaciones.
2. **Modularidad:** Permite dividir las dependencias en módulos reutilizables.
3. **Compatibilidad:** Funciona perfectamente con Jetpack Compose y Android.

### **Configuración de Koin en Jetpack Compose**

En el archivo `build.gradle` del módulo, añade las dependencias necesarias:

```kotlin
implementation("io.insert-koin:koin-android:4.1.1")
implementation("io.insert-koin:koin-androidx-compose:4.1.1")
```

### Implementación en el proyecto

{% stepper %}
{% step %}
### Definir un módulo Koin

Crea un archivo Kotlin en el paquete `di` del proyecto para definir la inyección de dependencias. Por ejemplo:

{% code title="AppModule.kt" %}
```kotlin
val appModule = module {
    // Singleton del FirebaseFirestore
    single { FirebaseFirestore.getInstance() }
    // Singleton del respositorio de usuarios, se le inyecta el FirebaseFirestore creado en la sección anterior
    single { UserFirestoreRepository(get()) }
    // Usamos factory para que proporcione una instancia del UseCase cada vez que se solicite
    factory { GetUsersUseCase(get()) }
    // Usamos factory para que proporcione una instancia del UseCase cada vez que se solicite
    factory { DeleteUserUseCase(get()) }
    // Crea el viewModel con las dependencias que tenga definidas
    viewModel { UsersScreenViewModel(get(), get()) }
}
```
{% endcode %}
{% endstep %}

{% step %}
### Crear una clase Application para iniciar Koin

En el paquete base del proyecto, crea una clase que defina cómo se inicia la aplicación

{% code title="MyUserApp.kt" %}
```kotlin
class MyUserApp : Application() {
    override fun onCreate() {
        super.onCreate()
        startKoin {
            androidContext(this@MyUserApp)
            modules(appModule)
        }
    }
}
```
{% endcode %}
{% endstep %}

{% step %}
### Actualiza el AndroidManifest.xml con la aplicación que acabamos de crear

Se debe poner el nombre de la clase que extiende Application en la propiedad `android:name`, precedida por un `.`

<pre class="language-xml"><code class="lang-xml">&#x3C;manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    &#x3C;application
<strong>        android:name=".MyUserApp"
</strong>        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MyAndroidApp"
        tools:targetApi="31">

        ...
        
        &#x3C;/application>

&#x3C;/manifest>
</code></pre>
{% endstep %}

{% step %}
### Modifica la creación de los viewModel para que usen Koin

Simplementa hay que sustituir el método constructor de viewModel() a koinViewModel()

<pre class="language-kotlin"><code class="lang-kotlin">@Composable
fun UsersScreen(
    navController: NavController,
    // usersViewModel: usersViewModel = viewModel()
<strong>    usersViewModel: UsersViewModel = koinViewModel()
</strong>) {
    // Aquí iría la definición de la ventana de usuarios
}
</code></pre>
{% endstep %}
{% endstepper %}
