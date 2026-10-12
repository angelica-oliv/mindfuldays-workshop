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
   - Utilizar o endpoint do modelo `gemini-3.8-flash:generateContent`.
   - Gerar reflexões concisas e inspiradoras com no máximo 2 frases para cada atitude.
   - Tratar ausência de chave de API e erros de rede com fallback amigável offline sem quebrar o app.

## 🛠️ Comandos de Verificação e Validação
Sempre verifique as alterações utilizando os seguintes comandos no terminal:
- **Compilação do app**: `./gradlew assembleDebug`
- **Testes Unitários**: `./gradlew testDebugUnitTest`
- **Linter & Análise Estática**: `./gradlew lintDebug`

## 🚫 Restrições Rígidas (Guardrails)
- **NUNCA** faça hardcode de credenciais ou chaves de API (`apiKey`) no código versionado. A chave deve ser configurada em `local.properties` e consumida via `BuildConfig.GEMINI_API_KEY`.
- **NÃO** misture lógica de negócios ou chamadas assíncronas de rede diretamente dentro de funções `@Composable`.
- Mantenha funções Composable limpas e desacopladas, utilizando parâmetros para eventos e lambdas (`onAction: () -> Unit`) para facilitar testes de UI.
- Use nomes descritivos em português para textos de interface visível e inglês para código técnico, métodos e classes.
```

Com o `AGENTS.md` configurado na raiz do projeto, qualquer agente (como o Gemini no Android Studio) passará a produzir código alinhado com o seu design system e suas regras de negócio.

---

## 🔑 3.2. Configuração da Gemini API e Gerenciamento Seguro de Credenciais

Para integrar a **Gemini API** ao aplicativo de forma robusta, moderna e direta, utilizamos chamadas REST com **Retrofit**, **Moshi** e **OkHttp** conectando ao endpoint oficial do modelo **`gemini-3.8-flash`**.

Abaixo estão os passos essenciais e boas práticas para evitar erros comuns de permissão, ativação e segurança:

### 1. Obtenção da API Key no Google AI Studio
1. Acesse o [Google AI Studio](https://aistudio.google.com/) e faça login com sua conta Google.
2. Clique em **Get API key** (Obter chave de API) e crie uma nova chave em um projeto novo ou existente.
3. Copie a chave gerada.

> [!WARNING]
> **Armadilha Comum — Chaves do Firebase (`API_KEY_SERVICE_BLOCKED` 403):**
> Nunca utilize chaves de API geradas automaticamente pelo Firebase com restrições para apps Android para chamar o endpoint da Gemini API. Essas chaves possuem restrições de escopo e geram o erro:
> `403 PERMISSION_DENIED: Requests to this API generativelanguage.googleapis.com method ... are blocked (API_KEY_SERVICE_BLOCKED)`.
> Utilize sempre uma chave gerada diretamente no **Google AI Studio** ou no Google Cloud com a API habilitada.

### 2. Ativação da Generative Language API no Google Cloud
Mesmo com uma chave válida gerada, se o projeto do Google Cloud associado à sua chave ainda não tiver a API habilitada, as chamadas serão recusadas com o erro:
`403 FORBIDDEN: Generative Language API has not been used in project ... or it is disabled (SERVICE_DISABLED)`.

Para ativar:
1. Acesse o console do Google Cloud no link fornecido pelo próprio erro ou em:
   `https://console.developers.google.com/apis/api/generativelanguage.googleapis.com/overview?project=<SEU_PROJECT_ID>`
2. Clique no botão **Ativar** (Enable). A ativação leva apenas alguns segundos para propagar.

### 3. Armazenamento Seguro no `local.properties` (Guardrail de Segurança)
Seguindo as diretrizes de segurança do projeto (`AGENTS.md`), **NUNCA faça commit de chaves de API no Git** nem insira a chave hardcoded no código Kotlin.

Abra o arquivo `local.properties` na raiz do projeto (que já é ignorado pelo `.gitignore`) e adicione:

```properties
GEMINI_API_KEY=sua_chave_do_ai_studio_aqui
```

### 4. Injeção da Chave via `buildConfigField` no `app/build.gradle.kts`
Para que o código Kotlin tenha acesso seguro à chave durante a compilação, configuramos o Gradle para carregar o `local.properties` e gerar a constante em `BuildConfig`.

