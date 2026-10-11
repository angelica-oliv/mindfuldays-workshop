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

## 🎨 Design Tokens (Material Design 3)
Respeta estrictamente la paleta de colores definida en los prototipos de Google Stitch:
- `SageGreen` (`#6B8E23`): Color primario (calma, enfoque).
- `SageGreenLight` (`#8FA853`): Variante suave para destacados secundarios.
- `SandMuted` (`#E8DFD8`): Color secundario y divisores.
- `WarmOffWhite` (`#FBF9F5`): Fondo predeterminado de las pantallas.
- `PureWhite` (`#FFFFFF`): Fondo de tarjetas elevadas y superficies.
- `ForestDark` (`#2C3E35`): Texto principal e íconos de alto contraste.

## 🧠 Reglas de Negocio Fundamentales
1. **Regla de las 9 Actitudes**: La lista contiene exactamente 9 actitudes fijas. La actitud del día se calcula determinísticamente a partir del día del año:
   `val index = (Calendar.getInstance().get(Calendar.DAY_OF_YEAR) - 1) % 9`
2. **Gemini API con Firebase AI Logic**:
   - Utilizar la biblioteca oficial `com.google.firebase:firebase-ai` con el backend `GenerativeBackend.googleAI()`.
   - Utilizar el modelo más reciente: `gemini-3.5-flash-lite`.
   - Generar reflexiones concisas e inspiradoras con un máximo de 2 oraciones por actitud.
   - Manejar la ausencia de conexión y excepciones con un mensaje amigable offline sin romper la app.

## 🛠️ Comandos de Verificación y Validación
Verifica siempre los cambios utilizando los siguientes comandos en la terminal:
- **Compilación de la app**: `./gradlew assembleDebug`
- **Pruebas Unitarias**: `./gradlew testDebugUnitTest`
- **Linter y Análisis Estático**: `./gradlew lintDebug`

## 🚫 Restricciones Estrictas (Guardrails)
- **NUNCA** hagas commit ni dejes credenciales o claves de API (`apiKey`) en el código. La autenticación y acceso se gestionan de forma segura mediante Firebase a través de `google-services.json` y Firebase App Check.
- **NO** mezcles lógica de negocio o llamadas asíncronas de red directamente dentro de funciones `@Composable`.
- Mantén las funciones Composable limpias y desacopladas, utilizando parámetros para eventos y lambdas (`onAction: () -> Unit`) para facilitar pruebas de UI.
- Utiliza nombres descriptivos en español para textos de interfaz visible e inglés para código técnico, métodos e interfaces.
```

Con `AGENTS.md` configurado en la raíz del proyecto, cualquier agente (como Gemini en Android Studio) producirá código perfectamente alineado con tu sistema de diseño y tus reglas de negocio.

---

## 🔥 3.2. Configuración de Firebase y Firebase AI Logic (Instrucciones Estilo JetPacker)

La forma recomendada y más moderna por Google para integrar la **Gemini API** en aplicaciones Android es a través de **Firebase AI Logic** (`com.google.firebase:firebase-ai`), tal como se demuestra en el repositorio oficial de referencia del equipo de Android: [android/ai-samples/jetpacker](https://github.com/android/ai-samples/tree/main/jetpacker).

A diferencia de las llamadas HTTP directas o del SDK anterior con claves de API expuestas, Firebase AI Logic ofrece:
* **Seguridad Reforzada**: Elimina la necesidad de exponer claves de API en el código cliente mediante **Firebase App Check** y atestación de Play Integrity.
* **Backend Optimizado**: Integración directa con `GenerativeBackend.googleAI()`.
* **Acceso a los Modelos Más Recientes**: Soporte nativo para el modelo **`gemini-3.5-flash-lite`**, optimizado para latencia ultra baja y respuestas concisas en tiempo real.

Sigue los 4 pasos de configuración descritos a continuación:

### 1. Creación del Proyecto en Firebase Console
1. Accede a [Firebase Console](https://console.firebase.google.com/) e inicia sesión con tu cuenta de Google.
2. Crea un nuevo proyecto (ej: `MindfulDays`) o selecciona uno existente.
3. Agrega una nueva aplicación Android indicando el **Package Name** del proyecto:
   * **Package Name**: `dev.mindfuldays.app`
4. Descarga el archivo de configuración `google-services.json` generado por Firebase.
5. Guarda el archivo dentro del directorio `app/` de tu proyecto (`MindfulDays/app/google-services.json`).

> [!TIP]
> **Archivo Mock Placeholder para Compilación Local:**
> Al igual que en el proyecto de referencia [JetPacker](https://github.com/android/ai-samples/tree/main/jetpacker), puedes mantener un archivo mock `app/google-services.json` inicial en el proyecto para que cualquier persona pueda compilar vía Gradle de inmediato antes de configurar su cuenta en la consola:
> ```json
> {
>   "project_info": {
>     "project_number": "123456",
>     "project_id": "mock_mindfuldays",
>     "storage_bucket": "mock_mindfuldays.firebasestorage.app"
>   },
>   "client": [
>     {
>       "client_info": {
>         "mobilesdk_app_id": "1:123456:android:mock",
>         "android_client_info": { "package_name": "dev.mindfuldays.app" }
>       },
>       "api_key": [{ "current_key": "123456-mock" }]
>     }
>   ],
>   "configuration_version": "1"
> }
> ```

### 2. Activación de la Gemini API en la Consola
1. En el menú lateral de Firebase Console, ve a **Build** → **AI Logic** (o **Vertex AI in Firebase**).
2. Haz clic en el botón de activación de la Gemini API y sigue las instrucciones para habilitar la API en Google Cloud asociado.

### 3. Configuración de Gradle
Agrega el plugin de Google Services y las dependencias de Firebase AI Logic en tu proyecto:

En el archivo raíz `build.gradle.kts` (o `gradle/libs.versions.toml`):
```kotlin
plugins {
    // Plugin de Google Services
    id("com.google.gms.google-services") version "4.4.2" apply false
}
```

En el archivo `app/build.gradle.kts`:
```kotlin
plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.compose.compiler)
    id("com.google.gms.google-services") // Aplica el plugin de Google Services
}

