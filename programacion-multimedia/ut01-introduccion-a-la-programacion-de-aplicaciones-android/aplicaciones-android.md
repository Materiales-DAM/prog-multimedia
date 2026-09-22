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

# Aplicaciones Android

## **Componentes principales de una aplicación Android**

Una aplicación Android se compone de varios elementos, cada uno con un propósito específico. Estos son los principales **componentes** de una aplicación Android:

### **Activities (Actividades)**

Una **Activity** es una pantalla de la interfaz de usuario que el usuario ve e interactúa. Cada pantalla en una aplicación generalmente se representa como una actividad independiente.

### **Services (Servicios)**

Un **Service** es un componente que realiza tareas en segundo plano sin necesidad de una interfaz de usuario. Los servicios pueden ejecutarse indefinidamente o por un tiempo limitado.

**Ejemplo**: Un servicio de reproducción de música que continúa funcionando incluso cuando el usuario cambia a otra aplicación.

### **Broadcast Receivers (Receptores de Difusión)**

Un **Broadcast Receiver** responde a eventos del sistema o de otras aplicaciones. Los eventos pueden ser del sistema operativo (como la carga de batería baja) o eventos enviados por otras aplicaciones.

**Ejemplo**: Un receptor que activa una alerta cuando el dispositivo se conecta a una red Wi-Fi.

### **Content Providers (Proveedores de Contenidos)**

Un **Content Provider** gestiona el acceso a los datos entre aplicaciones. Permiten que una aplicación comparta datos con otra, como contactos, imágenes o cualquier otra base de datos estructurada.

**Ejemplo**: El Content Provider del sistema gestiona los contactos del teléfono, permitiendo a varias aplicaciones acceder a los datos de contactos del usuario.

### **Intents (Intenciones)**

Los **Intents** son mensajes que permiten a los componentes de la aplicación comunicarse entre sí o con otras aplicaciones. Pueden usarse para iniciar actividades, enviar datos o ejecutar servicios en segundo plano.

**Ejemplo**: Iniciar la cámara desde una aplicación para tomar una foto y devolverla a la actividad principal.

## **Ciclo de vida de una actividad**

El **ciclo de vida de una actividad** es esencial para gestionar correctamente los recursos y el comportamiento de la aplicación cuando el usuario interactúa con ella. Las actividades pasan por varios estados a medida que se crean, se muestran y se destruyen.&#x20;

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Los estados principales del ciclo de vida son:

### **onCreate()**

Este método es llamado cuando la actividad es creada por primera vez. Aquí es donde se inicializa la interfaz de usuario y se preparan los recursos.

### **onStart()**

La actividad se vuelve visible para el usuario, pero aún no está interactiva. Este método se llama justo antes de que la actividad se muestre al usuario.

### **onResume()**

Aquí es donde la actividad pasa a ser interactiva con el usuario. La actividad está en primer plano y el usuario puede comenzar a interactuar con ella.

### **onPause()**

Este método se llama cuando la actividad está a punto de perder el foco, por ejemplo, cuando el usuario cambia a otra actividad o aplicación. En este estado, se deben guardar los datos y liberar los recursos que no son necesarios.

### **onStop()**

La actividad ya no es visible para el usuario. Aquí puedes liberar recursos pesados (como la memoria o los procesos de red).

### **onDestroy()**

Este es el último método llamado antes de que la actividad sea destruida. Libera todos los recursos que quedan y cierra cualquier tarea en segundo plano.

### Transiciones de estados más habituales

* **onCreate()** → **onStart()** → **onResume()** (la actividad está visible e interactiva)
* Si el usuario cambia de pantalla o la actividad ya no está en primer plano: **onPause()** → **onStop()**
* Si el usuario vuelve a la actividad, se llama nuevamente a **onRestart()** → **onStart()** → **onResume()**.
* Finalmente, si la actividad se cierra o se destruye: **onDestroy()**.
