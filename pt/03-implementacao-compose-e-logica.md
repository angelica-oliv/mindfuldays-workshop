# 🧩 Módulo 3 — AGENTS.md, Regra das 9 Atitudes, Gemini API e UI em Compose

Neste módulo, vamos estruturar o arquivo **`AGENTS.md`** como contexto operacional para agentes de IA, configurar o acesso seguro à **Gemini API** e focar apenas nas **peças-chave de código e arquitetura**, delegando o código repetitivo (*boilerplate*) ao assistente de IA por meio de prompts guiados.

---

## 🤖 3.1. Diretrizes para Agentes de IA: Criando o Arquivo `AGENTS.md`

Antes de pedir para a IA implementar ou refatorar arquivos do projeto, vamos configurar o nosso recurso mais estratégico: o arquivo **`AGENTS.md`**.

### 🌟 Por que o `AGENTS.md` é tão importante?

Assim como o `README.md` orienta pessoas desenvolvedoras, o **`AGENTS.md`** atua como a **fonte única de verdade operacional para agentes autônomos e assistentes de código com IA** (como Gemini no Android Studio, Cursor, Claude Code, GitHub Copilot e Antigravity).

1. **Grounding e Redução de Alucinações**: Ancora a IA nas decisões técnicas já tomadas.
2. **Consistência de Stack e Arquitetura**: Garante o respeito estrito a **MVVM**, **Clean Architecture**, **Kotlin idiomático** e **Jetpack Compose com Material Design 3**.
3. **Fidelidade aos Design Tokens e Regras de Negócio**: Mantém sempre à mão a paleta oficial extraída no Stitch e a rotação cíclica das 9 atitudes de Jon Kabat-Zinn.
4. **Guardrails de Segurança**: Proíbe explicitamente chaves secretas (`apiKey`) hardcoded ou cores hexadecimais fixas em Composables.
5. **Prompts mais curtos e rápidos no Workshop**: Com o `AGENTS.md` na raiz do projeto, você não precisa repetir regras arquiteturais nem paletas de cores a cada prompt.

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

## 🎨 Design Tokens & Temas (Material Design 3 — Light & Dark Mode)
Respeite estritamente os tokens de cores semânticos do Material 3, garantindo suporte perfeito e contraste adequado tanto em tema claro quanto escuro:

### Tema Claro (Light Theme):
- `primary`: Verde Sálvia (`#6B8E23`)
- `primaryContainer`: Sálvia Suave (`#8FA853`)
- `secondary`: Areia Muted (`#E8DFD8`)
- `background`: Off-White Calmo (`#FBF9F5`)
- `surface`: Branco Puro (`#FFFFFF`)
- `onBackground` / `onSurface`: Verde Floresta Escuro (`#2C3E35`)
- `onSurfaceVariant`: Verde Floresta Suave (`#5C6F64`)
- `outlineVariant`: Areia Muted (`#E8DFD8`)

### Tema Escuro (Dark Theme):
- `primary`: Sálvia Luminoso (`#A8C673`)
- `primaryContainer`: Floresta Escuro Elevado (`#2E4239`)
- `secondary`: Sálvia Suave (`#A3B5A8`)
- `background`: Floresta Noturno Profundo (`#15201A`)
- `surface`: Floresta Noturno Elevado (`#22322A`)
- `onBackground` / `onSurface`: Off-White Claro (`#F1EFEA`)
- `onSurfaceVariant`: Sálvia Muted Claro (`#A3B5A8`)
- `outlineVariant`: Borda Sutil Floresta (`#3B5045`)

## 🧠 Regras de Negócio Fundamentais
1. **Regra das 9 Atitudes**: A lista contém exatamente 9 atitudes fixas. O cálculo da atitude diária deve usar o dia do ano:
   `val index = (dayOfYear - 1).mod(attitudes.size)`
2. **Gemini API (Reflexões Diárias)**:
   - Utilizar o endpoint do modelo `gemini-3.8-flash:generateContent`.
   - Gerar reflexões concisas e inspiradoras com no máximo 2 frases para cada atitude, respeitando o idioma do usuário (pt, en, es).
   - Tratar ausência de chave de API e erros de rede com fallback amigável offline sem quebrar o app.

