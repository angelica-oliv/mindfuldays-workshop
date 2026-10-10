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
> **¿Por qué un prompt prescriptivo?** Al guiar a la IA especificando los componentes nativos exactos de Material 3, la tipografía estándar del sistema y las 3 pantallas sin elementos superfluos, el código generado en Android Studio tendrá fidelidad visual idéntica al diseño de Stitch y compilará limpiamente, sin dependencias externas ni complejidades innecesarias en el aula. La clave de API de Gemini nunca debe exponerse en la interfaz de usuario (UI), leyéndose de forma segura a través de `local.properties` y `BuildConfig`.

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
       - Centered column: App title "MINDFULDAYS" (MaterialTheme.typography.labelLarge, primary color) and subtitle "Atitude X de 9" (bodyMedium, muted).
       - Top-right corner: Standard IconButton with Icons.Default.Settings to navigate to SettingsScreen.
   - Central Card (ElevatedCard):
     * Container color white, elevation 4.dp, padded content.
     * Attitude title in bold (headlineMedium, e.g., "Aceitação").
     * Attitude description (bodyLarge, e.g., "Reconheça e acolha o momento presente exatamente como ele é.").
     * Thin HorizontalDivider (color #E8DFD8).
     * AI reflection text block (bodyMedium, italic, displaying generated reflection or default).
     * Primary filled Button with sparkle icon: "✨ Nova Reflexão (Gemini IA)". Shows CircularProgressIndicator when loading.
   - Bottom Action:
     * A single full-width OutlinedButton: "⏱️ Iniciar Timer de Meditação" navigating to TimerScreen.
   - STRICT EXCLUSIONS: Do NOT include bottom navigation bars, profile avatars, greetings, photo banners, audio players, or habit/streak charts.

2. Screen 2: Meditation Timer Screen (TimerScreen.kt)
   - TopAppBar: Title "Timer de Meditação" with back navigation arrow (Icons.AutoMirrored.Filled.ArrowBack).
   - Center Area:
     * Subtitle text: "Concentre-se na respiração" (bodyLarge, muted color).
     * Minimalist circular countdown timer: A clean circular progress ring (Canvas drawArc with stroke width 8.dp: track color #E8DFD8, progress color #6B8E23), large digital countdown text centered inside ("10:00" or mm:ss in headlineLarge/displayMedium), and status text below ("Pausado" / "Em andamento" / "Concluído").
   - Bottom Controls:
     * A centered horizontal Row with exactly two buttons:
       - Reset button: OutlinedIconButton with Icons.Default.Refresh.
       - Play/Pause button: Large FilledIconButton with primary container color and Play/Pause icon.
   - STRICT EXCLUSIONS: Do NOT include multiple timer dials, duration selector chips/pills, background nature sounds, audio pickers, or interval chime settings.

3. Screen 3: Settings Screen (SettingsScreen.kt)
   - TopAppBar: Title "Configurações" with back navigation arrow (Icons.AutoMirrored.Filled.ArrowBack).
   - Section "Lembretes Diários" (titleMedium, primary color):
     * Card (containerColor surface, elevation 2.dp) containing:
       - Row: Text "Lembrete da Atitude Diária" + standard Material 3 Switch (checked by default).
       - Thin HorizontalDivider.
       - Row: Text "Lembrete para Meditar" + standard Material 3 Switch (unchecked by default).
   - Section "Sobre o App" (titleMedium, primary color):
     * Card (containerColor surface, elevation 2.dp) containing:
       - Text "MindfulDays" (titleMedium bold).
       - Text "Versão 1.0 • 9 Atitudes de Jon Kabat-Zinn" (bodyMedium, muted).
   - STRICT EXCLUSIONS: Absolutely NO Gemini API key input field in the UI! (The API key is securely provided via local.properties and BuildConfig.GEMINI_API_KEY in code, never typed by the user in UI). Do NOT include time picker wheel dialogs, sound options, or nested accordions.

CORE ARCHITECTURE & CODE REQUIREMENTS:
- Package: dev.mindfuldays.app
- Clean Architecture with MVVM pattern (MindfulnessViewModel + StateFlow).
- Material Design 3 Theme in ui/theme/ (Color.kt, Theme.kt, Type.kt using system sans-serif fonts).
- Repository & Remote Service:
  * Model: MindfulnessAttitude (id, name, description, dailyReflection).
  * Repository: AttitudeRepository with the 9 Jon Kabat-Zinn attitudes.
  * Remote Service: GeminiApiService configured using BuildConfig.GEMINI_API_KEY (from local.properties).
- Navigation: Standard Compose navigation (or state-driven screen switching) connecting Home, Timer, and Settings.
- Localization: res/values/strings.xml for clean UI text.

Write clean, concise, idiomatic Kotlin and Jetpack Compose code with no unnecessary dependencies.
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
