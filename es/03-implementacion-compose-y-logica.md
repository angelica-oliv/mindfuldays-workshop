# 🧩 Módulo 3 — AGENTS.md, Regla de las 9 Actitudes, Gemini API y UI en Compose

En este módulo, estructuraremos el archivo **`AGENTS.md`** como contexto operacional para agentes de IA, configuraremos el acceso seguro a la **Gemini API** y nos enfocaremos únicamente en las **piezas clave de código y arquitectura**, delegando el código repetitivo (*boilerplate*) al asistente de IA mediante prompts guiados.

---

## 🤖 3.1. Directrices para Agentes de IA: Creación del Archivo `AGENTS.md`

Antes de pedirle a la IA que implemente o refactorice archivos del proyecto, configuraremos nuestro recurso más estratégico: el archivo **`AGENTS.md`**.

### 🌟 ¿Por qué es tan importante `AGENTS.md`?

Así como el `README.md` orienta a las personas desarrolladoras, el **`AGENTS.md`** actúa como la **fuente única de verdad operacional para agentes autónomos y asistentes de código con IA** (como Gemini en Android Studio, Cursor, Claude Code, GitHub Copilot y Antigravity).

1. **Grounding y Reducción de Alucinaciones**: Ancla a la IA en las decisiones técnicas ya tomadas.
2. **Consistencia de Stack y Arquitectura**: Garantiza el respeto estricto por **MVVM**, **Clean Architecture**, **Kotlin idiomático** y **Jetpack Compose con Material Design 3**.
3. **Fidelidad a los Design Tokens y Reglas de Negocio**: Mantiene siempre presentes la paleta oficial extraída en Stitch y la rotación cíclica de las 9 actitudes de Jon Kabat-Zinn.
4. **Guardrails de Seguridad**: Prohíbe explícitamente claves secretas (`apiKey`) hardcodeadas o colores hexadecimales fijos en Composables.
5. **Prompts más cortos y rápidos en el Workshop**: Con `AGENTS.md` en la raíz del proyecto, no necesitas repetir reglas arquitectónicas ni paletas de colores en cada prompt.

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
   `val index = (dayOfYear - 1).mod(attitudes.size)`
2. **Gemini API (Reflexiones Diarias)**:
   - Utilizar el endpoint del modelo `gemini-3.8-flash:generateContent`.
   - Generar reflexiones concisas e inspiradoras con un máximo de 2 oraciones por actitud, respetando el idioma del usuario (pt, en, es).
   - Manejar la ausencia de clave de API y errores de red con un mensaje amigable offline sin romper la app.

## 🛠️ Comandos de Verificación y Validación
Verifica siempre los cambios utilizando los siguientes comandos en la terminal:
- **Compilación de la app**: `./gradlew assembleDebug`
- **Pruebas Unitarias**: `./gradlew testDebugUnitTest`
- **Pruebas de UI (Robot Pattern)**: `./gradlew connectedDebugAndroidTest`

## 🚫 Restricciones Estrictas (Guardrails)
- **NUNCA utilices colores hexadecimales hardcodeados en Composables** (`Color(0xFF...)`). Utiliza siempre `MaterialTheme.colorScheme.background`, `MaterialTheme.colorScheme.surface`, `MaterialTheme.colorScheme.onSurface`, etc., para evitar problemas de contraste en el Modo Oscuro.
- **NUNCA** hagas commit ni dejes credenciales o claves de API (`apiKey`) en el código versionado. La clave debe configurarse en `local.properties` y consumirse mediante `BuildConfig.GEMINI_API_KEY`.
- **NO** mezcles lógica de negocio o llamadas asíncronas de red directamente dentro de funciones `@Composable`.
- Mantén las funciones Composable limpias y desacopladas, utilizando parámetros para eventos y lambdas (`onAction: () -> Unit`) para facilitar pruebas de UI.
- Utiliza recursos internacionalizados (`stringResource(R.string...)`) para textos visibles e inglés para código técnico, métodos e interfaces.
```

---

## 🔑 3.2. Configuración de Gemini API y Gestión Segura de Credenciales

Para integrar la **Gemini API** de forma segura y moderna, configuraremos la clave en `local.properties` y las dependencias de **Retrofit**, **Moshi** y **OkHttp**.

### 1. Obtención y Activación de la API Key
1. Ingresa a [Google AI Studio](https://aistudio.google.com/), haz clic en **Get API key** y copia la clave generada.
2. Asegúrate de tener habilitada la **Generative Language API** en tu consola de Google Cloud (`https://console.developers.google.com/apis/api/generativelanguage.googleapis.com/overview`).

