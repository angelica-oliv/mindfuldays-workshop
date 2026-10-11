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
2. **Gemini API com Firebase AI Logic**:
   - Utilizar a biblioteca oficial `com.google.firebase:firebase-ai` com o backend `GenerativeBackend.googleAI()`.
   - Utilizar o modelo mais recente: `gemini-3.5-flash-lite`.
   - Gerar reflexões concisas e inspiradoras com no máximo 2 frases para cada atitude.
   - Tratar ausência de conexão e exceções com fallback amigável offline sem quebrar o app.

## 🛠️ Comandos de Verificação e Validação
Sempre verifique as alterações utilizando os seguintes comandos no terminal:
- **Compilação do app**: `./gradlew assembleDebug`
- **Testes Unitários**: `./gradlew testDebugUnitTest`
- **Linter & Análise Estática**: `./gradlew lintDebug`

## 🚫 Restrições Rígidas (Guardrails)
- **NUNCA** faça hardcode de credenciais ou chaves de API (`apiKey`) no código. A autenticação é gerenciada com segurança pelo Firebase via `google-services.json` e Firebase App Check.
- **NÃO** misture lógica de negócios ou chamadas assíncronas de rede diretamente dentro de funções `@Composable`.
- Mantenha funções Composable limpas e desacopladas, utilizando parâmetros para eventos e lambdas (`onAction: () -> Unit`) para facilitar testes de UI.
- Use nomes descritivos em português para textos de interface visível e inglês para código técnico, métodos e classes.
```

Com o `AGENTS.md` configurado na raiz do projeto, qualquer agente (como o Gemini no Android Studio) passará a produzir código alinhado com o seu design system e suas regras de negócio.

---

## 🔥 3.2. Configuração do Firebase e Firebase AI Logic (Instruções Estilo JetPacker)

A forma recomendada e mais moderna pelo Google para integrar a **Gemini API** em aplicativos Android é através do **Firebase AI Logic** (`com.google.firebase:firebase-ai`), conforme demonstrado no repositório de referência oficial da equipe do Android: [android/ai-samples/jetpacker](https://github.com/android/ai-samples/tree/main/jetpacker).

Diferente de chamadas HTTP diretas ou do antigo SDK com chaves de API expostas, o Firebase AI Logic oferece:
* **Segurança Reforçada**: Elimina a necessidade de trafegar API keys expostas no código cliente por meio do **Firebase App Check** e atestação Play Integrity.
* **Backend Otimizado**: Integração direta com `GenerativeBackend.googleAI()`.
* **Aderência aos Modelos Mais Novos**: Suporte nativo ao modelo **`gemini-3.5-flash-lite`**, otimizado para baixíssima latência e respostas concisas em tempo real.

Siga os 4 passos de configuração descritos a seguir:

### 1. Criação do Projeto no Console do Firebase
1. Acesse o [Firebase Console](https://console.firebase.google.com/) e faça login com sua conta Google.
2. Crie um novo projeto (ex: `MindfulDays`) ou selecione um existente.
3. Adicione um novo aplicativo Android informando o **Package Name** do projeto:
   * **Package Name**: `dev.mindfuldays.app`
4. Baixe o arquivo de configuração `google-services.json` gerado pelo Firebase.
5. Salve o arquivo dentro do diretório `app/` do seu projeto (`MindfulDays/app/google-services.json`).

> [!TIP]
> **Arquivo Mock Placeholder para Compilação Local:**
> Assim como no projeto de referência [JetPacker](https://github.com/android/ai-samples/tree/main/jetpacker), você pode manter um arquivo mock `app/google-services.json` inicial no projeto para que qualquer pessoa consiga compilar via Gradle imediatamente antes mesmo de cadastrar sua conta no console:
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

### 2. Ativação da Gemini API no Console
1. No menu lateral do Firebase Console, acesse **Build** → **AI Logic** (ou **Vertex AI in Firebase**).
2. Clique no botão de ativação da Gemini API e conclua as instruções para habilitar a API no Google Cloud associado.

### 3. Configuração do Gradle
Adicione o plugin do Google Services e as dependências do Firebase AI Logic no seu projeto:

No arquivo raiz `build.gradle.kts` (ou `gradle/libs.versions.toml`):
```kotlin
plugins {
    // Plugin do Google Services
    id("com.google.gms.google-services") version "4.5.0" apply false
}
```

No arquivo `app/build.gradle.kts`:
```kotlin
plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.compose.compiler)
    id("com.google.gms.google-services") // Aplica o plugin do Google Services
}