No arquivo `app/build.gradle.kts`:

```kotlin
import java.util.Properties

// Carrega as variáveis do local.properties
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
        // Injeta a chave de forma segura no BuildConfig
        buildConfigField("String", "GEMINI_API_KEY", "\"$geminiApiKey\"")
    }

    buildFeatures {
        compose = true
        buildConfig = true // Habilita a geração da classe BuildConfig
    }
}
```

### 5. Dependências do Gradle (Retrofit, Moshi e OkHttp)
Para realizar a comunicação HTTP assíncrona e a serialização JSON de forma performática, adicione as dependências no seu projeto:

No arquivo `gradle/libs.versions.toml`:
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

No arquivo `app/build.gradle.kts`:
```kotlin
plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.kotlin.compose)
    alias(libs.plugins.google.devtools.ksp)
}

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

---

## 🌐 3.3. Internacionalização (i18n): Suporte Multi-idioma (Inglês, Português e Espanhol)

Uma das melhores práticas essenciais de desenvolvimento Android é nunca deixar textos visíveis hardcoded em código Kotlin ou Composables. Além de facilitar testes e manutenção, isso permite que o aplicativo se adapte instantaneamente ao idioma configurado no dispositivo do usuário.

No Android, os recursos de texto residem dentro de `app/src/main/res/values`:
- `values/strings.xml`: Tabela padrão (fallback internacional em Inglês).
- `values-pt/strings.xml`: Tabela específica para Português.
- `values-es/strings.xml`: Tabela específica para Espanhol.

### 1. `app/src/main/res/values/strings.xml` (Padrão / Inglês)
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

### 2. `app/src/main/res/values-pt/strings.xml` (Português)
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

### 3. `app/src/main/res/values-es/strings.xml` (Espanhol)
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
    <string name="attitude_2_desc">Observa tus pensamientos y sentimientos sin etiquetarlos como buenos o malos.</string>
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

---

## 🧠 3.4. Repositório e Modelo das 9 Atitudes com Internacionalização

A data class `MindfulnessAttitude` em `dev/mindfuldays/app/data/model/MindfulnessAttitude.kt` encapsula os atributos essenciais de cada atitude, incluindo anotações `@StringRes` para referenciar os recursos de strings:

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

Agora, implemente a classe de repositório em `dev/mindfuldays/app/data/repository/AttitudeRepository.kt` mapeando cada atitude para seu respectivo recurso de texto:

```kotlin
package dev.mindfuldays.app.data.repository

import dev.mindfuldays.app.R
import dev.mindfuldays.app.data.model.MindfulnessAttitude
import java.util.Calendar

class AttitudeRepository {

    val attitudes = listOf(
        MindfulnessAttitude(1, "Mente de Principiante", "Olhe para as coisas como se fosse a primeira vez, livre de expectativas.", R.string.attitude_1_name, R.string.attitude_1_desc),
        MindfulnessAttitude(2, "Não-Julgamento", "Observe seus pensamentos e sentimentos sem rotulá-los como bons ou ruins.", R.string.attitude_2_name, R.string.attitude_2_desc),
        MindfulnessAttitude(3, "Aceitação", "Reconheça e acolha o momento presente exatamente como ele é.", R.string.attitude_3_name, R.string.attitude_3_desc),
        MindfulnessAttitude(4, "Desapego", "Deixe ir pensamentos e desejos que tentam prender sua atenção.", R.string.attitude_4_name, R.string.attitude_4_desc),
        MindfulnessAttitude(5, "Confiança", "Desenvolva uma crença básica em si mesmo e nos seus sinais corporais.", R.string.attitude_5_name, R.string.attitude_5_desc),
        MindfulnessAttitude(6, "Não-Esforço", "Abandone a necessidade constante de alcançar um resultado imediato.", R.string.attitude_6_name, R.string.attitude_6_desc),
        MindfulnessAttitude(7, "Paciência", "Compreenda que certas coisas precisam de tempo para se desenvolver.", R.string.attitude_7_name, R.string.attitude_7_desc),
        MindfulnessAttitude(8, "Gratidão", "Aprecie o momento presente e valorize o que você já possui.", R.string.attitude_8_name, R.string.attitude_8_desc),
        MindfulnessAttitude(9, "Generosidade", "Ofereça atenção, carinho e presença com o coração aberto.", R.string.attitude_9_name, R.string.attitude_9_desc)
    )

