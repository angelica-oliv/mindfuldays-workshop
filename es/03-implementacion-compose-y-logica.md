# 🧩 Módulo 3 — UI en Jetpack Compose, Regla de las 9 Actitudes y Gemini API

En este módulo, estructuraremos el archivo **AGENTS.md** para proporcionar el contexto operacional a agentes de IA, implementaremos la lógica de negocio de la aplicación **MindfulDays**, configuraremos el tema Material Design 3 y construiremos las pantallas con **Jetpack Compose**.

---

## 🤖 3.1. Directrices para Agentes de IA: Creación del Archivo `AGENTS.md`

Antes de iniciar la implementación del código y las pantallas, configuraremos uno de los recursos más estratégicos para el desarrollo moderno orientado por inteligencia artificial: el archivo **`AGENTS.md`**.

### 🌟 ¿Por qué es tan importante `AGENTS.md`?

Así como el `README.md` orienta a las personas desarrolladoras sobre el proyecto, el **`AGENTS.md`** es una convención abierta adoptada por la comunidad para actuar como la **fuente única de verdad operacional para agentes autónomos y asistentes de código con IA** (como Gemini en Android Studio, Cursor, Claude Code, GitHub Copilot Workspace y Antigravity).

Al trabajar con IA en el desarrollo móvil, el mayor reto no es la capacidad de generar código, sino la **precisión y adherencia al contexto**. Sin instrucciones explícitas, los modelos de IA pueden sufrir de alucinaciones, sugerir dependencias incompatibles, mezclar código heredado (como layouts XML antiguos en lugar de Jetpack Compose) o romper patrones arquitectónicos.

`AGENTS.md` resuelve estos desafíos proporcionando:

1. **Grounding y Reducción Drástica de Alucinaciones**: El archivo ancla a la IA en las decisiones técnicas ya tomadas, eliminando suposiciones y manteniendo al agente enfocado en las directrices exactas del proyecto.
2. **Consistencia de Stack y Arquitectura**: Garantiza que cualquier código generado respete estrictamente el patrón **MVVM**, **Clean Architecture**, **Kotlin idiomático** y **Jetpack Compose con Material Design 3**.
3. **Fidelidad a los Design Tokens y Reglas de Negocio**: La IA tendrá siempre a mano la paleta de colores oficial extraída en Stitch (`SageGreen`, `SandMuted`, etc.) y la lógica de rotación cíclica de las 9 actitudes de Jon Kabat-Zinn.
4. **Guardrails de Seguridad**: Define límites esenciales, como la prohibición explícita de incluir claves secretas (`apiKey`) hardcodeadas o acoplar lógica de dominio dentro de funciones composables.
5. **Autonomía en Ejecución y Auto-corrección (Self-Healing)**: Especifica los comandos exactos de compilación, lint y pruebas (`./gradlew assembleDebug`, `./gradlew testDebugUnitTest`), permitiendo que agentes autónomos ejecuten, validen y corrijan posibles fallos antes de finalizar una tarea.
6. **Ahorro de Contexto y Tokens**: Elimina la necesidad de repetir prompts gigantescos en cada nueva pantalla o funcionalidad solicitada.

---

### 📝 Creando el archivo `AGENTS.md`

Crea el archivo `AGENTS.md` directamente en la **raíz de tu proyecto Android** (`MindfulDays/AGENTS.md`):

```markdown
# 🧘 MindfulDays — Directrices y Contexto para Agentes de IA

Este archivo actúa como la fuente de verdad para agentes de IA y herramientas de asistencia de código que operan en este repositorio.

## 📱 Visión General del Proyecto
**MindfulDays** es una aplicación Android nativa enfocada en mindfulness y bienestar mental, basada en las **9 Actitudes de Mindfulness de Jon Kabat-Zinn**, con soporte para reflexiones diarias generadas mediante la **Google Gemini API** y un temporizador circular de meditación.

## 🏗️ Patrones de Arquitectura y Stack Técnico
- **Lenguaje**: Kotlin 1.9+ (uso idiomático de coroutines, StateFlow e inmutabilidad).
- **UI Toolkit**: Jetpack Compose con Material Design 3 (M3). **Prohibido el uso de layouts XML tradicionales**.
- **Patrón de Arquitectura**: MVVM (Model-View-ViewModel) alineado con Clean Architecture:
  - `data/model/`: Data classes inmutables.
  - `data/repository/`: Repositorios para fuente de datos local y lógica de las 9 actitudes.
  - `data/remote/`: Clientes y servicios para comunicación con la Gemini API.
  - `ui/`: Pantallas y componentes en Compose divididos por feature (`home`, `timer`, `settings`).
  - `ui/theme/`: Tokens visuales (Color, Theme, Type).
  - `ui/viewmodel/`: ViewModels que exponen estados mediante `StateFlow`.
- **Paquete Base**: `dev.mindfuldays.app`.

## 🎨 Design Tokens & Temas (Material Design 3 — Light & Dark Mode)
Respeta estrictamente los tokens semánticos de colores de Material 3, garantizando soporte perfecto y contraste adecuado tanto en tema claro como oscuro:

### Tema Claro (Light Theme):
- `primary`: Verde Salvia (`#6B8E23`)
- `primaryContainer`: Salvia Suave (`#8FA853`)
- `secondary`: Arena Muted (`#E8DFD8`)
- `background`: Blanco Cálido (`#FBF9F5`)
- `surface`: Blanco Puro (`#FFFFFF`)
- `onBackground` / `onSurface`: Verde Bosque Oscuro (`#2C3E35`)
- `onSurfaceVariant`: Verde Bosque Suave (`#5C6F64`)
- `outlineVariant`: Arena Muted (`#E8DFD8`)

### Tema Oscuro (Dark Theme):
- `primary`: Salvia Luminoso (`#A8C673`)
- `primaryContainer`: Bosque Oscuro Elevado (`#2E4239`)
- `secondary`: Salvia Suave (`#A3B5A8`)
- `background`: Bosque Nocturno Profundo (`#15201A`)
- `surface`: Bosque Nocturno Elevado (`#22322A`)
- `onBackground` / `onSurface`: Blanco Cálido Claro (`#F1EFEA`)
- `onSurfaceVariant`: Salvia Muted Claro (`#A3B5A8`)
- `outlineVariant`: Borde Sutil de Bosque (`#3B5045`)

