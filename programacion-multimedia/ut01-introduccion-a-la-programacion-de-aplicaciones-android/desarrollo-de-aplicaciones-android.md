---
cover: ../.gitbook/assets/android.gif
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

# Desarrollo de aplicaciones Android

El desarrollo de aplicaciones Android puede llevarse a cabo utilizando dos enfoques principales para diseñar las interfaces de usuario: **XML** y **Jetpack Compose**. Ambos métodos permiten la creación de interfaces visuales en aplicaciones, pero tienen diferencias clave en su estructura y filosofía. Aquí te explico ambos enfoques y sus diferencias:

## **Desarrollo basado en XML**

Históricamente, el desarrollo de interfaces en Android se ha realizado mediante **archivos XML** (Extensible Markup Language). En este enfoque, se definen las vistas y la jerarquía de la interfaz en archivos separados del código de la lógica de la aplicación (en archivos `.xml` dentro de la carpeta `res/layout`). Los componentes visuales como botones, textos, imágenes y listas se crean usando etiquetas XML que describen las propiedades visuales y su disposición.**:**

```xml
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hola, Mundo!" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Presionar" />
</LinearLayout>
```

Las principales características son:

* Las vistas se describen mediante **XML**, pero la lógica de interacción se maneja en código Java o Kotlin.
* **Jerarquía de vistas**: Las vistas (Views) se anidan en una estructura jerárquica, donde cada componente ocupa un espacio en memoria.
* **UI Imperativa**: Aunque la estructura de la interfaz es declarativa (XML), su manipulación en tiempo de ejecución es más imperativa. Es decir, el desarrollador debe actualizar las vistas manualmente a través de código cuando cambien los datos.
* **Fragmentación del código**: El diseño y la lógica se manejan en archivos separados (XML y código Java/Kotlin).

## **Desarrollo con Jetpack Compose**

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="188"><figcaption></figcaption></figure>

**Jetpack Compose** es un moderno **kit de herramientas declarativo** de Android que permite crear interfaces de usuario completamente en código, sin necesidad de XML. Lanzado oficialmente por Google en 2020, Jetpack Compose está escrito en Kotlin y simplifica la creación de interfaces gracias a un enfoque declarativo, inspirado por frameworks como React o SwiftUI.

```kotlin
@Composable
fun Greeting() {
    Column {
        Text(text = "Hola, Mundo!")
        Button(onClick = { /* Acción al presionar */ }) {
            Text(text = "Presionar")
        }
    }
}
```

Las principales características son:

* **Declarativo completo**: La interfaz se construye mediante código declarativo. Se describe el estado de la UI y Jetpack Compose se encarga de renderizar los cambios cuando el estado subyacente cambia.
* **UI Reactiva**: La interfaz está vinculada al estado de los datos. Si el estado cambia, la UI se actualiza automáticamente, sin necesidad de manipular manualmente las vistas.
* **Menos fragmentación**: Todo, desde el diseño de la UI hasta la lógica, puede estar en el mismo archivo, lo que facilita el manejo del código.
* **Optimización del rendimiento**: Jetpack Compose utiliza menos jerarquías de vistas que el enfoque basado en XML, lo que puede mejorar el rendimiento en términos de memoria y procesamiento.
* **Compatibilidad con vistas heredadas**: Aunque es un enfoque moderno, Compose es compatible con vistas tradicionales de Android, lo que permite mezclar ambas técnicas si es necesario.

## **Diferencias clave entre XML y Jetpack Compose**

<table><thead><tr><th width="230.60003662109375">Característica</th><th>XML</th><th>Jetpack Compose</th></tr></thead><tbody><tr><td><strong>Paradigma</strong></td><td>Imperativo (en código)</td><td>Declarativo (reactivo)</td></tr><tr><td><strong>Definición de la UI</strong></td><td>Archivos XML separados</td><td>En código Kotlin</td></tr><tr><td><strong>Actualización de UI</strong></td><td>Manual (modificar vistas)</td><td>Automática según el estado</td></tr><tr><td><strong>Lenguaje principal</strong></td><td>XML y Kotlin/Java (separado)</td><td>Solo Kotlin (integrado)</td></tr><tr><td><strong>Compatibilidad</strong></td><td>Enfoque tradicional en Android</td><td>Tecnología más moderna</td></tr><tr><td><strong>Curva de aprendizaje</strong></td><td>Fácil de aprender, más código</td><td>Más conciso, pero requiere aprender Kotlin declarativo</td></tr><tr><td><strong>Modularidad</strong></td><td>UI y lógica separadas</td><td>UI y lógica juntas en composables</td></tr><tr><td><strong>Rendimiento</strong></td><td>Más jerarquías de vistas</td><td>Optimización en la renderización</td></tr></tbody></table>

#### ¿Cuál elegir?

* **XML**: Es ideal para proyectos más antiguos o cuando ya se tiene experiencia en el desarrollo tradicional de Android. Si la aplicación tiene muchas dependencias o módulos antiguos que se basan en XML, puede ser más sencillo continuar con este enfoque.
* **Jetpack Compose**: Es la opción recomendada para nuevos proyectos, especialmente si quieres aprovechar las ventajas de un desarrollo más ágil, moderno y con menos código. Compose permite mayor flexibilidad, reactividad y simplicidad en comparación con XML.

Ambos enfoques siguen siendo compatibles, por lo que puedes migrar gradualmente tu proyecto de XML a Jetpack Compose si lo prefieres.
