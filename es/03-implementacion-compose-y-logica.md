# 🧩 Módulo 3 — AGENTS.md, Regla de las 9 Actitudes, Gemini API y UI en Compose

En este módulo, estructuraremos el archivo **`AGENTS.md`** como contexto operacional y utilizaremos **un solo prompt unificado** para que Gemini en Android Studio configure las credenciales en Gradle, implemente la regla de las 9 actitudes, conecte la **Gemini API** con Retrofit/Moshi y prepare la UI para el workshop.

---

## 🤖 3.1. Directrices para Agentes de IA: Creación del Archivo `AGENTS.md`

Antes de solicitar cualquier cambio a la IA, configuramos nuestro recurso más estratégico: el archivo **`AGENTS.md`**.

### 🌟 ¿Por qué es tan importante `AGENTS.md`?

Así como el `README.md` orienta a los desarrolladores, el **`AGENTS.md`** actúa como la **fuente única de verdad operacional para agentes y asistentes de código con IA** (Gemini en Android Studio, Cursor, Claude Code, GitHub Copilot y Antigravity):

1. **Grounding y Reducción de Alucinaciones**: Ancla a la IA en las decisiones técnicas ya tomadas.
2. **Consistencia de Stack y Arquitectura**: Garantiza el respeto estricto por **MVVM**, **Clean Architecture**, **Kotlin idiomático** y **Jetpack Compose con Material Design 3**.
3. **Fidelidad a los Design Tokens y Reglas de Negocio**: Mantiene presente la paleta oficial de Stitch y la rotación cíclica de las 9 actitudes de Jon Kabat-Zinn.
4. **Guardrails de Seguridad**: Prohíbe explícitamente claves secretas (`apiKey`) hardcodeadas o colores hexadecimales fijos en Composables.
5. **Máxima Velocidad en Presentaciones y Workshops**: Al existir `AGENTS.md` en la raíz, un **único prompt** es suficiente para implementar toda la lógica de negocio y red.

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
   - Utilizar el endpoint del modelo `gemini-3.5-flash:generateContent` (o `gemini-3.5-flash-lite:generateContent`).
   - Configurar OkHttpClient con timeouts holgados adecuados para LLM (`connectTimeout`: 30s, `readTimeout`: 60s, `writeTimeout`: 30s). No fijar `callTimeout` agresivos ni `pingInterval` para evitar errores de SocketTimeoutException.
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

## 🔑 3.2. Clave de API en `local.properties` (Paso Manual Rápido)

