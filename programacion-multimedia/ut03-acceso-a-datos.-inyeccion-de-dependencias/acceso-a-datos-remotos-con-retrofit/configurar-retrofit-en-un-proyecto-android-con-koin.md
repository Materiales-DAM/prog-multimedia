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

# Configurar Retrofit en un proyecto Android con Koin

{% stepper %}
{% step %}
### Añadir las dependencias

Agrega las dependencias necesarias en tu archivo `build.gradle` (nivel de módulo):

```gradle
implementation("com.squareup.retrofit2:retrofit:2.9.0")
implementation("com.squareup.retrofit2:converter-gson:2.9.0")
```
{% endstep %}

{% step %}
### Configura Koin

Crea un módulo donde se configurará Retrofit para realizar las solicitudes HTTP.

{% code title="di.RetrofitModule.kt" %}
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
            // La IP 10.0.2.2 hace referencia la ip del host del emulador
            .baseUrl("http://10.0.2.2:8080")
            // Se configura la serialización con JSON
            .addConverterFactory(GsonConverterFactory.create())
            .build()
    }
}
```
{% endcode %}
{% endstep %}

{% step %}
### Actualiza la clase Application para que use el módulo de Retrofit

<pre class="language-kotlin"><code class="lang-kotlin">import android.app.Application
import org.koin.android.ext.koin.androidContext
import org.koin.core.context.startKoin

class MyApp : Application() {
    override fun onCreate() {
        super.onCreate()
        startKoin() {
            androidContext(this@MyApp)
            modules(
                appModule,
<strong>                retrofitModule
</strong>            )
        }
    }
}
</code></pre>
{% endstep %}

{% step %}
### Configura AndroidManifest.xml

Por defecto, Android no permite las comunicaciones no encriptadas. Para poder comunicarnos con la API REST tenemos dos opciones:

*   Habilitar las comunicaciones no encritpadas, añade la entrada usesCleartextTraffic

    <pre class="language-xml"><code class="lang-xml">&#x3C;application
        android:name=".MyApp"
        
    <strong>    android:usesCleartextTraffic="true"
    </strong>    
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        ....
        >
        
    </code></pre>
* [Habilitar el protocolo HTTPS en el lado del servidor](https://www.baeldung.com/spring-boot-https-self-signed-certificate).

Además, hay que añadir el siguiente permiso antes de application

<pre class="language-xml"><code class="lang-xml">&#x3C;manifest xmlns:android="http://schemas.android.com/apk/res/android" xmlns:tools="http://schemas.android.com/tools">

<strong>    &#x3C;uses-permission android:name="android.permission.INTERNET"/>
</strong>
    &#x3C;application
        android:name=".MyApp"
        ...
        >
</code></pre>
{% endstep %}
{% endstepper %}
