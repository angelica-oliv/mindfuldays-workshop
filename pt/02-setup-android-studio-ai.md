# 🛠️ Módulo 2 — Setup do Projeto no Android Studio (Versão Stable) com IA

Neste segundo módulo, vamos configurar o projeto do aplicativo **MindfulDays** utilizando a versão **Stable do Android Studio**. Utilizaremos a integração nativa com o **Gemini no Android Studio** para acelerar a criação da estrutura do app a partir dos protótipos que geramos no Stitch.

---

## 💻 2.1. Configuração do Ambiente no Android Studio Stable

1. Certifique-se de que está utilizando a versão **Stable** mais recente do Android Studio.
2. Abra o Android Studio e acesse **Settings/Preferences → Tools → AI Assistant (Gemini)**.
3. Faça login com sua conta Google e certifique-se de que o assistente **Gemini** está ativado.
4. Para utilizar o gerador de projetos **Create with AI** ou o painel de assistente do Gemini:
   * Acesse **New Project** na tela inicial do Android Studio.
   * Selecione o template **Empty Activity** (ou selecione a opção **Create with AI...** se disponível na barra lateral de templates).

---

## 📦 2.2. Definindo o Nome do Pacote e Estrutura

Ao criar o projeto, preencha os parâmetros fundamentais:

* **Name**: `MindfulDays`
* **Package Name**: `dev.mindfuldays.app` (Padrão profissional e recomendado para projetos open-source / dev).
* **Language**: Kotlin
* **Minimum SDK**: API 24 (Android 7.0 Nougat ou superior)
* **Build Configuration Language**: Kotlin DSL (`build.gradle.kts`)

---

## 🤖 2.3. Prompt Multimodal para o Gemini no Android Studio

Abra o painel do **Gemini** no Android Studio (**View → Tool Windows → Gemini**) ou utilize a janela **Create with AI**. Anexe as capturas de tela geradas no **Stitch** e cole o seguinte prompt estruturado e prescritivo:

> [!TIP]
> **Por que um prompt prescritivo e com classes em esqueleto?** Ao guiar a IA especificando os componentes nativos exatos do Material 3, a tipografia padrão do sistema e as 3 telas sem elementos supérfluos, o código gerado no Android Studio terá fidelidade visual idêntica ao design do Stitch. Além disso, ao instruir a IA a gerar classes como `GeminiApiService` e `AttitudeRepository` como esqueletos em branco (*stubs* com TODOs), garantimos que o projeto compile imediatamente com telas funcionais, reservando a lógica de negócio e integração da API Gemini para serem construídas passo a passo pelos alunos nos módulos seguintes. A chave da API do Gemini nunca deve ser exposta na interface do usuário (UI), sendo lida com segurança via `local.properties` e `BuildConfig`.