    fun getTodayAttitude(dayOfYear: Int = Calendar.getInstance().get(Calendar.DAY_OF_YEAR)): MindfulnessAttitude {
        val index = (dayOfYear - 1).mod(attitudes.size)
        return attitudes[index]
    }
}
```

---

## 🤖 3.4. Integração com Gemini API via Retrofit e Moshi (`GeminiApiService.kt`)

Agora vamos implementar o serviço de rede e o ViewModel para conectar a interface com a **Gemini API**.

> [!IMPORTANT]
> **Atenção ao Modelo (`gemini-3.8-flash`):**
> Modelos anteriores como `gemini-1.5-flash` ou `gemini-2.5-flash` foram descontinuados para novas chaves no endpoint `v1beta`, retornando erro HTTP 404 (`"This model is no longer available to new users"`).
> O modelo atualizado e recomendado para respostas ágeis de texto é o **`gemini-3.8-flash`**.
>
> **Atenção à Serialização com Moshi em Kotlin:**
> Ao utilizar Moshi no Android, anote todas as classes de transferência de dados com `@JsonClass(generateAdapter = true)` e configure `KotlinJsonAdapterFactory()` no builder do Moshi. Sem isso, o Moshi tentará utilizar reflexão padrão do Java, gerando uma exceção de serialização silenciosa em tempo de execução.

Crie o arquivo em `dev/mindfuldays/app/data/remote/GeminiApiService.kt`:

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

// Data Transfer Objects (DTOs) com adapters gerados pelo Moshi
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

// Interface Retrofit com o endpoint oficial do gemini-3.8-flash
interface GeminiApi {
    @POST("v1beta/models/gemini-3.8-flash:generateContent")
    suspend fun generateContent(
        @Query("key") apiKey: String,
        @Body request: GeminiRequest
    ): GeminiResponse
}

class GeminiApiService {

    private val api: GeminiApi by lazy {
        // Interceptor de log para depuração no Logcat durante o desenvolvimento
        val logging = HttpLoggingInterceptor().apply {
            level = HttpLoggingInterceptor.Level.BODY
        }
        val client = OkHttpClient.Builder()
            .addInterceptor(logging)
            .build()

        // Configuração do Moshi com suporte completo a classes Kotlin
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
     * Gera uma reflexão diária personalizada para a atitude informada usando o modelo gemini-3.8-flash,
     * adaptando o idioma do prompt e resposta para o idioma do usuário (pt, en, es).
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
            android.util.Log.e("GeminiApiService", "Erro ao gerar reflexão via Retrofit", e)
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

## 📱 3.6. Implementando a Home Screen em Jetpack Compose com Strings Internacionalizadas

Crie o arquivo em `dev/mindfuldays/app/ui/home/HomeScreen.kt` utilizando `stringResource(...)` para todas as labels e textos:

```kotlin
package dev.mindfuldays.app.ui.home

import androidx.compose.foundation.background
import androidx.compose.foundation.layout.*
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.AutoAwesome
import androidx.compose.material.icons.filled.Settings
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
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
            .background(Color(0xFFFBF9F5))
            .statusBarsPadding()
            .navigationBarsPadding()
            .padding(24.dp),
        verticalArrangement = Arrangement.SpaceBetween,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        // Header (Top Bar)
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
                    color = Color(0xFF6B8E23),
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
                    contentDescription = stringResource(R.string.cd_settings)
                )
            }
        }

        // Card Central (ElevatedCard)
        ElevatedCard(
            modifier = Modifier
                .fillMaxWidth()
                .padding(vertical = 16.dp),
            colors = CardDefaults.elevatedCardColors(
                containerColor = Color(0xFFFFFFFF)
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
                    color = Color(0xFFE8DFD8),
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

        // Ação de Navegação para o Timer
        OutlinedButton(
            onClick = onNavigateToTimer,
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

Com as telas internacionalizadas e a comunicação multilíngue com a Gemini API prontas, avançamos para o **Módulo 4: Qualidade de Software, Testes Automatizados com IA e Robot Pattern**.