> [!WARNING]
> **Trampa Común — Claves de Firebase (`API_KEY_SERVICE_BLOCKED` 403):**
> Nunca utilices claves generadas automáticamente por Firebase para llamar al endpoint de Gemini API. Utiliza siempre una clave creada directamente en **Google AI Studio**.

### 2. Almacenamiento Seguro en `local.properties`
Abre el archivo `local.properties` en la raíz del proyecto (ignorado por Git) y agrega:

```properties
GEMINI_API_KEY=tu_clave_de_ai_studio_aqui
```

### 3. Inyección vía `buildConfigField` en `app/build.gradle.kts`
En el archivo `app/build.gradle.kts`, lee `local.properties` y expón la constante en `BuildConfig`:

```kotlin
import java.util.Properties

val localProperties = Properties()
val localPropertiesFile = rootProject.file("local.properties")
if (localPropertiesFile.exists()) {
    localPropertiesFile.inputStream().use { localProperties.load(it) }
}
val geminiApiKey: String = localProperties.getProperty("GEMINI_API_KEY") ?: ""

android {
    // ...
    defaultConfig {
        // ...
        buildConfigField("String", "GEMINI_API_KEY", "\"$geminiApiKey\"")
    }

    buildFeatures {
        compose = true
        buildConfig = true // Habilita la generación de BuildConfig
    }
}
```

### 4. Dependencias de Red (`libs.versions.toml` y `app/build.gradle.kts`)
Agrega Retrofit, Moshi y OkHttp en `gradle/libs.versions.toml`:

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

Y decláralas en el bloque `dependencies` de `app/build.gradle.kts`:

```kotlin
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

## 🌐 3.3. Internacionalización (i18n) con IA (Inglés, Español y Portugués)

En lugar de copiar y pegar cientos de líneas de archivos XML manualmente, utilizaremos a Gemini para generar o verificar las tablas de recursos en los 3 idiomas (`values/strings.xml`, `values-es/strings.xml` y `values-pt/strings.xml`).

### 🔍 Estructura Clave de `strings.xml`
Asegúrate de que tus archivos de recursos sigan estos nombres de claves estándar (necesarios para la UI y las pruebas del Módulo 4):

```xml
<resources>
    <string name="app_name">MindfulDays</string>
    <string name="app_title">MINDFULDAYS</string>
    <string name="attitude_counter">Actitud %1$d de %2$d</string>
    <string name="default_reflection">“Respira profundo y trae tu atención al momento presente.”</string>
    <string name="btn_new_reflection">✨ Nueva Reflexión (Gemini IA)</string>
    <string name="btn_start_timer">⏱️ Iniciar Temporizador de Meditación</string>
    <string name="cd_settings">Configuración</string>
    <!-- Las 9 Actitudes: attitude_1_name / attitude_1_desc hasta attitude_9_name / attitude_9_desc -->
    <string name="attitude_1_name">Mente de Principiante</string>
    <string name="attitude_1_desc">Mira las cosas como si fuera la primera vez, libre de expectativas.</string>
</resources>
```

### 🤖 Prompt para Generar los Archivos `strings.xml` (EN / ES / PT)
Abre el chat de Gemini en Android Studio y ejecuta este prompt:

```text
Siguiendo las directrices de @AGENTS.md, genera o completa los 3 archivos de recursos de strings para internacionalización:
1. app/src/main/res/values/strings.xml (Inglés por defecto)
2. app/src/main/res/values-es/strings.xml (Español)
3. app/src/main/res/values-pt/strings.xml (Portugués)