```text
You are an expert Android developer. Create a minimalist Android application named 'MindfulDays' with package name 'dev.mindfuldays.app' using Jetpack Compose and Material Design 3.

Use the attached Stitch UI screenshots as the exact visual reference and follow these prescriptive rules:
- UI STYLE & TYPOGRAPHY: Strict minimalist design for a workshop tutorial. Use Android system fonts ONLY (default sans-serif / Roboto). Use native Android Material 3 components ONLY (Button, OutlinedButton, FilledIconButton, OutlinedIconButton, ElevatedCard, Card, TopAppBar, Switch, HorizontalDivider). Do NOT create complex custom UI components.
- COLOR PALETTE:
  * Primary: Sage Green (#6B8E23)
  * Secondary / Divider: Muted Sand (#E8DFD8)
  * Background: Warm Off-White (#FBF9F5)
  * Surface / Cards: Pure White (#FFFFFF)
  * OnBackground / Text: Dark Forest Green (#2C3E35)

IMPLEMENT EXACTLY THESE 3 SCREENS (no more, no less):

1. Screen 1: Home Screen (HomeScreen.kt)
   - Layout: Column with background #FBF9F5, vertical arrangement spaced between.
   - Header (Top):
     * A top Row containing:
       - Centered column: App title "MINDFULDAYS" (MaterialTheme.typography.labelLarge, primary color) and subtitle "Atitude X de 9" (bodyMedium, muted).
       - Top-right corner: Standard IconButton with Icons.Default.Settings to navigate to SettingsScreen.
   - Central Card (ElevatedCard):
     * Container color white, elevation 4.dp, padded content.
     * Attitude title in bold (headlineMedium, e.g., "Aceitação").
     * Attitude description (bodyLarge, e.g., "Reconheça e acolha o momento presente exatamente como ele é.").
     * Thin HorizontalDivider (color #E8DFD8).
     * AI reflection text block (bodyMedium, italic, displaying generated reflection or default).
     * Primary filled Button with sparkle icon: "✨ Nova Reflexão (Gemini IA)". Shows CircularProgressIndicator when loading.
   - Bottom Action:
     * A single full-width OutlinedButton: "⏱️ Iniciar Timer de Meditação" navigating to TimerScreen.
   - STRICT EXCLUSIONS: Do NOT include bottom navigation bars, profile avatars, greetings, photo banners, audio players, or habit/streak charts.

2. Screen 2: Meditation Timer Screen (TimerScreen.kt)
   - TopAppBar: Title "Timer de Meditação" with back navigation arrow (Icons.AutoMirrored.Filled.ArrowBack).
   - Center Area:
     * Subtitle text: "Concentre-se na respiração" (bodyLarge, muted color).
     * Minimalist circular countdown timer: A clean circular progress ring (Canvas drawArc with stroke width 8.dp: track color #E8DFD8, progress color #6B8E23), large digital countdown text centered inside ("10:00" or mm:ss in headlineLarge/displayMedium), and status text below ("Pausado" / "Em andamento" / "Concluído").
   - Bottom Controls:
     * A centered horizontal Row with exactly two buttons:
       - Reset button: OutlinedIconButton with Icons.Default.Refresh.
       - Play/Pause button: Large FilledIconButton with primary container color and Play/Pause icon.
   - STRICT EXCLUSIONS: Do NOT include multiple timer dials, duration selector chips/pills, background nature sounds, audio pickers, or interval chime settings.

3. Screen 3: Settings Screen (SettingsScreen.kt)
   - TopAppBar: Title "Configurações" with back navigation arrow (Icons.AutoMirrored.Filled.ArrowBack).
   - Section "Lembretes Diários" (titleMedium, primary color):
     * Card (containerColor surface, elevation 2.dp) containing:
       - Row: Text "Lembrete da Atitude Diária" + standard Material 3 Switch (checked by default).
       - Thin HorizontalDivider.
       - Row: Text "Lembrete para Meditar" + standard Material 3 Switch (unchecked by default).
   - Section "Sobre o App" (titleMedium, primary color):
     * Card (containerColor surface, elevation 2.dp) containing:
       - Text "MindfulDays" (titleMedium bold).
       - Text "Versão 1.0 • 9 Atitudes de Jon Kabat-Zinn" (bodyMedium, muted).
   - STRICT EXCLUSIONS: Absolutely NO Gemini API key input field in the UI! (The API key is securely provided via local.properties and BuildConfig.GEMINI_API_KEY in code, never typed by the user in UI). Do NOT include time picker wheel dialogs, sound options, or nested accordions.

EXPECTED FINAL PACKAGE STRUCTURE:
Organize all generated code cleanly under the root package 'dev.mindfuldays.app':
dev.mindfuldays.app/
├── data/
│   ├── model/
│   │   └── MindfulnessAttitude.kt
│   ├── remote/
│   │   └── GeminiApiService.kt
│   └── repository/
│       └── AttitudeRepository.kt
├── ui/
│   ├── home/
│   │   └── HomeScreen.kt
│   ├── timer/
│   │   └── TimerScreen.kt
│   ├── settings/
│   │   └── SettingsScreen.kt
│   ├── theme/
│   │   ├── Color.kt
│   │   ├── Theme.kt
│   │   └── Type.kt
│   └── viewmodel/
│       └── MindfulnessViewModel.kt
└── MainActivity.kt

INITIAL IMPLEMENTATION STATUS (WORKSHOP PROGRESSION & BLANK SKELETON CLASSES):
Since this project will be built progressively across workshop modules, generate classes with the following implementation levels:

1. FULLY IMPLEMENTED NOW (UI & Design Tokens):
   - ui/theme/ (Color.kt, Theme.kt, Type.kt): Fully implemented with the required Material 3 color tokens and system fonts.
   - ui/home/HomeScreen.kt, ui/timer/TimerScreen.kt, ui/settings/SettingsScreen.kt: Fully implement the declarative Composable layouts according to the exact screen specifications above.
   - data/model/MindfulnessAttitude.kt: Data class fully defined:
     data class MindfulnessAttitude(val id: Int, val name: String, val description: String, val dailyReflection: String)
   - MainActivity.kt: Simple state-based navigation switching between HomeScreen, TimerScreen, and SettingsScreen.

2. GENERATE AS EMPTY SKELETONS / STUBS (TO BE FILLED IN SUBSEQUENT WORKSHOP STEPS):
   - data/remote/GeminiApiService.kt: Generate as a BLANK/EMPTY interface skeleton with a simple stub and a TODO comment (do NOT implement API calls yet, students will implement this in Module 3):
     // TODO: Implement Google Gemini API call with generativeai SDK in Module 3
     interface GeminiApiService {
         suspend fun generateDailyReflection(attitude: String): String = ""
     }
   - data/repository/AttitudeRepository.kt: Generate as a SKELETON class stub with placeholder method signatures and a TODO comment:
     // TODO: Implement 9 Jon Kabat-Zinn attitudes & offline fallback logic in Module 3
     class AttitudeRepository(private val apiService: GeminiApiService? = null) {
         fun getAttitudeOfTheDay(): MindfulnessAttitude = MindfulnessAttitude(1, "Aceitação", "Reconheça e acolha o momento presente.", "Reflexão inicial.")
         suspend fun getAiReflection(attitude: String): String = "Reflexão temporária de exemplo."
     }
   - ui/viewmodel/MindfulnessViewModel.kt: Generate as an INITIAL SKELETON ViewModel with basic StateFlow and placeholder state values just enough to preview and run the UI without crashing:
     // TODO: Bind coroutines, offline caching and real Gemini API integration in Module 3

Write clean, concise, idiomatic Kotlin and Jetpack Compose code with no unnecessary dependencies.
```

