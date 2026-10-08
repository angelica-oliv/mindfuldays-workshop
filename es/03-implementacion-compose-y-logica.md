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
2. **Gemini API (Reflexiones Diarias)**:
   - Utilizar el endpoint del modelo `gemini-1.5-flash:generateContent`.
   - Generar reflexiones concisas e inspiradoras con un máximo de 2 oraciones por actitud.
   - Manejar la ausencia de clave de API y errores de red con un mensaje amigable offline sin romper la app.

## 🛠️ Comandos de Verificación y Validación
Verifica siempre los cambios utilizando los siguientes comandos en la terminal:
- **Compilación de la app**: `./gradlew assembleDebug`
- **Pruebas Unitarias**: `./gradlew testDebugUnitTest`
- **Linter y Análisis Estático**: `./gradlew lintDebug`

## 🚫 Restricciones Estrictas (Guardrails)
- **NUNCA** hagas commit ni dejes credenciales o claves de API (`apiKey`) hardcodeadas en el código versionado.
- **NO** mezcles lógica de negocio o llamadas asíncronas de red directamente dentro de funciones `@Composable`.
- Mantén las funciones Composable limpias y desacopladas, utilizando parámetros para eventos y lambdas (`onAction: () -> Unit`) para facilitar pruebas de UI.
- Utiliza nombres descriptivos en español para textos de interfaz visible e inglés para código técnico, métodos y clases.
```

Con `AGENTS.md` configurado en la raíz del proyecto, cualquier agente (como Gemini en Android Studio) producirá código perfectamente alineado con tu sistema de diseño y tus reglas de negocio.

---

## 🎨 3.2. Configuración del Tema y Tokens en Compose

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

## 🧠 3.3. Modelo de Datos y Calculador de las 9 Actitudes

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

## 🤖 3.4. Integración con Gemini API para Reflexiones Diarias

Crea la interfaz de servicio en `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:

```kotlin
package dev.mindfuldays.app.data.remote

import kotlinx.coroutines.Dispatchers
import kotlinx.coroutines.withContext
import java.net.HttpURLConnection
import java.net.URL
import org.json.JSONObject

class GeminiApiService(private val apiKey: String) {

    suspend fun generateReflection(attitudeTitle: String): String = withContext(Dispatchers.IO) {
        if (apiKey.isBlank()) {
            return@withContext "Configura tu GEMINI_API_KEY en el archivo local.properties para generar reflexiones personalizadas."
        }

        try {
            val url = URL("https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=$apiKey")
            val connection = url.openConnection() as HttpURLConnection
            connection.requestMethod = "POST"
            connection.setRequestProperty("Content-Type", "application/json")
            connection.doOutput = true

            val prompt = "Escribe una reflexión inspiradora de 2 oraciones sobre la actitud de mindfulness: $attitudeTitle."
            val jsonBody = JSONObject().apply {
                put("contents", listOf(JSONObject().apply {
                    put("parts", listOf(JSONObject().apply {
                        put("text", prompt)
                    }))
                }))
            }

            connection.outputStream.use { os ->
                os.write(jsonBody.toString().toByteArray())
            }

            if (connection.responseCode == 200) {
                val responseText = connection.inputStream.bufferedReader().use { it.readText() }
                val jsonResponse = JSONObject(responseText)
                val text = jsonResponse
                    .getJSONArray("candidates")
                    .getJSONObject(0)
                    .getJSONObject("content")
                    .getJSONArray("parts")
                    .getJSONObject(0)
                    .getString("text")
                text.trim()
            } else {
                "No fue posible conectar con Gemini. Intenta nuevamente en unos instantes."
            }
        } catch (e: Exception) {
            "Conectado en modo offline. Practica la reflexión: Concéntrate en tu respiración hoy."
        }
    }
}
```

---

## 📱 3.5. Implementando la Home Screen en Jetpack Compose

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
