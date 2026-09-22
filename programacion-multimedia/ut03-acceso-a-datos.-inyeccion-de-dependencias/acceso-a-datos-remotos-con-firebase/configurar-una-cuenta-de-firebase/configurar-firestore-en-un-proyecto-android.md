---
cover: ../../../.gitbook/assets/firestores.png
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

# Configurar Firestore en un proyecto Android

{% stepper %}
{% step %}
### Copia el fichero de configuración `google-services.json` al proyecto (descargado de Firebase previamente)&#x20;

1. Cambia a la opción Project en la vista del navegador de archivos\
   ![](<../../../.gitbook/assets/image (41).png>)
2. Copia el fichero dentro de la carpeta app
3. Vuelve a la opción Android
{% endstep %}

{% step %}
`build.gradle.kts (Project)`

Añade el plugin de google services al fichero `build.gradle.kts (Project)`

{% code title="build.gradle.kts" %}
```kotlin
plugins {
    alias(libs.plugins.android.application) apply false
    alias(libs.plugins.jetbrains.kotlin.android) apply false
    id("com.google.gms.google-services") version "4.4.2" apply false

}
```
{% endcode %}
{% endstep %}

{% step %}
`build.gradle.kts (Module)`

Añade este plugin dentro de `plugins`

```kotlin
plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.jetbrains.kotlin.android)
    // Este es el plugin de google services
    id("com.google.gms.google-services")
}
```

Añade la siguiente dependencia dentro de `dependencies`&#x20;

```kotlin
implementation("com.google.firebase:firebase-firestore:25.1.1")
```
{% endstep %}
{% endstepper %}
