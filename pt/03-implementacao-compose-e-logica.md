# 🧩 Módulo 3 — AGENTS.md, Regra das 9 Atitudes, Gemini API e UI em Compose

Neste módulo, vamos estruturar o arquivo **`AGENTS.md`** como contexto operacional e utilizar **um único prompt unificado** para que o Gemini no Android Studio configure as credenciais no Gradle, implemente a regra das 9 atitudes, conecte a **Gemini API** com Retrofit/Moshi e prepare a UI para o workshop.

---

## 🤖 3.1. Diretrizes para Agentes de IA: Criando o Arquivo `AGENTS.md`

Antes de solicitar qualquer alteração à IA, configuramos o nosso recurso mais estratégico: o arquivo **`AGENTS.md`**.

### 🌟 Por que o `AGENTS.md` é tão importante?

Assim como o `README.md` orienta pessoas desenvolvedoras, o **`AGENTS.md`** atua como a **fonte única de verdade operacional para agentes e assistentes de código com IA** (Gemini no Android Studio, Cursor, Claude Code, GitHub Copilot e Antigravity):

1. **Grounding e Redução de Alucinações**: Ancora a IA nas decisões técnicas já tomadas.
2. **Consistência de Stack e Arquitetura**: Garante o respeito estrito a **MVVM**, **Clean Architecture**, **Kotlin idiomático** e **Jetpack Compose com Material Design 3**.
3. **Fidelidade aos Design Tokens e Regras de Negócio**: Mantém presente a paleta oficial do Stitch e a rotação cíclica das 9 atitudes de Jon Kabat-Zinn.
4. **Guardrails de Segurança**: Proíbe explicitamente chaves secretas (`apiKey`) hardcoded ou cores hexadecimais fixas em Composables.
5. **Máxima Velocidade em Apresentações e Workshops**: Com o `AGENTS.md` na raiz, um **único prompt** é suficiente para implementar toda a lógica de negócio e rede.

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
- **UI Toolkit**: Jetpack Compose com Material Design 3 (M3). **Prohibido o uso de layouts XML tradicionais**.
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
   - Utilizar o endpoint do modelo `gemini-3.5-flash:generateContent` (ou `gemini-3.5-flash-lite:generateContent`).
   - Configurar OkHttpClient com timeouts adequados para LLM (`connectTimeout`: 30s, `readTimeout`: 60s, `writeTimeout`: 30s). Não fixar `callTimeout` agressivos nem `pingInterval` para evitar erros de SocketTimeoutException.
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

## 🔑 3.2. Chave de API no `local.properties` (Passo Manual Rápido)