## 🧠 Reglas de Negocio Fundamentales
1. **Regla de las 9 Actitudes**: La lista contiene exactamente 9 actitudes fijas. La actitud del día se calcula determinísticamente a partir del día del año:
   `val index = (Calendar.getInstance().get(Calendar.DAY_OF_YEAR) - 1) % 9`
2. **Gemini API (Reflexiones Diarias)**:
   - Utilizar el endpoint del modelo `gemini-3.8-flash:generateContent`.
   - Generar reflexiones concisas e inspiradoras con un máximo de 2 oraciones por actitud, respetando el idioma del usuario (pt, en, es).
   - Manejar la ausencia de clave de API y errores de red con un mensaje amigable offline sin romper la app.

## 🛠️ Comandos de Verificación e Validación
Verifica siempre los cambios utilizando los siguientes comandos en la terminal:
- **Compilación de la app**: `./gradlew assembleDebug`
- **Pruebas Unitarias**: `./gradlew testDebugUnitTest`
- **Pruebas de UI (Robot Pattern)**: `./gradlew connectedDebugAndroidTest`

## 🚫 Restricciones Estrictas (Guardrails)
- **NUNCA utilices colores hexadecimales hardcodeados en Composables** (`Color(0xFF...)`). Utiliza siempre `MaterialTheme.colorScheme.background`, `MaterialTheme.colorScheme.surface`, `MaterialTheme.colorScheme.onSurface`, etc., para evitar problemas de contraste en el Modo Oscuro.
- **NUNCA** hagas commit ni dejes credenciales o claves de API (`apiKey`) en el código versionado. La clave debe configurarse en `local.properties` y consumirse mediante `BuildConfig.GEMINI_API_KEY`.
- **NO** mezcles lógica de negocio o llamadas asíncronas de red directamente dentro de funciones `@Composable`.
- Mantén las funciones Composable limpias y desacopladas, utilizando parámetros para eventos y lambdas (`onAction: () -> Unit`) para facilitar pruebas de UI.
- Utiliza nombres descriptivos en español para textos de interfaz visible e inglés para código técnico, métodos e interfaces.
```

Con `AGENTS.md` configurado en la raíz del proyecto, cualquier agente (como Gemini en Android Studio) producirá código perfectamente alineado con tu sistema de diseño y tus reglas de negocio.

---

## 🔑 3.2. Configuración de Gemini API y Gestión Segura de Credenciales

Para integrar la **Gemini API** en la aplicación de forma robusta, moderna y directa, utilizamos peticiones REST mediante **Retrofit**, **Moshi** y **OkHttp** conectando al endpoint oficial del modelo **`gemini-3.8-flash`**.

A continuación se presentan los pasos esenciales y las mejores prácticas para evitar errores comunes de permisos, activación y seguridad:

### 1. Obtención de la API Key en Google AI Studio
1. Ingresa a [Google AI Studio](https://aistudio.google.com/) e inicia sesión con tu cuenta de Google.
2. Haz clic en **Get API key** (Obtener clave de API) y crea una nueva clave en un proyecto nuevo o existente.
3. Copia la clave generada.

> [!WARNING]
> **Trampa Común — Claves de Firebase (`API_KEY_SERVICE_BLOCKED` 403):**
> Nunca utilices claves de API generadas automáticamente por Firebase con restricciones para aplicaciones Android para llamar al endpoint de Gemini API. Dichas claves cuentan con restricciones de alcance y generan el error:
> `403 PERMISSION_DENIED: Requests to this API generativelanguage.googleapis.com method ... are blocked (API_KEY_SERVICE_BLOCKED)`.
> Utiliza siempre una clave generada directamente en **Google AI Studio** o en Google Cloud con la API habilitada.

### 2. Activación de la Generative Language API en Google Cloud
Incluso con una clave válida generada, si el proyecto de Google Cloud asociado a tu clave aún no tiene la API habilitada, las llamadas serán rechazadas con el error:
`403 FORBIDDEN: Generative Language API has not been used in project ... or it is disabled (SERVICE_DISABLED)`.

Para activarla:
1. Accede a la consola de Google Cloud a través del enlace proporcionado en el propio mensaje de error o en:
   `https://console.developers.google.com/apis/api/generativelanguage.googleapis.com/overview?project=<TU_PROJECT_ID>`
2. Haz clic en el botón **Habilitar** (Enable). La activación toma solo unos segundos en propagarse.

### 3. Almacenamiento Seguro en `local.properties` (Guardrail de Seguridad)
Siguiendo las directrices de seguridad del proyecto (`AGENTS.md`), **NUNCA hagas commit de claves de API en Git** ni coloques la clave hardcodeada en el código Kotlin.

Abre el archivo `local.properties` en la raíz del proyecto (que ya se encuentra ignorado por el `.gitignore`) y agrega:

```properties
GEMINI_API_KEY=tu_clave_de_ai_studio_aqui
```

### 4. Inyección de la Clave vía `buildConfigField` en `app/build.gradle.kts`
Para que el código Kotlin tenga acceso seguro a la clave durante la compilación, configuramos Gradle para cargar `local.properties` y generar la constante en `BuildConfig`.

En el archivo `app/build.gradle.kts`:

```kotlin
import java.util.Properties

// Carga las variables de local.properties
val localProperties = Properties()
val localPropertiesFile = rootProject.file("local.properties")
if (localPropertiesFile.exists()) {
    localPropertiesFile.inputStream().use { localProperties.load(it) }
}
val geminiApiKey: String = localProperties.getProperty("GEMINI_API_KEY") ?: ""

android {
    ...
    defaultConfig {
        ...
        // Inyecta la clave de forma segura en BuildConfig
        buildConfigField("String", "GEMINI_API_KEY", "\"$geminiApiKey\"")
    }

    buildFeatures {
        compose = true
        buildConfig = true // Habilita la generación de la clase BuildConfig
    }
}
```