## 🛠️ Comandos de Verificação e Validação
Sempre verifique as alterações utilizando os seguintes comandos no terminal:
- **Compilação do app**: `./gradlew assembleDebug`
- **Testes Unitários**: `./gradlew testDebugUnitTest`
- **Testes de UI (Robot Pattern)**: `./gradlew connectedDebugAndroidTest`

## 🚫 Restrições Rígidas (Guardrails)
- **NUNCA faça hardcode de cores hexadecimais em Composables** (`Color(0xFF...)`). Utilize sempre `MaterialTheme.colorScheme.background`, `MaterialTheme.colorScheme.surface`, `MaterialTheme.colorScheme.onSurface`, etc., para evitar problemas de contraste no Dark Mode.
- **NUNCA** faça hardcode de credenciais ou chaves de API (`apiKey`) no código versionado. A chave deve ser configurada em `local.properties` e consumida via `BuildConfig.GEMINI_API_KEY`.
- **NÃO** misture lógica de negócios ou chamadas assíncronas de rede diretamente dentro de funções `@Composable`.
- Mantenha funções Composable limpas e desacopladas, utilizando parâmetros para eventos e lambdas (`onAction: () -> Unit`) para facilitar testes de UI.
- Use recursos internacionalizados (`stringResource(R.string...)`) para textos visíveis e inglês para código técnico, métodos e classes.
```

---

## 🔑 3.2. Configuração da Gemini API e Gerenciamento Seguro de Credenciais

Para integrar a **Gemini API** de forma segura e moderna, vamos configurar a chave no `local.properties` e as dependências do **Retrofit**, **Moshi** e **OkHttp**.

### 1. Obtenção e Ativação da API Key
1. Acesse o [Google AI Studio](https://aistudio.google.com/), clique em **Get API key** e copie a chave gerada.
2. Certifique-se de que a **Generative Language API** esteja ativada no seu console do Google Cloud (`https://console.developers.google.com/apis/api/generativelanguage.googleapis.com/overview`).

> [!WARNING]
> **Armadilha Comum — Chaves do Firebase (`API_KEY_SERVICE_BLOCKED` 403):**
> Nunca utilize chaves geradas automaticamente pelo Firebase para chamar o endpoint da Gemini API. Utilize sempre uma chave criada diretamente no **Google AI Studio**.

### 2. Armazenamento Seguro no `local.properties`
Abra o arquivo `local.properties` na raiz do projeto (ignorado pelo Git) e adicione:

```properties
GEMINI_API_KEY=sua_chave_do_ai_studio_aqui
```

### 3. Injeção via `buildConfigField` no `app/build.gradle.kts`
No arquivo `app/build.gradle.kts`, leia o `local.properties` e exponha a constante em `BuildConfig`:

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
        buildConfig = true // Habilita a geração da classe BuildConfig
    }
}
```

### 4. Dependências de Rede (`libs.versions.toml` e `app/build.gradle.kts`)
Adicione Retrofit, Moshi e OkHttp no `gradle/libs.versions.toml`:

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

E declare no bloco `dependencies` do `app/build.gradle.kts`:

```kotlin
dependencies {
    // Networking e Gemini API
    implementation(libs.retrofit)
    implementation(libs.converter.moshi)
    implementation(libs.moshi.kotlin)
    implementation(libs.okhttp)
    implementation(libs.logging.interceptor)
    "ksp"(libs.moshi.kotlin.codegen)
}
```

### 🤖 Prompt para Configurar `buildConfigField` e Dependências com IA
Se você não tem familiaridade com arquivos Gradle (`build.gradle.kts` e `libs.versions.toml`), peça ao assistente do Gemini no Android Studio para fazer essa configuração automaticamente para você:

```text
Seguindo @AGENTS.md, configure o acesso seguro à GEMINI_API_KEY e as dependências de rede no Gradle:
1. Em `app/build.gradle.kts`:
   - Leia a propriedade `GEMINI_API_KEY` do arquivo `local.properties` na raiz do projeto usando `java.util.Properties` (com fallback para `""` caso não exista).
   - Dentro de `android.defaultConfig`, injete o campo `buildConfigField("String", "GEMINI_API_KEY", "\"$geminiApiKey\"")`.
   - Dentro de `android.buildFeatures`, habilite `buildConfig = true`.