1. Obtén tu API Key gratuita en [Google AI Studio](https://aistudio.google.com/) (**Get API key**).
2. Abre el archivo `local.properties` en la raíz de tu proyecto (ignorado por Git) y agrega tu clave:

```properties
GEMINI_API_KEY=tu_clave_de_ai_studio_aqui
```

> [!WARNING]
> **Importante:** Utiliza una clave generada en Google AI Studio (o Google Cloud con la Generative Language API habilitada). No utilices claves de Firebase con restricciones de app, ya que generan error `403 (API_KEY_SERVICE_BLOCKED)`.

---

## 🔍 3.3. Conceptos Clave de Arquitectura (Lo que la IA construirá)

Para entender lo que la IA implementará en el prompt unificado:

1. **Gradle & Inyección Segura**: `app/build.gradle.kts` lee `local.properties` y expone `BuildConfig.GEMINI_API_KEY`, agregando Retrofit, Moshi y OkHttp.
2. **Internacionalización (i18n)**: Generación sincronizada de `values/strings.xml`, `values-es/strings.xml` y `values-pt/strings.xml` con las 9 actitudes de Jon Kabat-Zinn.
3. **Fórmula de Rotación Cíclica**:
   ```kotlin
   fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude {
       val index = (dayOfYear - 1).mod(attitudes.size)
       return attitudes[index]
   }
   ```
4. **Cliente Gemini API**: Llamada REST a `v1beta/models/gemini-3.5-flash:generateContent` con adaptadores Moshi en Kotlin y fallback amigable offline si no hay red o falta la clave.

---

## ⚡ 3.4. Prompt Único y Completo para Gemini en Android Studio (Todo en Uno)

Abre el panel de **Gemini** en Android Studio (**View → Tool Windows → Gemini**) y envía el siguiente **prompt unificado**. Realizará todas las tareas del Módulo 3 en un solo paso:

```text
Actúa como un Desarrollador Android Senior y sigue estrictamente las directrices de @AGENTS.md.
Realiza en un solo paso todas las configuraciones e implementaciones pendientes del Módulo 3 para 'dev.mindfuldays.app':

1. CONFIGURACIÓN DE GRADLE Y SEGURIDAD:
   - En `app/build.gradle.kts`:
     * Carga `local.properties` mediante `java.util.Properties` y lee la propiedad `GEMINI_API_KEY` (fallback a "").
     * En `defaultConfig`, agrega: `buildConfigField("String", "GEMINI_API_KEY", "\"$geminiApiKey\"")`.
     * En `buildFeatures`, asegura `compose = true` y `buildConfig = true`.
   - En `gradle/libs.versions.toml` y `app/build.gradle.kts`, asegura las dependencias para:
     * Retrofit (`retrofit`, `converter-moshi`)
     * Moshi (`moshi-kotlin`, KSP `moshi-kotlin-codegen`)
     * OkHttp (`okhttp`, `logging-interceptor`)

2. RECURSOS DE STRINGS E INTERNACIONALIZACIÓN (i18n):
   - Crea/actualiza de forma consistente:
     * `app/src/main/res/values/strings.xml` (Inglés por defecto)
     * `app/src/main/res/values-es/strings.xml` (Español)
     * `app/src/main/res/values-pt/strings.xml` (Portugués)
   - Incluye las claves: `app_name`, `app_title`, `attitude_counter` ("Attitude %1$d of %2$d"), `default_reflection`, `btn_new_reflection`, `btn_start_timer`, `timer_title`, `timer_subtitle`, `timer_session_guided`, `timer_status_completed`, `timer_status_running`, `timer_status_paused`, `settings_title`, `settings_section_reminders`, `settings_daily_reminder`, `settings_meditate_reminder`, `settings_section_about`, `settings_version_info`, content descriptions (`cd_settings`, `cd_back`, `cd_reset`, `cd_play`, `cd_pause`), y las 9 Actitudes de Mindfulness de Jon Kabat-Zinn (`attitude_1_name` a `attitude_9_name` y `attitude_1_desc` a `attitude_9_desc`).

3. LÓGICA DE NEGOCIO Y REPOSITORIO (AttitudeRepository.kt):
   - En `dev/mindfuldays/app/data/repository/AttitudeRepository.kt`:
     * Implementa la lista inmutable pública `val attitudes = listOf(...)` con las 9 actitudes (IDs 1 al 9), con sus nombres, descripciones y referencias a recursos `@StringRes` (`nameRes`, `descriptionRes`).
     * Implementa `fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude` usando la fórmula `(dayOfYear - 1).mod(attitudes.size)`.

4. INTEGRACIÓN CON GEMINI API (GeminiApiService.kt):
   - En `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:
     * Define los DTOs con `@JsonClass(generateAdapter = true)`: `GeminiRequest`, `Content`, `Part`, `GeminiResponse`, `Candidate`, `ContentResponse`, `PartResponse`.
     * Interfaz Retrofit `GeminiApi` con `@POST("v1beta/models/gemini-3.5-flash:generateContent")` (IMPORTANTE: usa EXCLUSIVAMENTE 'gemini-3.5-flash' o 'gemini-3.5-flash-lite'; NO uses 'gemini-2.5-flash' que da 404 ni 'gemini-3.8-flash' que se congela) recibiendo `@Query("key") apiKey: String` y `@Body request: GeminiRequest`.
     * Configura `OkHttpClient.Builder()` optimizado para LLMs con timeouts holgados:
       - `.connectTimeout(30, TimeUnit.SECONDS)`
       - `.readTimeout(60, TimeUnit.SECONDS)`
       - `.writeTimeout(30, TimeUnit.SECONDS)`
       - `.retryOnConnectionFailure(true)`
       - `.addInterceptor(HttpLoggingInterceptor().apply { level = HttpLoggingInterceptor.Level.BODY })`
       - REGLA CRÍTICA DE TIMEOUT: NO uses `callTimeout(20s)` ni `pingInterval` (provocan cancelaciones prematuras y SocketTimeoutException durante la inferencia de Gemini).
     * Configura `Moshi.Builder().addLast(KotlinJsonAdapterFactory()).build()` y el cliente Retrofit con este `OkHttpClient`.
     * Implementa `suspend fun generateReflection(attitudeTitle: String, languageCode: String = Locale.getDefault().language): String` en `Dispatchers.IO`:
       - Lee `BuildConfig.GEMINI_API_KEY`. Si está vacía (`isBlank()`), retorna un mensaje amigable offline en el idioma del usuario.
       - Construye el prompt para solicitar una reflexión de mindfulness de máximo 2 oraciones en texto plano en el idioma correspondiente (`languageCode`).
       - En caso de excepción de red o timeout (re-lanzando `CancellationException`), registra el error y retorna el fallback offline sin fallar ni romper la app.

5. VIEWMODEL Y ESTADO DE UI (MindfulnessViewModel.kt):
   - En `dev/mindfuldays/app/ui/viewmodel/MindfulnessViewModel.kt`:
     * Define `MindfulnessUiState(val attitude: MindfulnessAttitude, val aiReflection: String = "", val isLoadingAi: Boolean = false)`.
     * Conecta `AttitudeRepository` y `GeminiApiService`.
     * Expón `val uiState: StateFlow<MindfulnessUiState>` inicializado con `repository.getTodayAttitude()`.
     * Implementa `fun generateAiReflection(attitudeTitle: String? = null, languageCode: String = Locale.getDefault().language)` actualizando `isLoadingAi = true`, llamando a `geminiService.generateReflection` y actualizando el estado.

6. DESIGN TOKENS Y SISTEMA DE TEMA (Color.kt y Theme.kt):
   - En `dev/mindfuldays/app/ui/theme/Color.kt`:
     * Codifica explícitamente los colores de diseño:
       val SageGreen = Color(0xFF6B8E23)
       val SoftSage = Color(0xFF8FA853)
       val MutedSand = Color(0xFFE8DFD8)
       val WarmOffWhite = Color(0xFFFBF9F5)
       val PureWhite = Color(0xFFFFFFFF)
       val DarkForestGreen = Color(0xFF2C3E35)
       val MutedForestGreen = Color(0xFF5C6F64)
       val LuminousSage = Color(0xFFA8C673)
       val DeepForestSurface = Color(0xFF2E4239)
       val DeepTranquilForest = Color(0xFF15201A)
       val ElevatedForestSurface = Color(0xFF22322A)
       val WarmOffWhiteText = Color(0xFFF1EFEA)
       val SoftMutedSage = Color(0xFFA3B5A8)
       val ForestOutline = Color(0xFF3B5045)
   - En `dev/mindfuldays/app/ui/theme/Theme.kt`:
     * Desactiva el color dinámico del sistema operativo por defecto (`dynamicColor: Boolean = false`) para evitar que el wallpaper del dispositivo sobreescriba y altere la paleta de la app.
     * Configura `LightColorScheme`:
       primary = SageGreen, primaryContainer = SoftSage, secondary = MutedSand,
       background = WarmOffWhite, surface = PureWhite, onPrimary = PureWhite,
       onBackground = DarkForestGreen, onSurface = DarkForestGreen,
       onSurfaceVariant = MutedForestGreen, outlineVariant = MutedSand
     * Configura `DarkColorScheme`:
       primary = LuminousSage, primaryContainer = DeepForestSurface, secondary = SoftMutedSage,
       background = DeepTranquilForest, surface = ElevatedForestSurface, onPrimary = DeepTranquilForest,
       onBackground = WarmOffWhiteText, onSurface = WarmOffWhiteText,
       onSurfaceVariant = SoftMutedSage, outlineVariant = ForestOutline
   - Audita `HomeScreen.kt`, `TimerScreen.kt`, `SettingsScreen.kt`: NUNCA uses colores hex hardcodeados, utiliza siempre `MaterialTheme.colorScheme.*` y asegura que todos los textos usen `stringResource(R.string.*)`. Además `HomeScreen` debe delegar a un composable stateless `HomeScreenContent` desacoplado para facilitar pruebas.

Sincroniza el proyecto y verifica que './gradlew assembleDebug' compile exitosamente.
```

---

## ✅ 3.5. Verificación de Compilación

En la terminal de Android Studio, ejecuta:

```bash
./gradlew assembleDebug
```

Con este **único prompt**, completamos toda la integración de red, persistencia, i18n y estado de negocio en minutos. ¡Avanzamos hacia el **Módulo 4: Calidad de Software, Pruebas Automatizadas con IA y Robot Pattern**!
