# 🧩 Módulo 3 — UI em Jetpack Compose, Regra das 9 Atitudes e Gemini API

Neste módulo, vamos implementar a lógica de negócio do aplicativo **MindfulDays**, configurar o tema Material Design 3 e construir as telas com **Jetpack Compose**.

---

## 🎨 3.1. Configuração do Tema e Tokens no Compose

Crie o arquivo `dev/mindfuldays/app/ui/theme/Color.kt`:

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

Crie o arquivo `dev/mindfuldays/app/ui/theme/Theme.kt`:

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

## 🧠 3.2. Modelo de Dados e Calculador das 9 Atitudes

Crie a data class em `dev/mindfuldays/app/data/model/MindfulnessAttitude.kt`:

```kotlin
package dev.mindfuldays.app.data.model

data class MindfulnessAttitude(
    val id: Int,
    val title: String,
    val description: String
)
```

Crie o repositório em `dev/mindfuldays/app/data/repository/AttitudeRepository.kt`:

```kotlin
package dev.mindfuldays.app.data.repository

import dev.mindfuldays.app.data.model.MindfulnessAttitude
import java.util.Calendar

class AttitudeRepository {

    val attitudes = listOf(
        MindfulnessAttitude(1, "Mente de Principiante", "Olhe para as coisas como se fosse a primeira vez, livre de expectativas."),
        MindfulnessAttitude(2, "Não-Julgamento", "Observe seus pensamentos e sentimentos sem rotulá-los como bons ou ruins."),
        MindfulnessAttitude(3, "Aceitação", "Reconheça e acolha o momento presente exatamente como ele é."),
        MindfulnessAttitude(4, "Desapego", "Deixe ir pensamentos e desejos que tentam prender sua atenção."),
        MindfulnessAttitude(5, "Confiança", "Desenvolva uma crença básica em si mesmo e nos seus sinais corporais."),
        MindfulnessAttitude(6, "Não-Esforço", "Abandone a necessidade constante de alcançar um resultado imediato."),
        MindfulnessAttitude(7, "Paciência", "Compreenda que certas coisas precisam de tempo para se desenvolver."),
        MindfulnessAttitude(8, "Gratidão", "Aprecie o momento presente e valorize o que você já possui."),
        MindfulnessAttitude(9, "Generosidade", "Ofereça atenção, carinho e presença com o coração aberto.")
    )

    fun getTodayAttitude(): MindfulnessAttitude {
        val dayOfYear = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)
        val index = (dayOfYear - 1) % attitudes.size
        return attitudes[index]
    }
}
```

---

## 🤖 3.3. Integração com Gemini API para Reflexões Diárias

Crie a interface de serviço em `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:

```kotlin
package dev.mindfuldays.app.data.remote

import kotlinx.coroutines.dispatchers.Dispatchers
import kotlinx.coroutines.withContext
import java.net.HttpURLConnection
import java.net.URL
import org.json.JSONObject

class GeminiApiService(private val apiKey: String) {

    suspend fun generateReflection(attitudeTitle: String): String = withContext(Dispatchers.IO) {
        if (apiKey.isBlank()) {
            return@withContext "Insira sua API Key do Gemini nas configurações para gerar reflexões personalizadas."
        }

        try {
            val url = URL("https://generativelanguage.googleapis.com/v1beta/models/gemini-1.5-flash:generateContent?key=$apiKey")
            val connection = url.openConnection() as HttpURLConnection
            connection.requestMethod = "POST"
            connection.setRequestProperty("Content-Type", "application/json")
            connection.doOutput = true

            val prompt = "Escreva uma reflexão inspiradora de 2 frases sobre a atitude de mindfulness: $attitudeTitle."
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
                "Não foi possível conectar ao Gemini. Tente novamente em instantes."
            }
        } catch (e: Exception) {
            "Conectado no modo offline. Pratique a reflexão: Concentre-se na sua respiração hoje."
        }
    }
}
```

---

## 📱 3.4. Implementando a Home Screen em Jetpack Compose

Crie o arquivo em `dev/mindfuldays/app/ui/home/HomeScreen.kt`:

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
                    text = "Atitude ${attitude.id} de 9",
                    style = MaterialTheme.typography.bodyMedium
                )
            }

            // Card Central
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
                            text = if (aiReflection.isNotBlank()) aiReflection else "Clique abaixo para gerar uma reflexão com IA.",
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
                        Text("✨ Nova Reflexão (Gemini IA)")
                    }
                }
            }

            // Ação de Navegação para o Timer
            OutlinedButton(
                onClick = onNavigateToTimer,
                modifier = Modifier.fillMaxWidth()
            ) {
                Text("⏱️ Iniciar Timer de Meditação")
            }
        }
    }
}
```

---

Com as telas e a comunicação com a API prontas, o app está pronto para testes e automação. Avançamos para o **Módulo 4: Qualidade, Testes e CI/CD com GitHub Actions**.