---

## 📁 2.4. Visão da Estrutura de Pacotes do Projeto

Após a execução do prompt e geração inicial, seu projeto em `dev.mindfuldays.app` estará organizado da seguinte forma:

```text
dev.mindfuldays.app/
├── data/
│   ├── model/
│   │   └── MindfulnessAttitude.kt    <- Data class com os atributos da atitude
│   ├── remote/
│   │   └── GeminiApiService.kt       <- Esqueleto / Stub vazio (implementado no Módulo 3)
│   └── repository/
│       └── AttitudeRepository.kt     <- Esqueleto com assinaturas (implementado no Módulo 3)
├── ui/
│   ├── home/
│   │   └── HomeScreen.kt             <- Layout Compose completo e funcional
│   ├── timer/
│   │   └── TimerScreen.kt            <- Layout Compose completo e funcional
│   ├── settings/
│   │   └── SettingsScreen.kt         <- Layout Compose completo e funcional
│   ├── theme/
│   │   ├── Color.kt                  <- Tokens Material 3 oficiais (Sálvia, Areia, Off-White)
│   │   ├── Theme.kt
│   │   └── Type.kt
│   └── viewmodel/
│       └── MindfulnessViewModel.kt   <- Esqueleto inicial de estado para a UI
└── MainActivity.kt                   <- Ponto de entrada e navegação básica entre as telas
```

Com a estrutura do projeto sincronizada e compilando no **Android Studio Stable**, avançamos para o **Módulo 3: Diretrizes com AGENTS.md, Implementação da UI em Compose e Integração com Gemini API**.