### 5. Dependencias de Gradle (Retrofit, Moshi y OkHttp)
Para realizar la comunicación HTTP asíncrona y la serialización JSON de forma performante, agrega las dependencias en tu proyecto:

En el archivo `gradle/libs.versions.toml`:
```toml
[versions]
retrofit = "3.0.0"
converterMoshi = "3.0.0"
okhttp = "5.3.2"
loggingInterceptor = "5.3.2"
moshiKotlin = "1.15.2"
moshiKotlinCodegen = "1.15.2"

[libraries]
retrofit = { group = "com.squareup.retrofit2", name = "retrofit", version.ref = "retrofit" }
converter-moshi = { group = "com.squareup.retrofit2", name = "converter-moshi", version.ref = "converterMoshi" }
okhttp = { group = "com.squareup.okhttp3", name = "okhttp", version.ref = "okhttp" }
logging-interceptor = { group = "com.squareup.okhttp3", name = "logging-interceptor", version.ref = "loggingInterceptor" }
moshi-kotlin = { group = "com.squareup.moshi", name = "moshi-kotlin", version.ref = "moshiKotlin" }
moshi-kotlin-codegen = { group = "com.squareup.moshi", name = "moshi-kotlin-codegen", version.ref = "moshiKotlinCodegen" }
```

En el archivo `app/build.gradle.kts`:
```kotlin
plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.kotlin.compose)
    alias(libs.plugins.google.devtools.ksp)
}

dependencies {
    // Networking y Gemini API
    implementation(libs.retrofit)
    implementation(libs.converter.moshi)
    implementation(libs.moshi.kotlin)
    implementation(libs.okhttp)
    implementation(libs.logging.interceptor)
    "ksp"(libs.moshi.kotlin.codegen)
}
```

---

## 🌐 3.3. Internacionalización (i18n): Soporte Multi-idioma (Inglés, Español y Portugués)

Una de las mejores prácticas esenciales del desarrollo en Android es nunca dejar textos visibles fijos (*hardcoded*) en código Kotlin ni en funciones Composable. Además de facilitar las pruebas y el mantenimiento, esto permite que la aplicación se adapte instantáneamente al idioma configurado en el dispositivo del usuario.

En Android, los recursos de texto residen en `app/src/main/res/values`:
- `values/strings.xml`: Tabla predeterminada (fallback internacional en Inglés).
- `values-es/strings.xml`: Tabla específica para Español.
- `values-pt/strings.xml`: Tabla específica para Portugués.

### 1. `app/src/main/res/values/strings.xml` (Predeterminado / Inglés)
```xml
<resources>
    <string name="app_name">MindfulDays</string>
    <string name="app_title">MINDFULDAYS</string>
    <string name="attitude_counter">Attitude %1$d of %2$d</string>

    <!-- Home Screen -->
    <string name="default_reflection">“Take a deep breath and bring your awareness to the present moment.”</string>
    <string name="btn_new_reflection">✨ New Reflection (Gemini AI)</string>
    <string name="btn_start_timer">⏱️ Start Meditation Timer</string>

    <!-- Timer Screen -->
    <string name="timer_title">Meditation Timer</string>
    <string name="timer_subtitle">Focus on your breath</string>
    <string name="timer_session_guided">• GUIDED SESSION</string>
    <string name="timer_status_completed">Completed</string>
    <string name="timer_status_running">In progress</string>
    <string name="timer_status_paused">Paused</string>

    <!-- Settings Screen -->
    <string name="settings_title">Settings</string>
    <string name="settings_section_reminders">Daily Reminders</string>
    <string name="settings_daily_reminder">Daily Attitude Reminder</string>
    <string name="settings_meditate_reminder">Meditation Reminder</string>
    <string name="settings_section_about">About the App</string>
    <string name="settings_version_info">Version 1.0 • 9 Jon Kabat-Zinn Attitudes</string>

    <!-- Accessibility Content Descriptions -->
    <string name="cd_settings">Settings</string>
    <string name="cd_back">Back</string>
    <string name="cd_reset">Reset</string>
    <string name="cd_play">Start</string>
    <string name="cd_pause">Pause</string>

    <!-- The 9 Attitudes -->
    <string name="attitude_1_name">Beginner\'s Mind</string>
    <string name="attitude_1_desc">Look at things as if for the first time, free from expectations.</string>
    <string name="attitude_2_name">Non-Judging</string>
    <string name="attitude_2_desc">Observe your thoughts and feelings without labeling them good or bad.</string>
    <string name="attitude_3_name">Acceptance</string>
    <string name="attitude_3_desc">Acknowledge and embrace the present moment exactly as it is.</string>
    <string name="attitude_4_name">Letting Go</string>
    <string name="attitude_4_desc">Release thoughts and desires that attempt to capture your attention.</string>
    <string name="attitude_5_name">Trust</string>
    <string name="attitude_5_desc">Develop a basic belief in yourself and in your body\'s signals.</string>
    <string name="attitude_6_name">Non-Striving</string>
    <string name="attitude_6_desc">Abandon the constant need to achieve an immediate result.</string>
    <string name="attitude_7_name">Patience</string>
    <string name="attitude_7_desc">Understand that certain things need time to develop naturally.</string>
    <string name="attitude_8_name">Gratitude</string>
    <string name="attitude_8_desc">Appreciate the present moment and value what you already have.</string>
    <string name="attitude_9_name">Generosity</string>
    <string name="attitude_9_desc">Offer attention, warmth, and presence with an open heart.</string>
</resources>
```

