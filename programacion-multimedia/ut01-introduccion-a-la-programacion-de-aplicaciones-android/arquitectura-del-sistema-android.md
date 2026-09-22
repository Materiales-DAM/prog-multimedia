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

# Arquitectura del sistema Android

La arquitectura de Android está diseñada de manera modular y se organiza en varias capas que interactúan entre sí para proporcionar una plataforma eficiente y flexible para el desarrollo y ejecución de aplicaciones móviles.&#x20;

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Arquitectura de Android</p></figcaption></figure>

A continuación, se describe cada una de estas capas, desde la base hasta la capa más alta, que es la interfaz de usuario:

## 1. **Kernel de Linux**

En la base de la arquitectura de Android se encuentra el **kernel de Linux**, que actúa como la capa de abstracción entre el hardware y el software. Esta capa proporciona funcionalidades esenciales, como:

* **Administración de procesos**: Controla la ejecución de las aplicaciones y gestiona los recursos.
* **Manejo de memoria**: Asigna y administra la memoria disponible.
* **Drivers de hardware**: Incluye controladores para interactuar con el hardware del dispositivo, como la pantalla, cámara, Wi-Fi, Bluetooth, sensores, etc.
* **Seguridad**: Proporciona un entorno seguro mediante permisos de acceso, y es fundamental para las medidas de seguridad de Android, como el modelo de usuario privilegiado.

## 2. **Bibliotecas nativas**

Encima del kernel de Linux, Android tiene un conjunto de **bibliotecas nativas** escritas principalmente en C y C++. Estas bibliotecas proporcionan las funciones esenciales para varias características del sistema, como:

* **Biblioteca de gráficos**: OpenGL ES y Skia, utilizadas para renderizar gráficos 2D y 3D.
* **Bibliotecas multimedia**: Para la reproducción y grabación de audio y video.
* **SQLite**: Base de datos ligera y local utilizada para almacenamiento de datos estructurados en aplicaciones.
* **LibC**: La implementación estándar de C para la ejecución de aplicaciones Android.
* **SSL**: Proporciona comunicación segura sobre la red.

## 3. **Android Runtime (ART)**

Android Runtime (ART) es la máquina virtual en la que se ejecutan las aplicaciones Android. Anteriormente, se utilizaba la **Dalvik VM**, pero ART la ha reemplazado en las versiones más recientes de Android. Sus funciones principales incluyen:

* **Compilación JIT y AOT**: ART utiliza la compilación Just-In-Time (JIT) y Ahead-Of-Time (AOT) para optimizar el rendimiento de las aplicaciones. AOT precompila las aplicaciones al momento de la instalación, mejorando el rendimiento de ejecución.
* **Gestión de memoria y recolección de basura**: ART se encarga de la gestión de memoria dinámica y automatiza el proceso de recolección de basura para liberar recursos de manera eficiente.

## 4. **Bibliotecas y APIs de Android**

Esta capa incluye un conjunto de bibliotecas desarrolladas en Java, que los desarrolladores de aplicaciones utilizan para interactuar con las características de Android. Proporcionan acceso a una variedad de servicios del sistema, como:

* **Biblioteca de interfaces de usuario**: Incluye componentes como vistas, botones, y listas, necesarios para construir interfaces de usuario.
* **APIs de red**: Para la conexión a Internet, manejo de datos y acceso a recursos en línea.
* **APIs de acceso a hardware**: Permiten a las aplicaciones usar el GPS, la cámara, los sensores del dispositivo, etc.
* **APIs de gráficos**: Para renderizar gráficos y crear interfaces visuales interactivas.

## 5. **Marco de trabajo de aplicaciones (Application Framework)**

El **framework de aplicaciones** es el conjunto de herramientas y servicios que los desarrolladores utilizan para crear aplicaciones. Se encargan de gestionar los componentes esenciales de la interacción del usuario y el sistema, como:

* **Gestor de actividades (Activity Manager)**: Administra el ciclo de vida de las actividades y el historial de navegación entre pantallas.
* **Gestor de recursos (Resource Manager)**: Facilita el acceso a los recursos de la aplicación, como imágenes, cadenas de texto, y archivos XML.
* **Notificaciones (Notification Manager)**: Controla cómo las aplicaciones generan y muestran notificaciones en la barra de estado.
* **Gestor de contenido (Content Provider)**: Permite compartir datos entre aplicaciones a través de un sistema estandarizado de acceso a datos.
* **Gestor de ventanas (Window Manager)**: Controla la disposición de las ventanas y vistas en pantalla.

## 6. **Aplicaciones y capa de interfaz de usuario**

En la capa superior de la arquitectura de Android se encuentran las **aplicaciones** que interactúan directamente con los usuarios. Estas incluyen tanto las aplicaciones del sistema (como teléfono, mensajes, contactos, cámara) como las aplicaciones de terceros instaladas desde la Google Play Store o de otras fuentes. Las aplicaciones acceden a las funciones del sistema a través del framework de aplicaciones, utilizando las APIs y bibliotecas que Android proporciona.