dependencies {
    // Firebase BoM y Firebase AI Logic SDK
    implementation(platform("com.google.firebase:firebase-bom:34.12.0"))
    implementation("com.google.firebase:firebase-ai")

    // Firebase App Check para validación de seguridad (Debug y Play Integrity)
    implementation("com.google.firebase:firebase-appcheck-debug")
    implementation("com.google.firebase:firebase-appcheck-playintegrity")
}
```

### 4. Atestación de Seguridad con Firebase App Check (Debug Token)
Siguiendo la guía de JetPacker, para probar la comunicación de IA en un entorno de desarrollo local (emulador o dispositivo físico):
1. Ejecuta la aplicación en Android Studio.
2. Abre la pestaña **Logcat** y filtra por el término `DebugAppCheckProvider`.
3. Verás una línea de log similar a:
   ```text
   Enter this debug secret into the allow list in the Firebase Console for your project: a8c2dd4c-7f7f-4764-b653-ef6c114ba27e
   ```
4. Copia el token secreto y regístralo en **Firebase Console** en **App Check** → **Apps** → **Manage Debug Tokens**.

---

## 🎨 3.3. Configuración del Tema y Tokens en Compose

Crea el archivo `dev/mindfuldays/app/ui/theme/Color.kt`:

```kotlin
package dev.mindfuldays.app.ui.theme

import androidx.compose.ui.graphics.Color

val SageGreen = Color(0xFF6B8E23)
val SageGreenLight = Color(0xFF8FA853)
val SandMuted = Color(0xFFE8DFD8)
val WarmOffWhite = Color(0xFFFBF9F5)
val ForestDark = Color(0xFF2C3E35)
val PureWhite = Color(0xFFFFFFFF)
```

Crea el archivo `dev/mindfuldays/app/ui/theme/Theme.kt`:

```kotlin
package dev.mindfuldays.app.ui.theme

import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.lightColorScheme
import androidx.compose.runtime.Composable

private val LightColorScheme = lightColorScheme(
    primary = SageGreen,
    secondary = SandMuted,
    background = WarmOffWhite,
    surface = PureWhite,
    onPrimary = PureWhite,
    onBackground = ForestDark,
    onSurface = ForestDark
)

@Composable
fun MindfulDaysTheme(content: @Composable () -> Unit) {
    MaterialTheme(
        colorScheme = LightColorScheme,
        content = content
    )
}
```

---

## 🧠 3.4. Modelo de Datos y Calculador de las 9 Actitudes

Crea la data class en `dev/mindfuldays/app/data/model/MindfulnessAttitude.kt`:

```kotlin
package dev.mindfuldays.app.data.model