### 2. `app/src/main/res/values-es/strings.xml` (Español)
```xml
<resources>
    <string name="app_name">MindfulDays</string>
    <string name="app_title">MINDFULDAYS</string>
    <string name="attitude_counter">Actitud %1$d de %2$d</string>

    <!-- Home Screen -->
    <string name="default_reflection">“Respira profundo y trae tu atención al momento presente.”</string>
    <string name="btn_new_reflection">✨ Nueva Reflexión (Gemini IA)</string>
    <string name="btn_start_timer">⏱️ Iniciar Temporizador de Meditación</string>

    <!-- Timer Screen -->
    <string name="timer_title">Temporizador de Meditación</string>
    <string name="timer_subtitle">Concéntrate en la respiración</string>
    <string name="timer_session_guided">• SESIÓN GUIADA</string>
    <string name="timer_status_completed">Completado</string>
    <string name="timer_status_running">En curso</string>
    <string name="timer_status_paused">Pausado</string>

    <!-- Settings Screen -->
    <string name="settings_title">Configuración</string>
    <string name="settings_section_reminders">Recordatorios Diarios</string>
    <string name="settings_daily_reminder">Recordatorio de Actitud Diaria</string>
    <string name="settings_meditate_reminder">Recordatorio para Meditar</string>
    <string name="settings_section_about">Acerca de la App</string>
    <string name="settings_version_info">Versión 1.0 • 9 Actitudes de Jon Kabat-Zinn</string>

    <!-- Accessibility Content Descriptions -->
    <string name="cd_settings">Configuración</string>
    <string name="cd_back">Volver</string>
    <string name="cd_reset">Reiniciar</string>
    <string name="cd_play">Iniciar</string>
    <string name="cd_pause">Pausar</string>

    <!-- The 9 Attitudes -->
    <string name="attitude_1_name">Mente de Principiante</string>
    <string name="attitude_1_desc">Mira las cosas como si fuera la primera vez, libre de expectativas.</string>
    <string name="attitude_2_name">No Juicio</string>
    <string name="attitude_2_desc">Observa tus pensamientos e sentimientos sin etiquetarlos como buenos o malos.</string>
    <string name="attitude_3_name">Aceptación</string>
    <string name="attitude_3_desc">Reconoce y acoge el momento presente exactamente como es.</string>
    <string name="attitude_4_name">Desapego</string>
    <string name="attitude_4_desc">Deja ir los pensamientos y deseos que intentan atrapar tu atención.</string>
    <string name="attitude_5_name">Confianza</string>
    <string name="attitude_5_desc">Desarrolla una creencia básica en ti mismo y en las señales de tu cuerpo.</string>
    <string name="attitude_6_name">No Esforzarse</string>
    <string name="attitude_6_desc">Abandona la necesidad constante de alcanzar un resultado inmediato.</string>
    <string name="attitude_7_name">Paciencia</string>
    <string name="attitude_7_desc">Comprende que ciertas cosas necesitan tiempo para desarrollarse.</string>
    <string name="attitude_8_name">Gratitud</string>
    <string name="attitude_8_desc">Aprecia el momento presente y valora lo que ya posees.</string>
    <string name="attitude_9_name">Generosidad</string>
    <string name="attitude_9_desc">Ofrece atención, cariño y presencia con el corazón abierto.</string>
</resources>
```

### 3. `app/src/main/res/values-pt/strings.xml` (Portugués)
```xml
<resources>
    <string name="app_name">MindfulDays</string>
    <string name="app_title">MINDFULDAYS</string>
    <string name="attitude_counter">Atitude %1$d de %2$d</string>

    <!-- Home Screen -->
    <string name="default_reflection">“Respire fundo e traga sua atenção para o momento presente.”</string>
    <string name="btn_new_reflection">✨ Nova Reflexão (Gemini IA)</string>
    <string name="btn_start_timer">⏱️ Iniciar Timer de Meditação</string>

    <!-- Timer Screen -->
    <string name="timer_title">Timer de Meditação</string>
    <string name="timer_subtitle">Concentre-se na respiração</string>
    <string name="timer_session_guided">• SESSÃO GUIADA</string>
    <string name="timer_status_completed">Concluído</string>
    <string name="timer_status_running">Em andamento</string>
    <string name="timer_status_paused">Pausado</string>

    <!-- Settings Screen -->
    <string name="settings_title">Configurações</string>
    <string name="settings_section_reminders">Lembretes Diários</string>
    <string name="settings_daily_reminder">Lembrete da Atitude Diária</string>
    <string name="settings_meditate_reminder">Lembrete para Meditar</string>
    <string name="settings_section_about">Sobre o App</string>
    <string name="settings_version_info">Versão 1.0 • 9 Atitudes de Jon Kabat-Zinn</string>

    <!-- Accessibility Content Descriptions -->
    <string name="cd_settings">Configurações</string>
    <string name="cd_back">Voltar</string>
    <string name="cd_reset">Reiniciar</string>
    <string name="cd_play">Iniciar</string>
    <string name="cd_pause">Pausar</string>

    <!-- The 9 Attitudes -->
    <string name="attitude_1_name">Mente de Principiante</string>
    <string name="attitude_1_desc">Olhe para as coisas como se fosse a primeira vez, livre de expectativas.</string>
    <string name="attitude_2_name">Não-Julgamento</string>
    <string name="attitude_2_desc">Observe seus pensamentos e sentimentos sem rotulá-los como bons ou ruins.</string>
    <string name="attitude_3_name">Aceitação</string>
    <string name="attitude_3_desc">Reconheça e acolha o momento presente exatamente como ele é.</string>
    <string name="attitude_4_name">Desapego</string>
    <string name="attitude_4_desc">Deixe ir pensamentos e desejos que tentam prender sua atenção.</string>
    <string name="attitude_5_name">Confiança</string>
    <string name="attitude_5_desc">Desenvolva uma crença básica em si mesmo e nos seus sinais corporais.</string>
    <string name="attitude_6_name">Não-Esforço</string>
    <string name="attitude_6_desc">Abandone a necessidade constante de alcançar um resultado imediato.</string>
    <string name="attitude_7_name">Paciência</string>
    <string name="attitude_7_desc">Compreenda que certas coisas precisam de tempo para se desenvolver.</string>
    <string name="attitude_8_name">Gratidão</string>
    <string name="attitude_8_desc">Aprecie o momento presente e valorize o que você já possui.</string>
    <string name="attitude_9_name">Generosidade</string>
    <string name="attitude_9_desc">Ofereça atenção, carinho e presença com o coração aberto.</string>
</resources>
```