2. Verifique em `gradle/libs.versions.toml` e `app/build.gradle.kts` se estão declaradas e adicionadas as dependências de `retrofit`, `converter-moshi`, `moshi-kotlin`, `moshi-kotlin-codegen` (via ksp), `okhttp` e `logging-interceptor`.
3. Sincronize o projeto e verifique se a compilação passa sem erros.
```

---

## 🌐 3.3. Internacionalização (i18n) com IA (Inglês, Português e Espanhol)

Em vez de copiar e colar centenas de linhas de arquivos XML manualmente, usaremos o Gemini para gerar ou verificar as tabelas de recursos nos 3 idiomas (`values/strings.xml`, `values-pt/strings.xml` e `values-es/strings.xml`).

### 🔍 Estrutura-Chave do `strings.xml`
Garanta que seus arquivos de recursos sigam estes nomes de chaves padronizados (necessários para a UI e para os testes do Módulo 4):

```xml
<resources>
    <string name="app_name">MindfulDays</string>
    <string name="app_title">MINDFULDAYS</string>
    <string name="attitude_counter">Atitude %1$d de %2$d</string>
    <string name="default_reflection">“Respire fundo e traga sua atenção para o momento presente.”</string>
    <string name="btn_new_reflection">✨ Nova Reflexão (Gemini IA)</string>
    <string name="btn_start_timer">⏱️ Iniciar Timer de Meditação</string>
    <string name="cd_settings">Configurações</string>
    <!-- As 9 Atitudes: attitude_1_name / attitude_1_desc até attitude_9_name / attitude_9_desc -->
    <string name="attitude_1_name">Mente de Principiante</string>
    <string name="attitude_1_desc">Olhe para as coisas como se fosse a primeira vez, livre de expectativas.</string>
</resources>
```

### 🤖 Prompt para Gerar os Arquivos `strings.xml` (EN / PT / ES)
Abra o chat do Gemini no Android Studio e execute este prompt:

```text
Seguindo as diretrizes de @AGENTS.md, gere ou complete os 3 arquivos de recursos de strings para internacionalização:
1. app/src/main/res/values/strings.xml (Inglês padrão)
2. app/src/main/res/values-pt/strings.xml (Português)
3. app/src/main/res/values-es/strings.xml (Espanhol)

