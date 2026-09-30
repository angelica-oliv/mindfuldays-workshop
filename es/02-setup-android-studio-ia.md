# 🛠️ Módulo 2 — Setup del Proyecto en Android Studio (Versión Estable) con IA

En este segundo módulo, configuraremos el proyecto de la aplicación **MindfulDays** utilizando la versión **Estable de Android Studio**. Utilizaremos la integración nativa con **Gemini en Android Studio** para acelerar la creación de la estructura de la app a partir de los prototipos generados en Stitch.

---

## 💻 2.1. Configuración del Entorno en Android Studio Estable

1. Asegúrate de estar utilizando la versión **Estable** más reciente de Android Studio.
2. Abre Android Studio y ve a **Settings/Preferences → Tools → AI Assistant (Gemini)**.
3. Inicia sesión con tu cuenta de Google y asegúrate de que el asistente **Gemini** esté activado.
4. Para utilizar el generador de proyectos **Create with AI** o el panel del asistente de Gemini:
   * Ve a **New Project** en la pantalla de inicio de Android Studio.
   * Selecciona la plantilla **Empty Activity** (o selecciona la opción **Create with AI...** si está disponible en la barra lateral de plantillas).

---

## 📦 2.2. Definiendo el Nombre del Paquete y la Estructura

Al crear el proyecto, completa los parámetros fundamentales:

* **Name**: `MindfulDays`
* **Package Name**: `dev.mindfuldays.app` (Estándar profesional y recomendado para proyectos open-source / dev).
* **Language**: Kotlin
* **Minimum SDK**: API 24 (Android 7.0 Nougat o superior)
* **Build Configuration Language**: Kotlin DSL (`build.gradle.kts`)

---

## 🤖 2.3. Prompt Multimodal para Gemini en Android Studio

Abre el panel de **Gemini** en Android Studio (**View → Tool Windows → Gemini**) o utiliza la ventana **Create with AI**. Adjunta las capturas de pantalla generadas en **Stitch** y pega el siguiente prompt estructurado:

```text
Create a modern Android application named 'MindfulDays' with package name 'dev.mindfuldays.app' using Jetpack Compose and Material Design 3.

Using the attached UI screenshots generated in Stitch as the visual source of truth, implement the following screens and functionality:

1. Home Screen: Implement a dashboard with a soft sage green (#6B8E23) and warm off-white (#FBF9F5) color palette. Include a top header displaying the current date and the 'Attitude of the Day' (cycling through 9 Jon Kabat-Zinn mindfulness attitudes). Place a central elevated card for daily AI reflections with a prompt button, and a bottom action to open the Timer.

2. Meditation Timer Screen: Implement a circular countdown timer starting at 10:00. Add Play, Pause, and Reset controls with clean Material 3 IconButton composables.

3. Settings Screen: Implement switches for 'Daily Attitude Reminder' and 'Meditation Time' with TimePicker dialogs for scheduling local notifications.

Core Architecture Requirements:
- Use Clean Architecture with MVVM pattern (ViewModel + StateFlow).
- Implement Material Design 3 Theme in ui/theme/ (Color.kt, Theme.kt, Type.kt).
- Create a service interface GeminiApiService for fetching reflections via Google Gemini API.
- Prepare string resources in res/values/strings.xml for Portuguese and English localization.

Ensure code is written in clean, idiomatic Kotlin using jetpack compose state management.
```

---

## 📁 2.4. Visión de la Estructura de Paquetes del Proyecto

Tras la ejecución del prompt y la generación inicial, tu proyecto en `dev.mindfuldays.app` estará organizado de la siguiente forma:

```text
dev.mindfuldays.app/
├── data/
│   ├── model/
│   │   └── MindfulnessAttitude.kt
│   ├── remote/
│   │   └── GeminiApiService.kt
│   └── repository/
│       └── AttitudeRepository.kt
├── ui/
│   ├── home/
│   │   └── HomeScreen.kt
│   ├── timer/
│   │   └── TimerScreen.kt
│   ├── settings/
│   │   └── SettingsScreen.kt
│   ├── theme/
│   │   ├── Color.kt
│   │   ├── Theme.kt
│   │   └── Type.kt
│   └── viewmodel/
│       └── MindfulnessViewModel.kt
└── MainActivity.kt
```

Con la estructura del proyecto sincronizada y compilando en **Android Studio Estable**, avanzamos hacia el **Módulo 3: Directrices con AGENTS.md, Implementación de la UI en Compose e Integración con Gemini API**.
