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

Abre el panel de **Gemini** en Android Studio (**View → Tool Windows → Gemini**) o utiliza la ventana **Create with AI**. Adjunta las capturas de pantalla generadas en **Stitch** y pega el siguiente prompt estructurado y prescriptivo:

> [!TIP]
> **¿Por qué un prompt prescriptivo y con clases en esqueleto?** Al guiar a la IA especificando los componentes nativos exactos de Material 3, la tipografía estándar del sistema y las 3 pantallas sin elementos superfluos, el código generado en Android Studio tendrá fidelidad visual idéntica al diseño de Stitch. Además, al indicarle a la IA que genere clases como `GeminiApiService` y `AttitudeRepository` como esqueletos en blanco (*stubs* con TODOs), garantizamos que el proyecto compile de inmediato con pantallas funcionales, reservando la lógica de negocio y la integración de la API de Gemini para que los estudiantes las construyan paso a paso en los siguientes módulos. La clave de API de Gemini nunca debe exponerse en la interfaz de usuario (UI), leyéndose de forma segura a través de `local.properties` y `BuildConfig`.

```text
You are an expert Android developer. Create a minimalist Android application named 'MindfulDays' with package name 'dev.mindfuldays.app' using Jetpack Compose and Material Design 3.

Use the attached Stitch UI screenshots as the exact visual reference and follow these prescriptive rules:
- UI STYLE & TYPOGRAPHY: Strict minimalist design for a workshop tutorial. Use Android system fonts ONLY (default sans-serif / Roboto). Use native Android Material 3 components ONLY (Button, OutlinedButton, FilledIconButton, OutlinedIconButton, ElevatedCard, Card, TopAppBar, Switch, HorizontalDivider). Do NOT create complex custom UI components.
- COLOR PALETTE:
  * Primary: Sage Green (#6B8E23)
  * Secondary / Divider: Muted Sand (#E8DFD8)
  * Background: Warm Off-White (#FBF9F5)
  * Surface / Cards: Pure White (#FFFFFF)
  * OnBackground / Text: Dark Forest Green (#2C3E35)

IMPLEMENT EXACTLY THESE 3 SCREENS (no more, no less):

1. Screen 1: Home Screen (HomeScreen.kt)
   - Layout: Column with background #FBF9F5, vertical arrangement spaced between.
   - Header (Top):
     * A top Row containing:
       - Centered column: App title "MINDFULDAYS" (MaterialTheme.typography.labelLarge, primary color) and subtitle "Actitud X de 9" (bodyMedium, muted).
       - Top-right corner: Standard IconButton with Icons.Default.Settings to navigate to SettingsScreen.
   - Central Card (ElevatedCard):
     * Container color white, elevation 4.dp, padded content.
     * Attitude title in bold (headlineMedium, e.g., "Aceptación").
     * Attitude description (bodyLarge, e.g., "Reconoce y acoge el momento presente exactamente como es.").
     * Thin HorizontalDivider (color #E8DFD8).
     * AI reflection text block (bodyMedium, italic, displaying generated reflection or default).
     * Primary filled Button with sparkle icon: "✨ Nueva Reflexión (Gemini IA)". Shows CircularProgressIndicator when loading.
   - Bottom Action:
     * A single full-width OutlinedButton: "⏱️ Iniciar Temporizador de Meditación" navigating to TimerScreen.
   - STRICT EXCLUSIONS: Do NOT include bottom navigation bars, profile avatars, greetings, photo banners, audio players, or habit/streak charts.

2. Screen 2: Meditation Timer Screen (TimerScreen.kt)
   - TopAppBar: Title "Temporizador de Meditación" with back navigation arrow (Icons.AutoMirrored.Filled.ArrowBack).
   - Center Area:
     * Subtitle text: "Concéntrate en la respiración" (bodyLarge, muted color).
     * Minimalist circular countdown timer: A clean circular progress ring (Canvas drawArc with stroke width 8.dp: track color #E8DFD8, progress color #6B8E23), large digital countdown text centered inside ("10:00" or mm:ss in headlineLarge/displayMedium), and status text below ("Pausado" / "En curso" / "Completado").
   - Bottom Controls:
     * A centered horizontal Row with exactly two buttons:
       - Reset button: OutlinedIconButton with Icons.Default.Refresh.
       - Play/Pause button: Large FilledIconButton with primary container color and Play/Pause icon.
   - STRICT EXCLUSIONS: Do NOT include multiple timer dials, duration selector chips/pills, background nature sounds, audio pickers, or interval chime settings.

3. Screen 3: Settings Screen (SettingsScreen.kt)
   - TopAppBar: Title "Configuración" with back navigation arrow (Icons.AutoMirrored.Filled.ArrowBack).
   - Section "Recordatorios Diarios" (titleMedium, primary color):
     * Card (containerColor surface, elevation 2.dp) containing:
       - Row: Text "Recordatorio de Actitud Diaria" + standard Material 3 Switch (checked by default).
       - Thin HorizontalDivider.
       - Row: Text "Recordatorio para Meditar" + standard Material 3 Switch (unchecked by default).
   - Section "Acerca de la App" (titleMedium, primary color):
     * Card (containerColor surface, elevation 2.dp) containing:
       - Text "MindfulDays" (titleMedium bold).
       - Text "Versión 1.0 • 9 Actitudes de Jon Kabat-Zinn" (bodyMedium, muted).
   - STRICT EXCLUSIONS: Absolutely NO Gemini API key input field in the UI! (The API key is securely provided via local.properties and BuildConfig.GEMINI_API_KEY in code, never typed by the user in UI). Do NOT include time picker wheel dialogs, sound options, or nested accordions.

EXPECTED FINAL PACKAGE STRUCTURE:
Organize all generated code cleanly under the root package 'dev.mindfuldays.app':
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

INITIAL IMPLEMENTATION STATUS (WORKSHOP PROGRESSION & BLANK SKELETON CLASSES):
Since this project will be built progressively across workshop modules, generate classes with the following implementation levels:

1. FULLY IMPLEMENTED NOW (UI & Design Tokens):
   - ui/theme/ (Color.kt, Theme.kt, Type.kt): Fully implemented with the required Material 3 color tokens and system fonts.
   - ui/home/HomeScreen.kt, ui/timer/TimerScreen.kt, ui/settings/SettingsScreen.kt: Fully implement the declarative Composable layouts according to the exact screen specifications above.
   - data/model/MindfulnessAttitude.kt: Data class fully defined:
     data class MindfulnessAttitude(val id: Int, val name: String, val description: String, val dailyReflection: String)
   - MainActivity.kt: Simple state-based navigation switching between HomeScreen, TimerScreen, and SettingsScreen.

2. GENERATE AS EMPTY SKELETONS / STUBS (TO BE FILLED IN SUBSEQUENT WORKSHOP STEPS):
   - data/remote/GeminiApiService.kt: Generate as a BLANK/EMPTY interface skeleton with a simple stub and a TODO comment (do NOT implement API calls yet, students will implement this in Module 3):
     // TODO: Implement Google Gemini API call with generativeai SDK in Module 3
     interface GeminiApiService {
         suspend fun generateDailyReflection(attitude: String): String = ""
     }
   - data/repository/AttitudeRepository.kt: Generate as a SKELETON class stub with placeholder method signatures and a TODO comment:
     // TODO: Implement 9 Jon Kabat-Zinn attitudes & offline fallback logic in Module 3
     class AttitudeRepository(private val apiService: GeminiApiService? = null) {
         fun getAttitudeOfTheDay(): MindfulnessAttitude = MindfulnessAttitude(1, "Aceptación", "Reconoce y acoge el momento presente.", "Reflexión inicial.")
         suspend fun getAiReflection(attitude: String): String = "Reflexión temporal de ejemplo."
     }
   - ui/viewmodel/MindfulnessViewModel.kt: Generate as an INITIAL SKELETON ViewModel with basic StateFlow and placeholder state values just enough to preview and run the UI without crashing:
     // TODO: Bind coroutines, offline caching and real Gemini API integration in Module 3

Write clean, concise, idiomatic Kotlin and Jetpack Compose code with no unnecessary dependencies.
```