---

## 🧠 3.4. Repositorio y Modelo de las 9 Actitudes con Internacionalización

La data class `MindfulnessAttitude` en `dev/mindfuldays/app/data/model/MindfulnessAttitude.kt` encapsula los atributos esenciales de cada actitud, incluyendo anotaciones `@StringRes` para referenciar los recursos de cadenas:

```kotlin
package dev.mindfuldays.app.data.model

import androidx.annotation.StringRes

data class MindfulnessAttitude(
    val id: Int,
    val name: String = "",
    val description: String = "",
    @get:StringRes val nameRes: Int = 0,
    @get:StringRes val descriptionRes: Int = 0
)
```

Ahora, implementa la clase de repositorio en `dev/mindfuldays/app/data/repository/AttitudeRepository.kt` mapeando cada actitud con su respectivo recurso de texto:

```kotlin
package dev.mindfuldays.app.data.repository

import dev.mindfuldays.app.R
import dev.mindfuldays.app.data.model.MindfulnessAttitude
import java.util.Calendar

class AttitudeRepository {

    val attitudes = listOf(
        MindfulnessAttitude(1, "Mente de Principiante", "Mira las cosas como si fuera la primera vez, libre de expectativas.", R.string.attitude_1_name, R.string.attitude_1_desc),
        MindfulnessAttitude(2, "No Juicio", "Observa tus pensamientos e sentimientos sin etiquetarlos como buenos o malos.", R.string.attitude_2_name, R.string.attitude_2_desc),
        MindfulnessAttitude(3, "Aceptación", "Reconoce y acoge el momento presente exactamente como es.", R.string.attitude_3_name, R.string.attitude_3_desc),
        MindfulnessAttitude(4, "Desapego", "Deja ir los pensamientos y deseos que intentan atrapar tu atención.", R.string.attitude_4_name, R.string.attitude_4_desc),
        MindfulnessAttitude(5, "Confianza", "Desarrolla una creencia básica en ti mismo y en las señales de tu cuerpo.", R.string.attitude_5_name, R.string.attitude_5_desc),
        MindfulnessAttitude(6, "No Esforzarse", "Abandona la necesidad constante de alcanzar un resultado inmediato.", R.string.attitude_6_name, R.string.attitude_6_desc),
        MindfulnessAttitude(7, "Paciencia", "Comprende que ciertas cosas necesitan tiempo para desarrollarse.", R.string.attitude_7_name, R.string.attitude_7_desc),
        MindfulnessAttitude(8, "Gratitud", "Aprecia el momento presente y valora lo que ya posees.", R.string.attitude_8_name, R.string.attitude_8_desc),
        MindfulnessAttitude(9, "Generosidad", "Ofrece atención, cariño y presencia con el corazón abierto.", R.string.attitude_9_name, R.string.attitude_9_desc)
    )

    fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude {
        val index = (dayOfYear - 1).mod(attitudes.size)
        return attitudes[index]
    }
}
```

---

## 🤖 3.4. Integración con Gemini API vía Retrofit y Moshi (`GeminiApiService.kt`)

Ahora implementaremos el servicio de red y el ViewModel para conectar la interfaz con la **Gemini API**.

> [!IMPORTANT]
> **Atención al Modelo (`gemini-3.8-flash`):**
> Modelos anteriores como `gemini-1.5-flash` o `gemini-2.5-flash` han sido descontinuados para nuevas claves en el endpoint `v1beta`, devolviendo el error HTTP 404 (`"This model is no longer available to new users"`).
> El modelo actualizado y recomendado para respuestas ágiles de texto es **`gemini-3.8-flash`**.
>
> **Atención a la Serialización con Moshi en Kotlin:**
> Al utilizar Moshi en Android, anota todas las clases de transferencia de datos con `@JsonClass(generateAdapter = true)` y configura `KotlinJsonAdapterFactory()` en el builder de Moshi. De lo contrario, Moshi intentará utilizar la reflexión estándar de Java, produciendo una excepción silenciosa de serialización en tiempo de ejecución.

Crea el archivo en `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:

```kotlin
package dev.mindfuldays.app.data.remote

import dev.mindfuldays.app.BuildConfig
import kotlinx.coroutines.CancellationException
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.withContext
import okhttp3.OkHttpClient
import okhttp3.logging.HttpLoggingInterceptor
import retrofit2.Retrofit
import com.squareup.moshi.JsonClass
import com.squareup.moshi.Moshi
import com.squareup.moshi.kotlin.reflect.KotlinJsonAdapterFactory
import retrofit2.converter.moshi.MoshiConverterFactory
import retrofit2.http.Body
import retrofit2.http.POST
import retrofit2.http.Query

// Data Transfer Objects (DTOs) con adaptadores generados por Moshi
@JsonClass(generateAdapter = true)
data class GeminiRequest(val contents: List<Content>)

@JsonClass(generateAdapter = true)
data class Content(val parts: List<Part>)

@JsonClass(generateAdapter = true)
data class Part(val text: String)

@JsonClass(generateAdapter = true)
data class GeminiResponse(val candidates: List<Candidate>?)

@JsonClass(generateAdapter = true)
data class Candidate(val content: ContentResponse?)

@JsonClass(generateAdapter = true)
data class ContentResponse(val parts: List<PartResponse>?)

@JsonClass(generateAdapter = true)
data class PartResponse(val text: String?)

// Interfaz Retrofit con el endpoint oficial de gemini-3.8-flash
interface GeminiApi {
    @POST("v1beta/models/gemini-3.8-flash:generateContent")
    suspend fun generateContent(
        @Query("key") apiKey: String,
        @Body request: GeminiRequest
    ): GeminiResponse
}

class GeminiApiService {