1. Obtenha sua API Key gratuita no [Google AI Studio](https://aistudio.google.com/) (**Get API key**).
2. Abra o arquivo `local.properties` na raiz do seu projeto (ignorado pelo Git) e adicione a chave:

```properties
GEMINI_API_KEY=sua_chave_do_ai_studio_aqui
```

> [!WARNING]
> **Importante:** Utilize uma chave gerada no Google AI Studio (ou Google Cloud com a Generative Language API ativada). Não utilize chaves do Firebase com restrições para apps, pois geram o erro `403 (API_KEY_SERVICE_BLOCKED)`.

---

## 🔍 3.3. Conceitos-Chave de Arquitetura (O que a IA construirá)

Para entender o que a IA implementará no prompt unificado:

1. **Gradle & Injeção Segura**: O `app/build.gradle.kts` lê o `local.properties` e expõe `BuildConfig.GEMINI_API_KEY`, adicionando Retrofit, Moshi e OkHttp.
2. **Internacionalização (i18n)**: Geração sincronizada de `values/strings.xml`, `values-pt/strings.xml` e `values-es/strings.xml` com as 9 atitudes de Jon Kabat-Zinn.
3. **Fórmula de Rotação Cíclica**:
   ```kotlin
   fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude {
       val index = (dayOfYear - 1).mod(attitudes.size)
       return attitudes[index]
   }
   ```
4. **Cliente Gemini API**: Chamada REST para `v1beta/models/gemini-3.5-flash:generateContent` com adaptadores Moshi em Kotlin e fallback amigável offline se não houver internet ou se a chave estiver ausente.

---

## ⚡ 3.4. Prompt Único e Completo para o Gemini no Android Studio (Tudo em Um)

Abra o painel do **Gemini** no Android Studio (**View → Tool Windows → Gemini**) e envie o seguinte **prompt unificado**. Ele executará todas as tarefas do Módulo 3 em uma única rodada:

```text
Atue como um Desenvolvedor Android Sênior e siga estritamente as diretrizes de @AGENTS.md.
Realize em um único passo todas as configurações e implementações pendentes do Módulo 3 para 'dev.mindfuldays.app':

1. CONFIGURAÇÃO DE GRADLE E SEGURANÇA:
   - Em `app/build.gradle.kts`:
     * Carregue `local.properties` via `java.util.Properties` e leia a propriedade `GEMINI_API_KEY` (fallback para "").
     * Em `defaultConfig`, adicione: `buildConfigField("String", "GEMINI_API_KEY", "\"$geminiApiKey\"")`.
     * Em `buildFeatures`, garanta `compose = true` e `buildConfig = true`.
   - Em `gradle/libs.versions.toml` e `app/build.gradle.kts`, garanta as dependências para:
     * Retrofit (`retrofit`, `converter-moshi`)
     * Moshi (`moshi-kotlin`, KSP `moshi-kotlin-codegen`)
     * OkHttp (`okhttp`, `logging-interceptor`)

2. RECURSOS DE STRINGS E INTERNACIONALIZAÇÃO (i18n):
   - Crie/atualize de forma consistente:
     * `app/src/main/res/values/strings.xml` (Inglês padrão)
     * `app/src/main/res/values-pt/strings.xml` (Português)
     * `app/src/main/res/values-es/strings.xml` (Espanhol)
   - Inclua as chaves: `app_name`, `app_title`, `attitude_counter` ("Attitude %1$d of %2$d"), `default_reflection`, `btn_new_reflection`, `btn_start_timer`, `timer_title`, `timer_subtitle`, `timer_session_guided`, `timer_status_completed`, `timer_status_running`, `timer_status_paused`, `settings_title`, `settings_section_reminders`, `settings_daily_reminder`, `settings_meditate_reminder`, `settings_section_about`, `settings_version_info`, content descriptions (`cd_settings`, `cd_back`, `cd_reset`, `cd_play`, `cd_pause`), e as 9 Atitudes de Mindfulness de Jon Kabat-Zinn (`attitude_1_name` a `attitude_9_name` e `attitude_1_desc` a `attitude_9_desc`).

3. LÓGICA DE NEGÓCIO E REPOSITÓRIO (AttitudeRepository.kt):
   - Em `dev/mindfuldays/app/data/repository/AttitudeRepository.kt`:
     * Implemente a lista imutável pública `val attitudes = listOf(...)` com as 9 atitudes (IDs de 1 a 9), com seus nomes, descrições e referências a recursos `@StringRes` (`nameRes`, `descriptionRes`).
     * Implemente `fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude` usando a fórmula `(dayOfYear - 1).mod(attitudes.size)`.

4. INTEGRAÇÃO COM GEMINI API (GeminiApiService.kt):
   - Em `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:
     * Defina os DTOs com `@JsonClass(generateAdapter = true)`: `GeminiRequest`, `Content`, `Part`, `GeminiResponse`, `Candidate`, `ContentResponse`, `PartResponse`.
     * Interface Retrofit `GeminiApi` com `@POST("v1beta/models/gemini-3.5-flash:generateContent")` (IMPORTANTE: use EXCLUSIVAMENTE 'gemini-3.5-flash' ou 'gemini-3.5-flash-lite'; NÃO use 'gemini-2.5-flash' que dá 404 nem 'gemini-3.8-flash' que congela) recebendo `@Query("key") apiKey: String` e `@Body request: GeminiRequest`.
     * Configure `OkHttpClient.Builder()` otimizado para LLMs com timeouts adequados:
       - `.connectTimeout(30, TimeUnit.SECONDS)`
       - `.readTimeout(60, TimeUnit.SECONDS)`
       - `.writeTimeout(30, TimeUnit.SECONDS)`
       - `.retryOnConnectionFailure(true)`
       - `.addInterceptor(HttpLoggingInterceptor().apply { level = HttpLoggingInterceptor.Level.BODY })`
       - REGRA CRÍTICA DE TIMEOUT: NÃO use `callTimeout(20s)` nem `pingInterval` (provocam cancelamentos prematuros e SocketTimeoutException durante a inferência do Gemini).
     * Configure `Moshi.Builder().addLast(KotlinJsonAdapterFactory()).build()` e o cliente Retrofit com este `OkHttpClient`.
     * Implemente `suspend fun generateReflection(attitudeTitle: String, languageCode: String = Locale.getDefault().language): String` em `Dispatchers.IO`:
       - Leia `BuildConfig.GEMINI_API_KEY`. Se estiver vazia (`isBlank()`), retorne uma mensagem amigável offline no idioma do usuário.
       - Construa o prompt solicitando uma reflexão serena de mindfulness de no máximo 2 frases em texto simples no idioma correspondente (`languageCode`).
       - Em caso de exceção de rede ou timeout (relançando `CancellationException`), registre o erro e retorne o fallback offline sem quebrar o app.

5. VIEWMODEL E ESTADO DE UI (MindfulnessViewModel.kt):
   - Em `dev/mindfuldays/app/ui/viewmodel/MindfulnessViewModel.kt`:
     * Defina `MindfulnessUiState(val attitude: MindfulnessAttitude, val aiReflection: String = "", val isLoadingAi: Boolean = false)`.
     * Conecte `AttitudeRepository` e `GeminiApiService`.
     * Exponha `val uiState: StateFlow<MindfulnessUiState>` inicializado com `repository.getTodayAttitude()`.
     * Implemente `fun generateAiReflection(attitudeTitle: String? = null, languageCode: String = Locale.getDefault().language)` atualizando `isLoadingAi = true`, chamando `geminiService.generateReflection` e atualizando o estado.

6. DESIGN TOKENS E SISTEMA DE TEMA (Color.kt e Theme.kt):
   - Em `dev/mindfuldays/app/ui/theme/Color.kt`:
     * Codifique explicitamente as cores do design:
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
   - Em `dev/mindfuldays/app/ui/theme/Theme.kt`:
     * Desative a cor dinâmica do sistema operacional por padrão (`dynamicColor: Boolean = false`) para evitar que o papel de parede do dispositivo sobrescreva e altere a paleta do app.
     * Configure `LightColorScheme`:
       primary = SageGreen, primaryContainer = SoftSage, secondary = MutedSand,
       background = WarmOffWhite, surface = PureWhite, onPrimary = PureWhite,
       onBackground = DarkForestGreen, onSurface = DarkForestGreen,
       onSurfaceVariant = MutedForestGreen, outlineVariant = MutedSand
     * Configure `DarkColorScheme`:
       primary = LuminousSage, primaryContainer = DeepForestSurface, secondary = SoftMutedSage,
       background = DeepTranquilForest, surface = ElevatedForestSurface, onPrimary = DeepTranquilForest,
       onBackground = WarmOffWhiteText, onSurface = WarmOffWhiteText,
       onSurfaceVariant = SoftMutedSage, outlineVariant = ForestOutline
   - Audite `HomeScreen.kt`, `TimerScreen.kt`, `SettingsScreen.kt`: NUNCA use cores hexadecimais hardcoded, utilize sempre `MaterialTheme.colorScheme.*` e certifique-se de que todos os textos usem `stringResource(R.string.*)`. Além disso `HomeScreen` deve delegar para um composable stateless `HomeScreenContent` desacoplado para facilitar os testes.

Sincronize o projeto e verifique se './gradlew assembleDebug' compila com sucesso.
```

---

## ✅ 3.5. Verificação de Compilação

No terminal do Android Studio, execute:

```bash
./gradlew assembleDebug
```

Com este **único prompt**, completamos toda a integração de rede, persistência, i18n e estado de negócio em minutos. Avançamos para o **Módulo 4: Qualidade de Software, Testes Automatizados com IA e Robot Pattern**!