Incluye exactamente estas claves en los 3 idiomas:
- Generales y Home: app_name, app_title, attitude_counter ("Attitude %1$d of %2$d"), default_reflection, btn_new_reflection, btn_start_timer.
- Temporizador: timer_title, timer_subtitle, timer_session_guided, timer_status_completed, timer_status_running, timer_status_paused.
- Configuración: settings_title, settings_section_reminders, settings_daily_reminder, settings_meditate_reminder, settings_section_about, settings_version_info.
- Accesibilidad: cd_settings, cd_back, cd_reset, cd_play, cd_pause.
- Las 9 Actitudes de Mindfulness de Jon Kabat-Zinn (attitude_1_name a attitude_9_name y attitude_1_desc a attitude_9_desc):
  1. Mente de Principiante (Beginner's Mind)
  2. No Juicio (Non-Judging)
  3. Aceptación (Acceptance)
  4. Desapego (Letting Go)
  5. Confianza (Trust)
  6. No Esforzarse (Non-Striving)
  7. Paciencia (Patience)
  8. Gratitud (Gratitude)
  9. Generosidad (Generosity)
```

---

## 🧠 3.4. Regla de las 9 Actitudes y Estado de la UI (`AttitudeRepository` y `MindfulnessViewModel`)

En el Módulo 2 generamos `AttitudeRepository.kt` y `MindfulnessViewModel.kt` como esqueletos (*stubs*). Ahora implementaremos la lógica real.

### 🔍 Código Clave a Enfocar: Fórmula de Rotación Cíclica
El corazón del dominio de **MindfulDays** es el modelo `MindfulnessAttitude` y la función determinística `getTodayAttitude`, que rota las 9 actitudes según el día del año usando la operación módulo (`.mod(9)`):

```kotlin
// data/model/MindfulnessAttitude.kt
data class MindfulnessAttitude(
    val id: Int,
    val name: String = "",
    val description: String = "",
    @get:StringRes val nameRes: Int = 0,
    @get:StringRes val descriptionRes: Int = 0
)

// Lógica central en data/repository/AttitudeRepository.kt
fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude {
    val index = (dayOfYear - 1).mod(attitudes.size)
    return attitudes[index]
}
```

> [!TIP]
> **¿Por qué pasar `dayOfYear` como parámetro con valor por defecto?**
> Esto permite que en producción tome automáticamente el día actual del calendario, mientras que en las **Pruebas Unitarias (Módulo 4)** podemos inyectar cualquier día (día 1, día 9, día 10, día 365) para probar la rotación sin depender del reloj del sistema.

### 🤖 Prompt para Implementar `AttitudeRepository.kt` y `MindfulnessViewModel.kt`
En lugar de escribir manualmente la lista de las 9 actitudes y el `StateFlow` del ViewModel, pídele a Gemini:

```text
Siguiendo @AGENTS.md, completa la implementación de estas dos clases reemplazando los TODOs:

1. En `dev/mindfuldays/app/data/repository/AttitudeRepository.kt`:
   - Define la propiedad pública `val attitudes = listOf(...)` con las 9 Actitudes de Mindfulness de Jon Kabat-Zinn (IDs del 1 al 9), incluyendo sus textos por defecto (`name`, `description`) y sus referencias `@StringRes` (`R.string.attitude_1_name`, `R.string.attitude_1_desc`, etc.).
   - Implementa `fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude` usando `val index = (dayOfYear - 1).mod(attitudes.size)`.

2. En `dev/mindfuldays/app/ui/viewmodel/MindfulnessViewModel.kt`:
   - Mantén `data class MindfulnessUiState(val attitude: MindfulnessAttitude, val aiReflection: String = "", val isLoadingAi: Boolean = false)`.
   - En `MindfulnessViewModel(private val repository: AttitudeRepository = AttitudeRepository(), private val geminiService: GeminiApiService = GeminiApiService())`, expón `val uiState: StateFlow<MindfulnessUiState>` inicializado con `repository.getTodayAttitude()`.
   - Implementa `fun generateAiReflection(attitudeTitle: String? = null, languageCode: String = Locale.getDefault().language)` que actualice `isLoadingAi = true`, llame a `geminiService.generateReflection(title, languageCode)` y actualice `aiReflection` e `isLoadingAi = false`.
```

---

## 🤖 3.5. Integración con Gemini API vía Retrofit y Moshi (`GeminiApiService.kt`)

Ahora conectaremos nuestra aplicación con el modelo **`gemini-3.8-flash`** utilizando Retrofit y Moshi.

> [!IMPORTANT]
> **Dos Puntos Críticos en Producción:**
> 1. **Modelo (`gemini-3.8-flash`)**: Modelos anteriores como `gemini-1.5-flash` o `gemini-2.5-flash` devuelven HTTP 404 para nuevas claves en `v1beta`. Usa siempre **`gemini-3.8-flash`**.
> 2. **Serialización con Moshi en Kotlin**: Anota los DTOs con `@JsonClass(generateAdapter = true)` y registra `KotlinJsonAdapterFactory()` en el builder de Moshi para evitar fallos de reflexión en tiempo de ejecución.

### 🔍 Código Clave a Enfocar: Contrato Retrofit y Configuración Moshi
Estos son los dos bloques esenciales que estructuran la llamada a la API:

```kotlin
// 1. DTOs y Endpoint oficial en data/remote/GeminiApiService.kt
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

interface GeminiApi {
    @POST("v1beta/models/gemini-3.8-flash:generateContent")
    suspend fun generateContent(
        @Query("key") apiKey: String,
        @Body request: GeminiRequest
    ): GeminiResponse
}

// 2. Builder de Moshi + Retrofit
val moshi = Moshi.Builder()
    .addLast(KotlinJsonAdapterFactory())
    .build()
```

### 🤖 Prompt para Generar `GeminiApiService.kt` Completo
Usa este prompt en el asistente de IA para generar toda la clase `GeminiApiService.kt` con soporte multilingüe y modo offline:

```text
Siguiendo @AGENTS.md, implementa la clase completa `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:
1. Incluye los DTOs (`GeminiRequest`, `Content`, `Part`, `GeminiResponse`, `Candidate`, `ContentResponse`, `PartResponse`) anotados con `@JsonClass(generateAdapter = true)` y la interfaz `GeminiApi` con `@POST("v1beta/models/gemini-3.8-flash:generateContent")`.
2. Configura `OkHttpClient` con `HttpLoggingInterceptor(Level.BODY)`, `Moshi` con `KotlinJsonAdapterFactory()` y `Retrofit` apuntando a `"https://generativelanguage.googleapis.com/"`.
3. Implementa `suspend fun generateReflection(attitudeTitle: String, languageCode: String = Locale.getDefault().language): String` ejecutándose en `Dispatchers.IO`:
   - Lee `BuildConfig.GEMINI_API_KEY`. Si está vacía (`isBlank()`), retorna inmediatamente un mensaje amigable de fallback offline según `languageCode` ("es", "en", "pt").
   - Construye un prompt sereno de mindfulness pidiendo una reflexión inspiradora de máximo 2 oraciones en texto plano sobre `attitudeTitle`, estrictamente en el idioma `languageCode`.
   - Captura cualquier excepción de red (re-lanzando `CancellationException`), registra el error en `Log.e` y retorna el fallback offline sin romper la app.
```

---

## 🎨 3.6. Tema Dual (Light/Dark Mode) y `HomeScreen.kt` Desacoplada

En el Módulo 2 generamos los archivos `Color.kt`, `Theme.kt` y `HomeScreen.kt`. Antes de pasar a las pruebas automatizadas del Módulo 4, revisaremos dos conceptos clave de UI en Jetpack Compose.

> [!CAUTION]
> **El Peligro de Hardcodear Colores en Composables:**
> Si defines colores fijos como `Color(0xFFFFFFFF)` directamente en un Composable, en **Modo Oscuro** el texto (`onSurface`, blanco cálido) quedará invisible sobre el fondo blanco. Usa siempre tokens semánticos: `MaterialTheme.colorScheme.background`, `surface`, `onSurface`, `onSurfaceVariant`, `primary` y `outlineVariant`.

### 🔍 Código Clave a Enfocar: Separación de Estado (`HomeScreen` vs `HomeScreenContent`)
Para que nuestras pruebas de UI con **Robot Pattern** (Módulo 4) sean rápidas y determinísticas, separamos `HomeScreen` en una función con estado (conectada al ViewModel) y una función *stateless* (`HomeScreenContent`) que recibe solo datos primitivos y lambdas:

```kotlin
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
```

### 🤖 Prompt de Auditoría para `Theme.kt` y `HomeScreen.kt`
Si deseas verificar o ajustar tu tema y pantalla principal generados en el Módulo 2, ejecuta este prompt:

```text
Revisa `Color.kt`, `Theme.kt` y `HomeScreen.kt` contra las reglas de @AGENTS.md:
1. Verifica que `Theme.kt` defina correctamente `LightColorScheme` y `DarkColorScheme` usando la paleta oficial de MindfulDays y `dynamicColor: Boolean = false` por defecto.
2. Verifica que `HomeScreen.kt` NO tenga ningún `Color(0xFF...)` ni textos hardcodeados: todos los colores deben usar `MaterialTheme.colorScheme.*` y todos los textos deben usar `stringResource(R.string.*)`.
3. Asegúrate de que `HomeScreen.kt` exponga el composable stateless `HomeScreenContent(attitude: MindfulnessAttitude, aiReflection: String, isLoadingAi: Boolean, onGenerateAiReflection: () -> Unit, onNavigateToSettings: () -> Unit, onNavigateToTimer: () -> Unit, modifier: Modifier = Modifier)` para nuestras pruebas de UI.
```

---

### ✅ Verificación Rápida del Módulo 3
En la terminal de Android Studio, verifica que todo compile correctamente antes de iniciar las pruebas:

```bash
./gradlew assembleDebug
```

Con el contexto en `AGENTS.md`, la lógica de las 9 actitudes y la integración con Gemini API listas en una fracción del tiempo, avanzamos hacia el **Módulo 4: Calidad de Software, Pruebas Automatizadas con IA y Robot Pattern**.