    private val api: GeminiApi by lazy {
        // Interceptor de log para depuración en Logcat durante el desarrollo
        val logging = HttpLoggingInterceptor().apply {
            level = HttpLoggingInterceptor.Level.BODY
        }
        val client = OkHttpClient.Builder()
            .addInterceptor(logging)
            .build()

        // Configuración de Moshi con soporte completo a clases Kotlin
        val moshi = Moshi.Builder()
            .addLast(KotlinJsonAdapterFactory())
            .build()

        Retrofit.Builder()
            .baseUrl("https://generativelanguage.googleapis.com/")
            .client(client)
            .addConverterFactory(MoshiConverterFactory.create(moshi))
            .build()
            .create(GeminiApi::class.java)
    }

    /**
     * Genera una reflexión diaria personalizada para la actitud indicada usando el modelo gemini-3.8-flash,
     * adaptando el idioma del prompt y la respuesta para el idioma del usuario (es, en, pt).
     */
    suspend fun generateReflection(
        attitudeTitle: String,
        languageCode: String = java.util.Locale.getDefault().language
    ): String = withContext(Dispatchers.IO) {
        try {
            val apiKey = BuildConfig.GEMINI_API_KEY
            if (apiKey.isBlank()) {
                return@withContext getOfflineFallback(languageCode)
            }

            val (systemInstruction, userPrompt) = when (languageCode.lowercase().take(2)) {
                "en" -> Pair(
                    "You are a calm, wise and welcoming mindfulness assistant in the MindfulDays application. " +
                        "Your purpose is to generate serene reflections to cultivate daily mindfulness based on Jon Kabat-Zinn's 9 attitudes. " +
                        "Always respond with at most 2 short, poetic and inspiring sentences. " +
                        "CRITICAL REQUIREMENT: Your entire response MUST be written in English. " +
                        "Never use complex formatting or markdown, use simple and serene plain text.",
                    "Write an inspiring 2-sentence reflection about the mindfulness attitude: \"$attitudeTitle\".\n" +
                        "Requested Language: English. Please write the entire reflection strictly in English."
                )
                "es" -> Pair(
                    "Eres un asistente sereno, sabio y acogedor de mindfulness en la aplicación MindfulDays. " +
                        "Tu propósito es generar reflexiones breves para cultivar la atención plena diaria según las 9 actitudes de Jon Kabat-Zinn. " +
                        "Responde siempre con un máximo de 2 oraciones breves, poéticas e inspiradoras. " +
                        "REQUISITO OBLIGATORIO: Toda tu respuesta DEBE estar escrita en español. " +
                        "Nunca utilices markdown complejo ni caracteres especiales, utiliza texto plano y sereno.",
                    "Escribe una reflexión inspiradora de 2 oraciones sobre la actitud de mindfulness: \"$attitudeTitle\".\n" +
                        "Idioma solicitado: Español. Por favor, escribe toda la reflexión estrictamente en español."
                )
                else -> Pair(
                    "Você é um assistente calmo, sábio e acolhedor de mindfulness no aplicativo MindfulDays. " +
                        "Seu propósito é gerar reflexões serenas para cultivar a atenção plena no dia a dia com base nas 9 atitudes de Jon Kabat-Zinn. " +
                        "Responda sempre com no máximo 2 frases curtas, poéticas e inspiradoras. " +
                        "REQUISITO OBRIGATÓRIO: Toda a sua resposta DEVE ser gerada em português. " +
                        "Nunca use formatação complexa ou markdown, utilize texto simples e sereno.",
                    "Escreva uma reflexão inspiradora de 2 frases sobre a atitude de mindfulness: \"$attitudeTitle\".\n" +
                        "Idioma solicitado: Português. Por favor, escreva toda a reflexão estritamente em português."
                )
            }

            val request = GeminiRequest(
                contents = listOf(
                    Content(parts = listOf(Part(text = "$systemInstruction\n\n$userPrompt")))
                )
            )

            val response = api.generateContent(apiKey = apiKey, request = request)
            val reflection = response.candidates?.firstOrNull()?.content?.parts?.firstOrNull()?.text?.trim()
            reflection ?: getDefaultFallback(languageCode)
        } catch (e: Exception) {
            if (e is CancellationException) throw e
            android.util.Log.e("GeminiApiService", "Error al generar reflexión vía Retrofit", e)
            getOfflineFallback(languageCode)
        }
    }

    private fun getOfflineFallback(languageCode: String): String = when (languageCode.lowercase()) {
        "en" -> "Connected in offline mode. Practice this reflection: Take a deep breath and bring your awareness to the present moment."
        "es" -> "Conectado en modo offline. Practica la reflexión: Respira profundo y enfoca tu atención en el momento presente."
        else -> "Conectado no modo offline. Pratique a reflexão: Respire fundo e traga sua atenção para o momento presente."
    }

    private fun getDefaultFallback(languageCode: String): String = when (languageCode.lowercase()) {
        "en" -> "Welcome the present moment exactly as it unfolds."
        "es" -> "Acoge el momento presente exactamente como se manifiesta."
        else -> "Acolha o momento presente exatamente como ele se manifesta."
    }
}
```

Ahora, crea el ViewModel que conecta el repositorio, el servicio de Gemini y el estado de la UI en `dev/mindfuldays/app/ui/viewmodel/MindfulnessViewModel.kt`:

```kotlin
package dev.mindfuldays.app.ui.viewmodel

import androidx.lifecycle.ViewModel
import androidx.lifecycle.viewModelScope
import dev.mindfuldays.app.data.model.MindfulnessAttitude
import dev.mindfuldays.app.data.remote.GeminiApiService
import dev.mindfuldays.app.data.repository.AttitudeRepository
import kotlinx.coroutines.flow.MutableStateFlow
import kotlinx.coroutines.flow.StateFlow
import kotlinx.coroutines.flow.asStateFlow
import kotlinx.coroutines.flow.update
import kotlinx.coroutines.launch
import java.util.Locale

data class MindfulnessUiState(
    val attitude: MindfulnessAttitude,
    val aiReflection: String = "",
    val isLoadingAi: Boolean = false
)

