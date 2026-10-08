# 🧩 Módulo 3 — UI em Jetpack Compose, Regra das 9 Atitudes e Gemini API

Neste módulo, vamos estruturar o arquivo **AGENTS.md** para fornecer o contexto operacional a agentes de IA, implementar a lógica de negócio do aplicativo **MindfulDays**, configurar o tema Material Design 3 e construir as telas com **Jetpack Compose**.

---

## 🤖 3.1. Diretrizes para Agentes de IA: Criando o Arquivo `AGENTS.md`

Antes de iniciar a implementação do código e das telas, vamos configurar um dos recursos mais estratégicos para o desenvolvimento moderno orientado por inteligência artificial: o arquivo **`AGENTS.md`**.

### 🌟 Por que o `AGENTS.md` é tão importante?

Assim como o `README.md` orienta pessoas desenvolvedoras sobre o projeto, o **`AGENTS.md`** é uma convenção aberta adotada pela comunidade para servir como a **fonte única de verdade operacional para agentes autônomos e assistentes de código com IA** (como o Gemini no Android Studio, Cursor, Claude Code, GitHub Copilot Workspace e Antigravity).

Ao trabalhar com IA no desenvolvimento móvel, o maior desafio não é a capacidade de gerar código, mas sim a **precisão e aderência ao contexto**. Sem instruções explícitas, os modelos de IA podem sofrer de alucinações, sugerir dependências incompatíveis, misturar código legado (como layouts XML antigos em vez de Jetpack Compose) ou quebrar padrões arquiteturais.

O `AGENTS.md` resolve esses desafios entregando:

1. **Grounding e Redução Drástica de Alucinações**: O arquivo ancora a IA nas decisões técnicas já tomadas, eliminando suposições e mantendo o agente focado nas diretrizes exatas do projeto.
2. **Consistência de Stack e Arquitetura**: Garante que qualquer código gerado respeite estritamente o padrão **MVVM**, **Clean Architecture**, **Kotlin idiomático** e **Jetpack Compose com Material Design 3**.
3. **Fidelidade aos Design Tokens e Regras de Negócio**: A IA terá sempre à mão a paleta de cores oficial extraída no Stitch (`SageGreen`, `SandMuted`, etc.) e a lógica de rotação cíclica das 9 atitudes de Jon Kabat-Zinn.
4. **Guardrails de Segurança**: Define limites essenciais, como a proibição explícita de fazer hardcode de chaves secretas (`apiKey`) ou acoplar lógica de domínio dentro de composables.
5. **Autonomia em Execução e Auto-correção (Self-Healing)**: Especifica os comandos exatos de compilação, lint e testes (`./gradlew assembleDebug`, `./gradlew testDebugUnitTest`), permitindo que agentes autônomos executem, validem e corrijam eventuais falhas antes de finalizar uma tarefa.
6. **Economia de Contexto e Tokens**: Elimina a necessidade de repetir prompts gigantescos a cada nova tela ou funcionalidade solicitada.

---

### 📝 Criando o arquivo `AGENTS.md`

Crie o arquivo `AGENTS.md` diretamente na **raiz do seu projeto Android** (`MindfulDays/AGENTS.md`):

```markdown
# 🧘 MindfulDays — Diretrizes e Contexto para Agentes de IA

Este arquivo atua como a fonte de verdade para agentes de IA e ferramentas de assistência de código que atuam neste repositório.

## 📱 Visão Geral do Projeto
O **MindfulDays** é um aplicativo Android nativo focado em mindfulness e saúde mental, baseado nas **9 Atitudes de Mindfulness de Jon Kabat-Zinn**, com suporte a reflexões diárias geradas via **Google Gemini API** e um timer circular de meditação.

## 🏗️ Padrões de Arquitetura e Stack Técnica
- **Linguagem**: Kotlin 1.9+ (uso idiomático de coroutines, StateFlow e imutabilidade).
- **UI Toolkit**: Jetpack Compose com Material Design 3 (M3). **Proibido o uso de layouts XML tradicionais**.
- **Padrão de Arquitetura**: MVVM (Model-View-ViewModel) alinhado com Clean Architecture:
  - `data/model/`: Data classes imutáveis.
  - `data/repository/`: Repositórios para fonte de dados local e lógica das 9 atitudes.
  - `data/remote/`: Clientes e serviços para comunicação com a Gemini API.
  - `ui/`: Telas e componentes em Compose divididos por feature (`home`, `timer`, `settings`).
  - `ui/theme/`: Tokens visuais (Color, Theme, Type).
  - `ui/viewmodel/`: ViewModels expondo estados via `StateFlow`.
- **Pacote Base**: `dev.mindfuldays.app`.

## 🎨 Design Tokens (Material Design 3)
Respeite estritamente a paleta de cores definida nos protótipos do Google Stitch:
- `SageGreen` (`#6B8E23`): Cor primária (tranquilidade, foco).
- `SageGreenLight` (`#8FA853`): Variante suave para destaques secundários.
- `SandMuted` (`#E8DFD8`): Cor secundária e divisores.
- `WarmOffWhite` (`#FBF9F5`): Fundo padrão das telas.
- `PureWhite` (`#FFFFFF`): Fundo de cards elevados e superfícies.
- `ForestDark` (`#2C3E35`): Texto principal e ícones de alto contraste.

## 🧠 Regras de Negócio Fundamentais
1. **Regra das 9 Atitudes**: A lista contém exatamente 9 atitudes fixas. O cálculo da atitude diária deve usar o dia do ano:
   `val index = (Calendar.getInstance().get(Calendar.DAY_OF_YEAR) - 1) % 9`
2. **Gemini API (Reflexões Diárias)**:
   - Utilizar o endpoint do modelo `gemini-1.5-flash:generateContent`.
   - Gerar reflexões concisas e inspiradoras com no máximo 2 frases para cada atitude.
   - Tratar ausência de chave de API e erros de rede com fallback amigável offline sem quebrar o app.

## 🛠️ Comandos de Verificação e Validação
Sempre verifique as alterações utilizando os seguintes comandos no terminal:
- **Compilação do app**: `./gradlew assembleDebug`
- **Testes Unitários**: `./gradlew testDebugUnitTest`
- **Linter & Análise Estática**: `./gradlew lintDebug`

## 🚫 Restrições Rígidas (Guardrails)
- **NUNCA** faça hardcode de credenciais ou chaves de API (`apiKey`) no código versionado.
- **NÃO** misture lógica de negócios ou chamadas assíncronas de rede diretamente dentro de funções `@Composable`.
- Mantenha funções Composable limpas e desacopladas, utilizando parâmetros para eventos e lambdas (`onAction: () -> Unit`) para facilitar testes de UI.
- Use nomes descritivos em português para textos de interface visível e inglês para código técnico, métodos e classes.
```

Com o `AGENTS.md` configurado na raiz do projeto, qualquer agente (como o Gemini no Android Studio) passará a produzir código alinhado com o seu design system e suas regras de negócio.

---

## 🎨 3.2. Configuração do Tema e Tokens no Compose

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

## 🧠 3.3. Modelo de Dados e Calculador das 9 Atitudes

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

## 🤖 3.4. Integração com Gemini API para Reflexões Diárias

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
            return@withContext "Configure sua GEMINI_API_KEY no arquivo local.properties para gerar reflexões personalizadas."
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

## 📱 3.5. Implementando a Home Screen em Jetpack Compose

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
