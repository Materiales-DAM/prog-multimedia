---
cover: ../../../../.gitbook/assets/image (5).png
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

# Arquitectura CLEAN Model-View-ViewModel

La arquitectura **CLEAN MVVM** es un enfoque estructural que separa el código en diferentes capas para lograr un alto grado de modularidad, mantenibilidad y testabilidad. Cada capa tiene responsabilidades específicas y está diseñada para estar lo más desacoplada posible de las demás. A continuación, se explican las capas principales **UI**, **ViewModel**, **UseCases,** **Repository y DataSource**.

<figure><img src="../../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## **1. UI (Capa de Presentación)**

La **UI** es la capa responsable de mostrar la interfaz de usuario y capturar las interacciones del usuario. En Android, puede estar representada por actividades, fragmentos o composables en Jetpack Compose.

**Responsabilidades:**

* Renderizar datos provenientes del `ViewModel`.
* Capturar las acciones del usuario y comunicarlas al `ViewModel`.

**Características:**

* No contiene lógica de negocio, solo lógica relacionada con la interfaz.
* Depende directamente del `ViewModel`.

## **2. ViewModel (Capa de Presentación Intermedia)**

El **ViewModel** actúa como intermediario entre la capa de presentación (View) y la lógica de negocio (UseCases). Su responsabilidad principal es manejar el estado de la interfaz y ejecutar acciones relacionadas con los datos.

**Responsabilidades:**

* Solicitar datos a los `UseCases` y exponerlos en un formato que la `View` pueda consumir.
* Manejar la lógica de presentación, como el control del estado de carga o errores.
* Mantener el estado de la interfaz de usuario.

**Características:**

* No contiene lógica de negocio compleja.
* Utiliza corrutinas (por ejemplo, `viewModelScope`) para tareas asíncronas.
* Expuesto a través de flujos como `StateFlow` o `LiveData`.

## **3. UseCases (Capa de Dominio)**

Los **UseCases** representan la lógica de negocio de la aplicación. Cada UseCase encapsula una acción específica que la aplicación puede realizar desde el punto de vista del negocio.

**Responsabilidades:**

* Implementar la lógica de negocio o reglas de la aplicación.
* Orquestar interacciones entre la capa de datos (`Repository`) y otras dependencias.
* Garantizar que las operaciones realizadas sigan las reglas del dominio.

**Características:**

* Es independiente de la interfaz de usuario y del framework (Android, Compose, etc.).
* Facilita la reutilización en diferentes partes de la aplicación.
* Testeable de forma aislada.

## **4. Repository (Capa de Datos)**

El **Repository** es la capa encargada de acceder a las fuentes de datos, como bases de datos locales, servicios de red (APIs) o cualquier otro almacenamiento.

**Responsabilidades:**

* Proporcionar un acceso abstracto a los datos.
* Decidir la fuente de datos (remota o local) según la lógica definida.
* Transformar los datos en un formato que el dominio pueda usar.

**Características:**

* Implementa una interfaz para desacoplar la fuente de datos de la lógica de negocio.
* Puede combinar múltiples fuentes de datos.
* Contiene lógica específica de acceso a datos.

## **Relaciones entre las Capas**

1. **View → ViewModel:**
   * La `View` se suscribe al estado del `ViewModel` y envía eventos como clics de usuario.
2. **ViewModel → UseCase:**
   * El `ViewModel` llama a los `UseCases` para ejecutar acciones y obtener datos.
3. **UseCase → Repository:**
   * Los `UseCases` utilizan los `Repositories` para acceder a datos.
4. **Repository → Fuente de Datos:**
   * Los `Repositories` interactúan con fuentes como APIs o bases de datos para recuperar o almacenar datos.