class MindfulnessViewModel(
    private val repository: AttitudeRepository = AttitudeRepository(),
    private val geminiService: GeminiApiService = GeminiApiService()
) : ViewModel() {

    private val _uiState = MutableStateFlow(
        MindfulnessUiState(attitude = repository.getTodayAttitude())
    )
    val uiState: StateFlow<MindfulnessUiState> = _uiState.asStateFlow()

    fun generateAiReflection(
        attitudeTitle: String? = null,
        languageCode: String = Locale.getDefault().language
    ) {
        viewModelScope.launch {
            _uiState.update { it.copy(isLoadingAi = true) }
            val title = attitudeTitle ?: _uiState.value.attitude.name
            val reflection = geminiService.generateReflection(title, languageCode)
            _uiState.update {
                it.copy(
                    aiReflection = reflection,
                    isLoadingAi = false
                )
            }
        }
    }
}
```

---

## 🎨 3.5. Configuración del Design System: Soporte Completo para Modo Claro y Oscuro (`Color.kt` y `Theme.kt`)

Para asegurar que la aplicación brinde una experiencia visual acogedora y legible bajo cualquier condición de iluminación, configuramos el soporte nativo para **Modo Claro (Light Theme)** y **Modo Oscuro (Dark Theme)** en Material Design 3.

> [!CAUTION]
> **El Peligro de Hardcodear Colores en Composables:**
> Si defines colores fijos como `Color(0xFFFFFFFF)` o `Color(0xFFFBF9F5)` directamente en los layouts, el texto de la interfaz (que por defecto en Material 3 cambia a colores claros en Modo Oscuro mediante `onSurface`) se volverá invisible, generando el clásico problema de **texto blanco sobre fondo blanco**.
> Utiliza siempre tokens semánticos: `MaterialTheme.colorScheme.background`, `MaterialTheme.colorScheme.surface`, `MaterialTheme.colorScheme.onSurface`, `MaterialTheme.colorScheme.primary` y `MaterialTheme.colorScheme.outlineVariant`.

### 1. `dev/mindfuldays/app/ui/theme/Color.kt`
```kotlin
package dev.mindfuldays.app.ui.theme

import androidx.compose.ui.graphics.Color

// Paleta Light Theme (Material Design 3)
val SageGreen = Color(0xFF6B8E23)
val SageGreenLight = Color(0xFF8FA853)
val MutedSand = Color(0xFFE8DFD8)
val WarmOffWhite = Color(0xFFFBF9F5)
val PureWhite = Color(0xFFFFFFFF)
val DarkForestGreen = Color(0xFF2C3E35)
val MutedForestGreen = Color(0xFF5C6F64)

// Paleta Dark Theme (Material Design 3)
val LuminousSage = Color(0xFFA8C673)
val ForestNight = Color(0xFF15201A)
val ForestSurface = Color(0xFF22322A)
val ForestSurfaceVariant = Color(0xFF2E4239)
val SoftMutedSage = Color(0xFFA3B5A8)
val ForestOutline = Color(0xFF3B5045)
val WarmOffWhiteText = Color(0xFFF1EFEA)
```

### 2. `dev/mindfuldays/app/ui/theme/Theme.kt`
```kotlin
package dev.mindfuldays.app.ui.theme

import android.os.Build
import androidx.compose.foundation.isSystemInDarkTheme
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.darkColorScheme
import androidx.compose.material3.dynamicDarkColorScheme
import androidx.compose.material3.dynamicLightColorScheme
import androidx.compose.material3.lightColorScheme
import androidx.compose.runtime.Composable
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.platform.LocalContext

private val LightColorScheme = lightColorScheme(
    primary = SageGreen,
    onPrimary = PureWhite,
    primaryContainer = SageGreenLight,
    onPrimaryContainer = PureWhite,
    secondary = MutedSand,
    onSecondary = DarkForestGreen,
    background = WarmOffWhite,
    onBackground = DarkForestGreen,
    surface = PureWhite,
    onSurface = DarkForestGreen,
    surfaceVariant = Color(0xFFF2ECE6),
    onSurfaceVariant = MutedForestGreen,
    outline = MutedSand,
    outlineVariant = MutedSand
)

private val DarkColorScheme = darkColorScheme(
    primary = LuminousSage,
    onPrimary = Color(0xFF1E3500),
    primaryContainer = ForestSurfaceVariant,
    onPrimaryContainer = LuminousSage,
    secondary = SoftMutedSage,
    onSecondary = ForestNight,
    background = ForestNight,
    onBackground = WarmOffWhiteText,
    surface = ForestSurface,
    onSurface = WarmOffWhiteText,
    surfaceVariant = ForestSurfaceVariant,
    onSurfaceVariant = SoftMutedSage,
    outline = ForestOutline,
    outlineVariant = ForestOutline
)

@Composable
fun MindfulDaysTheme(
    darkTheme: Boolean = isSystemInDarkTheme(),
    dynamicColor: Boolean = false,
    content: @Composable () -> Unit
) {
    val colorScheme = when {
        dynamicColor && Build.VERSION.SDK_INT >= Build.VERSION_CODES.S -> {
            val context = LocalContext.current
            if (darkTheme) dynamicDarkColorScheme(context) else dynamicLightColorScheme(context)
        }
        darkTheme -> DarkColorScheme
        else -> LightColorScheme
    }

    MaterialTheme(
        colorScheme = colorScheme,
        typography = Typography,
        content = content
    )
}
```

---

## 📱 3.6. Implementando la Home Screen en Jetpack Compose con Tokens Semánticos y Cadenas Internacionalizadas

Crea el archivo en `dev/mindfuldays/app/ui/home/HomeScreen.kt` utilizando `stringResource(...)` para todos los textos y tokens semánticos de colores:

```kotlin
package dev.mindfuldays.app.ui.home

import androidx.compose.foundation.BorderStroke
import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.AutoAwesome
import androidx.compose.material.icons.filled.Settings
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.res.stringResource
import androidx.compose.ui.text.font.FontStyle
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.lifecycle.compose.collectAsStateWithLifecycle
import dev.mindfuldays.app.R
import dev.mindfuldays.app.data.model.MindfulnessAttitude
import dev.mindfuldays.app.data.repository.AttitudeRepository
import dev.mindfuldays.app.ui.theme.MindfulDaysTheme
import dev.mindfuldays.app.ui.viewmodel.MindfulnessViewModel