Inclua exatamente estas chaves nos 3 idiomas:
- Gerais e Home: app_name, app_title, attitude_counter ("Attitude %1$d of %2$d"), default_reflection, btn_new_reflection, btn_start_timer.
- Timer: timer_title, timer_subtitle, timer_session_guided, timer_status_completed, timer_status_running, timer_status_paused.
- Configurações: settings_title, settings_section_reminders, settings_daily_reminder, settings_meditate_reminder, settings_section_about, settings_version_info.
- Acessibilidade: cd_settings, cd_back, cd_reset, cd_play, cd_pause.
- As 9 Atitudes de Mindfulness de Jon Kabat-Zinn (attitude_1_name a attitude_9_name e attitude_1_desc a attitude_9_desc):
  1. Mente de Principiante (Beginner's Mind)
  2. Não-Julgamento (Non-Judging)
  3. Aceitação (Acceptance)
  4. Desapego (Letting Go)
  5. Confiança (Trust)
  6. Não-Esforço (Non-Striving)
  7. Paciência (Patience)
  8. Gratidão (Gratitude)
  9. Generosidade (Generosity)
```

---

## 🧠 3.4. Regra das 9 Atitudes e Estado da UI (`AttitudeRepository` e `MindfulnessViewModel`)

No Módulo 2 geramos `AttitudeRepository.kt` e `MindfulnessViewModel.kt` como esqueletos (*stubs*). Agora vamos implementar a lógica real.

### 🔍 Código-Chave em Foco: Fórmula de Rotação Cíclica
O coração do domínio do **MindfulDays** é o modelo `MindfulnessAttitude` e a função determinística `getTodayAttitude`, que rotaciona as 9 atitudes conforme o dia do ano usando a operação módulo (`.mod(9)`):

```kotlin
// data/model/MindfulnessAttitude.kt
data class MindfulnessAttitude(
    val id: Int,
    val name: String = "",
    val description: String = "",
    @get:StringRes val nameRes: Int = 0,
    @get:StringRes val descriptionRes: Int = 0
)

// Lógica central em data/repository/AttitudeRepository.kt
fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude {
    val index = (dayOfYear - 1).mod(attitudes.size)
    return attitudes[index]
}
```

> [!TIP]
> **Por que passar `dayOfYear` como parâmetro com valor padrão?**
> Isso permite que em produção ele use automaticamente o dia atual do calendário, enquanto nos **Testes Unitários (Módulo 4)** podemos injetar qualquer dia (dia 1, dia 9, dia 10, dia 365) para validar a rotação sem depender do relógio do sistema.

### 🤖 Prompt para Implementar `AttitudeRepository.kt` e `MindfulnessViewModel.kt`
Em vez de digitar manualmente a lista das 9 atitudes e o `StateFlow` do ViewModel, peça ao Gemini:

```text
Seguindo @AGENTS.md, complete a implementação destas duas classes substituindo os TODOs:

1. Em `dev/mindfuldays/app/data/repository/AttitudeRepository.kt`:
   - Defina a propriedade pública `val attitudes = listOf(...)` com as 9 Atitudes de Mindfulness de Jon Kabat-Zinn (IDs de 1 a 9), incluindo seus textos padrão (`name`, `description`) e suas referências `@StringRes` (`R.string.attitude_1_name`, `R.string.attitude_1_desc`, etc.).
   - Implemente `fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude` usando `val index = (dayOfYear - 1).mod(attitudes.size)`.

2. Em `dev/mindfuldays/app/ui/viewmodel/MindfulnessViewModel.kt`:
   - Mantenha `data class MindfulnessUiState(val attitude: MindfulnessAttitude, val aiReflection: String = "", val isLoadingAi: Boolean = false)`.
   - Em `MindfulnessViewModel(private val repository: AttitudeRepository = AttitudeRepository(), private val geminiService: GeminiApiService = GeminiApiService())`, exponha `val uiState: StateFlow<MindfulnessUiState>` inicializado com `repository.getTodayAttitude()`.
   - Implemente `fun generateAiReflection(attitudeTitle: String? = null, languageCode: String = Locale.getDefault().language)` atualizando `isLoadingAi = true`, chamando `geminiService.generateReflection(title, languageCode)` e atualizando `aiReflection` e `isLoadingAi = false`.
```

---

## 🤖 3.5. Integração com Gemini API via Retrofit e Moshi (`GeminiApiService.kt`)

Agora vamos conectar nosso aplicativo ao modelo **`gemini-3.8-flash`** utilizando Retrofit e Moshi.

> [!IMPORTANT]
> **Dois Pontos Críticos em Produção:**
> 1. **Modelo (`gemini-3.8-flash`)**: Modelos anteriores como `gemini-1.5-flash` ou `gemini-2.5-flash` retornam HTTP 404 para novas chaves no `v1beta`. Use sempre o **`gemini-3.8-flash`**.
> 2. **Serialização com Moshi em Kotlin**: Anote os DTOs com `@JsonClass(generateAdapter = true)` e registre `KotlinJsonAdapterFactory()` no builder do Moshi para evitar falhas silenciosas de reflexão em tempo de execução.

### 🔍 Código-Chave em Foco: Contrato Retrofit e Configuração Moshi
Estes são os dois blocos essenciais que estruturam a chamada à API:

```kotlin
// 1. DTOs e Endpoint oficial em data/remote/GeminiApiService.kt
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

// 2. Builder do Moshi + Retrofit
val moshi = Moshi.Builder()
    .addLast(KotlinJsonAdapterFactory())
    .build()
```

### 🤖 Prompt para Gerar o `GeminiApiService.kt` Completo
Use este prompt no assistente de IA para gerar toda a classe `GeminiApiService.kt` com suporte multilíngue e fallback offline:

```text
Seguindo @AGENTS.md, implemente a classe completa `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:
1. Inclua os DTOs (`GeminiRequest`, `Content`, `Part`, `GeminiResponse`, `Candidate`, `ContentResponse`, `PartResponse`) anotados com `@JsonClass(generateAdapter = true)` e a interface `GeminiApi` com `@POST("v1beta/models/gemini-3.8-flash:generateContent")`.
2. Configure `OkHttpClient` com `HttpLoggingInterceptor(Level.BODY)`, `Moshi` com `KotlinJsonAdapterFactory()` e `Retrofit` apontando para `"https://generativelanguage.googleapis.com/"`.
3. Implemente `suspend fun generateReflection(attitudeTitle: String, languageCode: String = Locale.getDefault().language): String` executando em `Dispatchers.IO`:
   - Leia `BuildConfig.GEMINI_API_KEY`. Se estiver vazia (`isBlank()`), retorne imediatamente uma mensagem amigável de fallback offline conforme `languageCode` ("pt", "en", "es").
   - Construa um prompt sereno de mindfulness pedindo uma reflexão inspiradora de no máximo 2 frases em texto simples sobre `attitudeTitle`, estritamente no idioma `languageCode`.
   - Capture qualquer exceção de rede (relançando `CancellationException`), registre o erro com `Log.e` e retorne o fallback offline sem quebrar o app.
```

---

## 🎨 3.6. Tema Dual (Light/Dark Mode) e `HomeScreen.kt` Desacoplada

No Módulo 2 já geramos `Color.kt`, `Theme.kt` e `HomeScreen.kt`. Antes de avançar para os testes automatizados do Módulo 4, vamos revisar dois conceitos-chave de UI no Jetpack Compose.

> [!CAUTION]
> **O Perigo do Hardcode de Cores em Composables:**
> Se você definir cores fixas como `Color(0xFFFFFFFF)` diretamente em um Composable, no **Dark Mode** o texto (`onSurface`, off-white claro) ficará invisível sobre o fundo branco. Use sempre tokens semânticos: `MaterialTheme.colorScheme.background`, `surface`, `onSurface`, `onSurfaceVariant`, `primary` e `outlineVariant`.

### 🔍 Código-Chave em Foco: Separação de Estado (`HomeScreen` vs `HomeScreenContent`)
Para que nossos testes de UI com **Robot Pattern** (Módulo 4) sejam rápidos e determinísticos, separamos `HomeScreen` em uma função com estado (conectada ao ViewModel) e uma função *stateless* (`HomeScreenContent`) que recebe apenas dados primitivos e lambdas:

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

### 🤖 Prompt de Auditoria para `Theme.kt` e `HomeScreen.kt`
Se quiser verificar ou ajustar seu tema e tela principal gerados no Módulo 2, execute este prompt:

```text
Revise `Color.kt`, `Theme.kt` e `HomeScreen.kt` contra as regras de @AGENTS.md:
1. Verifique se `Theme.kt` define corretamente `LightColorScheme` e `DarkColorScheme` usando a paleta oficial do MindfulDays e `dynamicColor: Boolean = false` por padrão.
2. Verifique se `HomeScreen.kt` NÃO possui nenhum `Color(0xFF...)` nem textos hardcoded: todas as cores devem usar `MaterialTheme.colorScheme.*` e todos os textos devem usar `stringResource(R.string.*)`.
3. Certifique-se de que `HomeScreen.kt` exponha o composable stateless `HomeScreenContent(attitude: MindfulnessAttitude, aiReflection: String, isLoadingAi: Boolean, onGenerateAiReflection: () -> Unit, onNavigateToSettings: () -> Unit, onNavigateToTimer: () -> Unit, modifier: Modifier = Modifier)` para nossos testes de UI.
```

---

### ✅ Verificação Rápida do Módulo 3
No terminal do Android Studio, verifique se tudo compila corretamente antes de iniciar os testes:

```bash
./gradlew assembleDebug
```

Com o contexto no `AGENTS.md`, a lógica das 9 atitudes e a integração com a Gemini API prontas em uma fração do tempo, avançamos para o **Módulo 4: Qualidade de Software, Testes Automatizados com IA e Robot Pattern**.