data class MindfulnessAttitude(
    val id: Int,
    val title: String,
    val description: String
)
```

Crea el repositorio en `dev/mindfuldays/app/data/repository/AttitudeRepository.kt`:

```kotlin
package dev.mindfuldays.app.data.repository

import dev.mindfuldays.app.data.model.MindfulnessAttitude
import java.util.Calendar

class AttitudeRepository {

    val attitudes = listOf(
        MindfulnessAttitude(1, "Mente de Principiante", "Mira las cosas como si fuera la primera vez, libre de expectativas."),
        MindfulnessAttitude(2, "No Juicio", "Observa tus pensamientos y sentimientos sin etiquetarlos como buenos o malos."),
        MindfulnessAttitude(3, "Aceptación", "Reconoce y acoge el momento presente exactamente como es."),
        MindfulnessAttitude(4, "Desapego", "Deja ir los pensamientos y deseos que intentan atrapar tu atención."),
        MindfulnessAttitude(5, "Confianza", "Desarrolla una creencia básica en ti mismo y en las señales de tu cuerpo."),
        MindfulnessAttitude(6, "No Esforzarse", "Abandona la necesidad constante de alcanzar un resultado inmediato."),
        MindfulnessAttitude(7, "Paciencia", "Comprende que ciertas cosas necesitan tiempo para desarrollarse."),
        MindfulnessAttitude(8, "Gratitud", "Aprecia el momento presente y valora lo que ya posees."),
        MindfulnessAttitude(9, "Generosidad", "Ofrece atención, cariño y presencia con el corazón abierto.")
    )

    fun getTodayAttitude(): MindfulnessAttitude {
        val dayOfYear = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)
        val index = (dayOfYear - 1) % attitudes.size
        return attitudes[index]
    }
}
```

---

## 🤖 3.5. Integración con Gemini API usando Firebase AI Logic (Patrón Museum Assistant con Gemini 3.5 flash-lite)

En el proyecto de referencia [JetPacker (Museum Assistant)](https://github.com/android/ai-samples/tree/main/jetpacker), la integración con Gemini se realiza a través de **Firebase AI Logic** con el modelo **`gemini-3.5-flash-lite`** y `GenerativeBackend.googleAI()`.

La gran ventaja de este enfoque es la utilización de:
1. `Firebase.ai(backend = GenerativeBackend.googleAI())`: Punto de entrada nativo del SDK de Firebase AI.
2. `modelName = "gemini-3.5-flash-lite"`: El modelo más moderno, ultrarrápido y eficiente de Google para asistentes y reflexiones en tiempo real.
3. `systemInstruction`: Delimita la personalidad del modelo (sereno, acogedor, máximo 2 oraciones, sin formato complejo).
4. `generateContent` o `startChat()`: Permite generar reflexiones puntuales o iniciar un diálogo interactivo de mindfulness.

Crea el archivo en `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:

```kotlin
package dev.mindfuldays.app.data.remote

import com.google.firebase.Firebase
import com.google.firebase.ai.ai
import com.google.firebase.ai.type.GenerativeBackend
import com.google.firebase.ai.type.content
import kotlinx.coroutines.CancellationException
import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.withContext

class GeminiApiService {

    // Modelo generativo inicializado mediante Firebase AI Logic (idéntico a Museum Assistant en JetPacker)
    private val generativeModel = Firebase.ai(backend = GenerativeBackend.googleAI())
        .generativeModel(
            modelName = "gemini-3.5-flash-lite",
            systemInstruction = content {
                text(
                    "Eres un asistente sereno, sabio y acogedor de mindfulness en la aplicación MindfulDays. " +
                    "Tu propósito es generar reflexiones breves para cultivar la atención plena diaria según las 9 actitudes de Jon Kabat-Zinn. " +
                    "Responde siempre con un máximo de 2 oraciones breves, poéticas e inspiradoras. " +
                    "Nunca utilices markdown complejo ni caracteres especiales, utiliza texto plano y sereno."
                )
            }
        )

    /**
     * Genera una reflexión diaria personalizada para la actitud indicada.
     */
    suspend fun generateReflection(attitudeTitle: String): String = withContext(Dispatchers.IO) {
        try {
            val prompt = "Escribe una reflexión inspiradora de 2 oraciones sobre la actitud de mindfulness: $attitudeTitle."
            val response = generativeModel.generateContent(prompt)
            response.text?.trim() ?: "Acoge el momento presente exactamente como se manifiesta."
        } catch (e: Exception) {
            if (e is CancellationException) throw e
            // Fallback amigable para modo offline o error de comunicación
            "Conectado en modo offline. Practica la reflexión: Respira profundo y enfoca tu atención en el momento presente."
        }
    }

    /**
     * Bonus: Soporte para Chat Interactivo Multi-Turno (idéntico al Chatbot de JetPacker).
     */
    fun startMindfulnessChat() = generativeModel.startChat()
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

    fun generateAiReflection() {
        viewModelScope.launch {
            _uiState.update { it.copy(isLoadingAi = true) }
            val attitudeTitle = _uiState.value.attitude.title
            val reflection = geminiService.generateReflection(attitudeTitle)
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

## 📱 3.6. Implementando la Home Screen en Jetpack Compose

Crea el archivo en `dev/mindfuldays/app/ui/home/HomeScreen.kt`:

```kotlin
package dev.mindfuldays.app.ui.home