dependencies {
    // Firebase BoM e Firebase AI Logic SDK
    implementation(platform("com.google.firebase:firebase-bom:34.12.0"))
    implementation("com.google.firebase:firebase-ai")

    // Firebase App Check para validação de segurança (Debug e Play Integrity)
    implementation("com.google.firebase:firebase-appcheck-debug")
    implementation("com.google.firebase:firebase-appcheck-playintegrity")
}
```

### 4. Atestação de Segurança com Firebase App Check (Debug Token)
Seguindo o guia do JetPacker, para testar a comunicação de IA em ambiente de desenvolvimento local (emulador ou aparelho físico):
1. Execute o aplicativo no Android Studio.
2. Abra a aba **Logcat** e filtre pelo termo `DebugAppCheckProvider`.
3. Localize uma linha de log similar a:
   ```text
   Enter this debug secret into the allow list in the Firebase Console for your project: a8c2dd4c-7f7f-4764-b653-ef6c114ba27e
   ```
4. Copie o token secreto e registre-o no **Firebase Console** em **App Check** → **Apps** → **Manage Debug Tokens**.

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

## 🤖 3.4. Integração com Gemini API usando Firebase AI Logic (Padrão Museum Assistant com Gemini 3.5 flash-lite)

No projeto de referência [JetPacker (Museum Assistant)](https://github.com/android/ai-samples/tree/main/jetpacker), a integração com o Gemini é realizada através do **Firebase AI Logic** com o modelo **`gemini-3.5-flash-lite`** e `GenerativeBackend.googleAI()`.

A grande vantagem dessa abordagem é a utilização de:
1. `Firebase.ai(backend = GenerativeBackend.googleAI())`: Ponto de entrada nativo do SDK do Firebase AI.
2. `modelName = "gemini-3.5-flash-lite"`: O modelo mais moderno, ultrarrápido e eficiente do Google para assistentes e reflexões em tempo real.
3. `systemInstruction`: Delimita a personalidade do modelo (calmo, acolhedor, no máximo 2 frases, sem formatação complexa).
4. `generateContent` ou `startChat()`: Permite gerar reflexões pontuais ou iniciar um diálogo interativo de mindfulness.

Crie o arquivo em `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:

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

    // Modelo generativo inicializado via Firebase AI Logic (idêntico ao Museum Assistant do JetPacker)
    private val generativeModel = Firebase.ai(backend = GenerativeBackend.googleAI())
        .generativeModel(
            modelName = "gemini-3.5-flash-lite",
            systemInstruction = content {
                text(
                    "Você é um assistente calmo, sábio e acolhedor de mindfulness no aplicativo MindfulDays. " +
                    "Seu propósito é gerar reflexões serenas para cultivar a atenção plena no dia a dia com base nas 9 atitudes de Jon Kabat-Zinn. " +
                    "Responda sempre com no máximo 2 frases curtas, poéticas e inspiradoras. " +
                    "Nunca use formatação complexa ou markdown, utilize texto simples e sereno."
                )
            }
        )

    /**
     * Gera uma reflexão diária personalizada para a atitude informada.
     */
    suspend fun generateReflection(attitudeTitle: String): String = withContext(Dispatchers.IO) {
        try {
            val prompt = "Escreva uma reflexão inspiradora de 2 frases sobre a atitude de mindfulness: $attitudeTitle."
            val response = generativeModel.generateContent(prompt)
            response.text?.trim() ?: "Acolha o momento presente exatamente como ele se manifesta."
        } catch (e: Exception) {
            if (e is CancellationException) throw e
            // Fallback amigável para modo offline ou erro de comunicação
            "Conectado no modo offline. Pratique a reflexão: Respire fundo e traga sua atenção para o momento presente."
        }
    }

    /**
     * Bônus: Suporte a Chat Interativo Multi-Turno (idêntico ao Chatbot do JetPacker).
     */
    fun startMindfulnessChat() = generativeModel.startChat()
}
```

Agora, crie o ViewModel que conecta o repositório, o serviço do Gemini e o estado da UI em `dev/mindfuldays/app/ui/viewmodel/MindfulnessViewModel.kt`:

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
