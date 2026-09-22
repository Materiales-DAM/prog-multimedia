---
hidden: true
cover: ../../../.gitbook/assets/Firebase_Logo.png
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

# Configurar una cuenta de Firebase

{% stepper %}
{% step %}
### Accede a Firebase

Abre tu navegador y ve a [Firebase Console](https://console.firebase.google.com/). Haz clic en el botón **"Comenzar"** o **"Ir a la consola"**.
{% endstep %}

{% step %}
### (Opcional) Crea una cuenta

Si aún no tienes una cuenta, zaz click en "Crear cuenta" y sigue el proceso para configurarla. Si ya tienes cuenta haz login.
{% endstep %}

{% step %}
### Crea un proyecto en Firebase

1. Una vez en la consola de Firebase, haz clic en el botón **"Crear proyecto"**.
2. Asigna un nombre a tu proyecto. Ejemplo: **"MiPrimerProyecto"**.
3. Haz clic en **"Continuar"** y espera a que Firebase cree el proyecto.
{% endstep %}

{% step %}
### Configura tu proyecto

1. Una vez creado el proyecto, serás redirigido al panel de Firebase.
2. Desde el panel, puedes agregar diferentes productos de Firebase a tu proyecto, vamos a agregar los siguientes productos:
   * **Authentication**: Para gestionar usuarios.&#x20;
   * **Cloud Firestore**: Base de datos en tiempo real.
{% endstep %}

{% step %}
### Descarga el fichero de configuración de Firebase

* Haz clic en el ícono de la plataforma Android para agregar Firebase a tu aplicación
* Descarga el archivo de configuración `google-services.json`&#x20;
{% endstep %}
{% endstepper %}