---

## 📁 2.4. Visión de la Estructura de Paquetes del Proyecto

Tras la ejecución del prompt y la generación inicial, tu proyecto en `dev.mindfuldays.app` estará organizado de la siguiente forma:

```text
dev.mindfuldays.app/
├── data/
│   ├── model/
│   │   └── MindfulnessAttitude.kt    <- Data class con los atributos de la actitud
│   ├── remote/
│   │   └── GeminiApiService.kt       <- Esqueleto / Stub vacío (implementado en el Módulo 3)
│   └── repository/
│       └── AttitudeRepository.kt     <- Esqueleto con firmas (implementado en el Módulo 3)
├── ui/
│   ├── home/
│   │   └── HomeScreen.kt             <- Layout Compose completo y funcional
│   ├── timer/
│   │   └── TimerScreen.kt            <- Layout Compose completo y funcional
│   ├── settings/
│   │   └── SettingsScreen.kt         <- Layout Compose completo y funcional
│   ├── theme/
│   │   ├── Color.kt                  <- Tokens Material 3 oficiales (Salvia, Arena, Blanco Cálido)
│   │   ├── Theme.kt
│   │   └── Type.kt
│   └── viewmodel/
│       └── MindfulnessViewModel.kt   <- Esqueleto inicial de estado para la UI
└── MainActivity.kt                   <- Punto de entrada y navegación básica entre pantallas
```

Con la estructura del proyecto sincronizada y compilando en **Android Studio Estable**, avanzamos hacia el **Módulo 3: Directrices con AGENTS.md, Implementación de la UI en Compose e Integración con Gemini API**.