@Composable
fun HomeScreen(
    viewModel: MindfulnessViewModel,
    onNavigateToSettings: () -> Unit,
    onNavigateToTimer: () -> Unit,
    modifier: Modifier = Modifier
) {
    val uiState by viewModel.uiState.collectAsStateWithLifecycle()
    val localizedAttitudeName = if (uiState.attitude.nameRes != 0) {
        stringResource(uiState.attitude.nameRes)
    } else {
        uiState.attitude.name
    }

    HomeScreenContent(
        attitude = uiState.attitude,
        aiReflection = uiState.aiReflection,
        isLoadingAi = uiState.isLoadingAi,
        onGenerateAiReflection = {
            viewModel.generateAiReflection(attitudeTitle = localizedAttitudeName)
        },
        onNavigateToSettings = onNavigateToSettings,
        onNavigateToTimer = onNavigateToTimer,
        modifier = modifier
    )
}

@Composable
fun HomeScreenContent(
    attitude: MindfulnessAttitude,
    aiReflection: String,
    isLoadingAi: Boolean,
    onGenerateAiReflection: () -> Unit,
    onNavigateToSettings: () -> Unit,
    onNavigateToTimer: () -> Unit,
    modifier: Modifier = Modifier
) {
    Column(
        modifier = modifier
            .fillMaxSize()
            .background(MaterialTheme.colorScheme.background)
            .statusBarsPadding()
            .navigationBarsPadding()
            .padding(24.dp),
        verticalArrangement = Arrangement.SpaceBetween,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        // Encabezado (Top Bar)
        Row(
            modifier = Modifier.fillMaxWidth(),
            verticalAlignment = Alignment.CenterVertically
        ) {
            Spacer(modifier = Modifier.size(48.dp))
            Column(
                modifier = Modifier.weight(1f),
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                Text(
                    text = stringResource(R.string.app_title),
                    style = MaterialTheme.typography.labelLarge,
                    color = MaterialTheme.colorScheme.primary,
                    fontWeight = FontWeight.Bold
                )
                Text(
                    text = stringResource(R.string.attitude_counter, attitude.id, 9),
                    style = MaterialTheme.typography.bodyMedium,
                    color = MaterialTheme.colorScheme.onSurfaceVariant
                )
            }
            IconButton(onClick = onNavigateToSettings) {
                Icon(
                    imageVector = Icons.Default.Settings,
                    contentDescription = stringResource(R.string.cd_settings),
                    tint = MaterialTheme.colorScheme.onBackground
                )
            }
        }

        // Tarjeta Central (ElevatedCard)
        ElevatedCard(
            modifier = Modifier
                .fillMaxWidth()
                .padding(vertical = 16.dp),
            colors = CardDefaults.elevatedCardColors(
                containerColor = MaterialTheme.colorScheme.surface
            ),
            elevation = CardDefaults.elevatedCardElevation(
                defaultElevation = 4.dp
            )
        ) {
            Column(
                modifier = Modifier.padding(20.dp),
                verticalArrangement = Arrangement.spacedBy(12.dp)
            ) {
                Text(
                    text = if (attitude.nameRes != 0) stringResource(attitude.nameRes) else attitude.name,
                    style = MaterialTheme.typography.headlineMedium,
                    fontWeight = FontWeight.Bold,
                    color = MaterialTheme.colorScheme.onSurface
                )
                Text(
                    text = if (attitude.descriptionRes != 0) stringResource(attitude.descriptionRes) else attitude.description,
                    style = MaterialTheme.typography.bodyLarge,
                    color = MaterialTheme.colorScheme.onSurface
                )
                HorizontalDivider(
                    color = MaterialTheme.colorScheme.outlineVariant,
                    thickness = 1.dp
                )
                Text(
                    text = if (aiReflection.isNotBlank()) aiReflection else stringResource(R.string.default_reflection),
                    style = MaterialTheme.typography.bodyMedium,
                    fontStyle = FontStyle.Italic,
                    color = MaterialTheme.colorScheme.onSurfaceVariant
                )
                Spacer(modifier = Modifier.height(4.dp))
                Button(
                    onClick = onGenerateAiReflection,
                    enabled = !isLoadingAi,
                    colors = ButtonDefaults.buttonColors(
                        containerColor = MaterialTheme.colorScheme.primary,
                        contentColor = MaterialTheme.colorScheme.onPrimary
                    ),
                    modifier = Modifier.fillMaxWidth()
                ) {
                    if (isLoadingAi) {
                        CircularProgressIndicator(
                            modifier = Modifier.size(20.dp),
                            color = MaterialTheme.colorScheme.onPrimary,
                            strokeWidth = 2.dp
                        )
                    } else {
                        Icon(
                            imageVector = Icons.Default.AutoAwesome,
                            contentDescription = null,
                            modifier = Modifier.size(18.dp)
                        )
                        Spacer(modifier = Modifier.width(8.dp))
                        Text(text = stringResource(R.string.btn_new_reflection))
                    }
                }
            }
        }

        // Acción de Navegación hacia el Temporizador
        OutlinedButton(
            onClick = onNavigateToTimer,
            border = BorderStroke(1.dp, MaterialTheme.colorScheme.outlineVariant),
            colors = ButtonDefaults.outlinedButtonColors(
                contentColor = MaterialTheme.colorScheme.primary
            ),
            modifier = Modifier
                .fillMaxWidth()
                .padding(bottom = 8.dp)
        ) {
            Text(
                text = stringResource(R.string.btn_start_timer),
                style = MaterialTheme.typography.bodyLarge
            )
        }
    }
}
```

---

Con las pantallas internacionalizadas y la comunicación multilingüe con la Gemini API listas, avanzamos hacia el **Módulo 4: Calidad de Software, Pruebas Automatizadas con IA y Robot Pattern**.