import androidx.compose.foundation.layout.*
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.unit.dp
import dev.mindfuldays.app.data.model.MindfulnessAttitude

@Composable
fun HomeScreen(
    attitude: MindfulnessAttitude,
    aiReflection: String,
    isLoadingAi: Boolean,
    onGenerateAiReflection: () -> Unit,
    onNavigateToTimer: () -> Unit
) {
    Surface(
        modifier = Modifier.fillMaxSize(),
        color = MaterialTheme.colorScheme.background
    ) {
        Column(
            modifier = Modifier
                .fillMaxSize()
                .padding(24.dp),
            horizontalAlignment = Alignment.CenterHorizontally,
            verticalArrangement = Arrangement.SpaceBetween
        ) {
            // Header
            Column(horizontalAlignment = Alignment.CenterHorizontally) {
                Text(
                    text = "MINDFULDAYS",
                    style = MaterialTheme.typography.labelLarge,
                    color = MaterialTheme.colorScheme.primary
                )
                Spacer(modifier = Modifier.height(8.dp))
                Text(
                    text = "Actitud ${attitude.id} de 9",
                    style = MaterialTheme.typography.bodyMedium
                )
            }

            // Tarjeta Central
            Card(
                modifier = Modifier
                    .fillMaxWidth()
                    .padding(vertical = 16.dp),
                colors = CardDefaults.cardColors(containerColor = MaterialTheme.colorScheme.surface),
                elevation = CardDefaults.cardElevation(defaultElevation = 4.dp)
            ) {
                Column(modifier = Modifier.padding(20.dp)) {
                    Text(
                        text = attitude.title,
                        style = MaterialTheme.typography.headlineMedium,
                        color = MaterialTheme.colorScheme.primary
                    )
                    Spacer(modifier = Modifier.height(8.dp))
                    Text(
                        text = attitude.description,
                        style = MaterialTheme.typography.bodyLarge
                    )

                    Spacer(modifier = Modifier.height(16.dp))
                    Divider(color = MaterialTheme.colorScheme.secondary)
                    Spacer(modifier = Modifier.height(16.dp))

                    if (isLoadingAi) {
                        CircularProgressIndicator(
                            modifier = Modifier.align(Alignment.CenterHorizontally),
                            color = MaterialTheme.colorScheme.primary
                        )
                    } else {
                        Text(
                            text = if (aiReflection.isNotBlank()) aiReflection else "Haz clic abajo para generar una reflexión con IA.",
                            style = MaterialTheme.typography.bodyMedium,
                            color = MaterialTheme.colorScheme.onSurface
                        )
                    }

                    Spacer(modifier = Modifier.height(16.dp))
                    Button(
                        onClick = onGenerateAiReflection,
                        modifier = Modifier.fillMaxWidth(),
                        colors = ButtonDefaults.buttonColors(containerColor = MaterialTheme.colorScheme.primary)
                    ) {
                        Text("✨ Nueva Reflexión (Gemini IA)")
                    }
                }
            }

            // Acción de Navegación hacia el Temporizador
            OutlinedButton(
                onClick = onNavigateToTimer,
                modifier = Modifier.fillMaxWidth()
            ) {
                Text("⏱️ Iniciar Temporizador de Meditación")
            }
        }
    }
}
```

---

Con las pantallas y la comunicación con la API listas, la app está preparada para pruebas y automatización. Avanzamos hacia el **Módulo 4: Calidad de Código, Pruebas Automatizadas y CI/CD en GitHub**.
