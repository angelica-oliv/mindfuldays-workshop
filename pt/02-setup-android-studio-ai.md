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

FAST WORKSHOP EXECUTION RULES (CRITICAL FOR SPEED):
- PLANNER & TASKS: Execute this setup in at most 2 coding tasks (Task 1: Theme, strings.xml & skeleton stubs; Task 2: 3 Compose screens & MainActivity navigation). Do NOT create separate asset/polish tasks.
- NO ICON GENERATION: Do NOT invoke app_icon_agent and do NOT modify or generate custom launcher icons (ic_launcher* or custom vector drawables).
- NO EMULATOR / CRITIC LOOP: Do NOT deploy to an emulator or run critic_agent / automated adb UI inspection loops. Verify ONLY that './gradlew assembleDebug' compiles cleanly.
- MINIMAL DEPENDENCIES: Do NOT add unused libraries such as CameraX, Room, Play Services Location, Coil, or Accompanist.

Use the attached Stitch UI screenshots as the exact visual reference and follow these prescriptive rules:
- UI STYLE & TYPOGRAPHY: Strict minimalist design for a workshop tutorial. Use Android system fonts ONLY (default sans-serif / Roboto). Use native Android Material 3 components ONLY (Button, OutlinedButton, FilledIconButton, OutlinedIconButton, ElevatedCard, Card, TopAppBar, Switch, HorizontalDivider). Do NOT create complex custom UI components.
- INTERNATIONALIZATION (i18n): Never hardcode user-facing text strings in Composables. Load all labels, titles, descriptions, and button texts using stringResource(R.string...) from 'res/values/strings.xml' ONLY. Do NOT create 'values-pt' or 'values-es' directories in this step (multi-locale files will be added in Module 3; creating them now triggers blocking MissingTranslation lint loops).
- COLOR PALETTE & DUAL-THEME ADAPTATION (LIGHT & DARK MODE):
  * Strictly avoid hardcoded hex colors (e.g., Color(0xFF...)) in any Composable function! Always use semantic MaterialTheme.colorScheme tokens so the UI seamlessly adapts between Light and Dark themes without contrast issues:
    - Screen Backgrounds: MaterialTheme.colorScheme.background
    - Surfaces / Cards: MaterialTheme.colorScheme.surface
    - Primary actions & Branding: MaterialTheme.colorScheme.primary
    - Titles & High contrast text: MaterialTheme.colorScheme.onSurface
    - Subtitles & Secondary text: MaterialTheme.colorScheme.onSurfaceVariant
    - Dividers & Outlines: MaterialTheme.colorScheme.outlineVariant
  * Light Theme Tokens:
    - Primary: Sage Green (#6B8E23)
    - Primary Container: Soft Sage (#8FA853)
    - Secondary / Dividers: Muted Sand (#E8DFD8)
    - Background: Warm Off-White (#FBF9F5)
    - Surface / Cards: Pure White (#FFFFFF)
    - Text / OnSurface: Dark Forest Green (#2C3E35)
    - Text Secondary / OnSurfaceVariant: Muted Forest Green (#5C6F64)
  * Dark Theme Tokens:
    - Primary: Luminous Sage (#A8C673)
    - Primary Container: Deep Forest Surface Variant (#2E4239)
    - Secondary: Soft Muted Sage (#A3B5A8)
    - Background: Deep Tranquil Forest Night (#15201A)
    - Surface / Cards: Elevated Forest Surface (#22322A)
    - Text / OnSurface: Warm Off-White Text (#F1EFEA)
    - Text Secondary / OnSurfaceVariant: Soft Muted Sage (#A3B5A8)
    - Outline / Dividers: Forest Outline (#3B5045)

IMPLEMENT EXACTLY THESE 3 SCREENS (no more, no less):

1. Screen 1: Home Screen (HomeScreen.kt)
   - Layout: Column with background MaterialTheme.colorScheme.background, vertical arrangement spaced between.
   - Header (Top):
     * A top Row containing:
       - Centered column: App title "MINDFULDAYS" (MaterialTheme.typography.labelLarge, color MaterialTheme.colorScheme.primary) and subtitle "Atitude X de 9" (bodyMedium, color MaterialTheme.colorScheme.onSurfaceVariant).
       - Top-right corner: Standard IconButton with Icons.Default.Settings (tint MaterialTheme.colorScheme.onBackground) to navigate to SettingsScreen.
   - Central Card (ElevatedCard):
     * Container color MaterialTheme.colorScheme.surface, elevation 4.dp, padded content.
     * Attitude title in bold (headlineMedium, e.g., "Aceitação", color MaterialTheme.colorScheme.onSurface).
     * Attitude description (bodyLarge, e.g., "Reconheça e acolha o momento presente exatamente como ele é.", color MaterialTheme.colorScheme.onSurface).
     * Thin HorizontalDivider (color MaterialTheme.colorScheme.outlineVariant).
     * AI reflection text block (bodyMedium, italic, color MaterialTheme.colorScheme.onSurfaceVariant, displaying generated reflection or default).
     * Primary filled Button with sparkle icon: "✨ Nova Reflexão (Gemini IA)". Shows CircularProgressIndicator when loading.
   - Bottom Action:
     * A single full-width OutlinedButton: "⏱️ Iniciar Timer de Meditação" navigating to TimerScreen (border MaterialTheme.colorScheme.outlineVariant, contentColor MaterialTheme.colorScheme.primary).
   - STRICT EXCLUSIONS: Do NOT include bottom navigation bars, profile avatars, greetings, photo banners, audio players, or habit/streak charts.

2. Screen 2: Meditation Timer Screen (TimerScreen.kt)
   - TopAppBar: Title "Timer de Meditação" with back navigation arrow (Icons.AutoMirrored.Filled.ArrowBack).
   - Center Area:
     * Subtitle text: "Concentre-se na respiração" (bodyLarge, color MaterialTheme.colorScheme.onSurfaceVariant).
     * Minimalist circular countdown timer: A clean circular progress ring (Canvas drawArc with stroke width 8.dp: track color MaterialTheme.colorScheme.outlineVariant, progress color MaterialTheme.colorScheme.primary), large digital countdown text centered inside ("10:00" or mm:ss in headlineLarge/displayMedium, color MaterialTheme.colorScheme.onSurface), and status text below ("Pausado" / "Em andamento" / "Concluído", color MaterialTheme.colorScheme.onSurfaceVariant). Plays a gentle completion notification chime via RingtoneManager when finished.
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
      * In HomeScreen.kt, implement a stateful 'HomeScreen(viewModel: MindfulnessViewModel, onNavigateToSettings: () -> Unit, onNavigateToTimer: () -> Unit)' that collects 'viewModel.uiState' with lifecycle and delegates to a stateless 'HomeScreenContent'.
   - data/model/MindfulnessAttitude.kt: Data class fully defined with string resource IDs for i18n support:
     data class MindfulnessAttitude(val id: Int, val name: String = "", val description: String = "", @get:StringRes val nameRes: Int = 0, @get:StringRes val descriptionRes: Int = 0)
   - MainActivity.kt: Instantiates 'viewModel: MindfulnessViewModel = viewModel()' and performs simple state-based navigation between HomeScreen, TimerScreen, and SettingsScreen.

2. GENERATE AS EMPTY SKELETONS / STUBS (TO BE FILLED IN SUBSEQUENT WORKSHOP MODULE 3):
   - data/remote/GeminiApiService.kt: Generate as a SKELETON class stub with a placeholder method accepting languageCode and a TODO comment (students will implement this with Retrofit & Gemini API in Module 3):
     // TODO: Implement Google Gemini API call with Retrofit in Module 3
     class GeminiApiService {
         suspend fun generateReflection(attitudeTitle: String, languageCode: String = "pt"): String = "Respire fundo e traga sua atenção para o momento presente."
     }
   - data/repository/AttitudeRepository.kt: Generate as a SKELETON class stub with the exact method signature expected in Module 3 and a TODO comment:
     // TODO: Implement 9 Jon Kabat-Zinn attitudes & daily rotation in Module 3
     class AttitudeRepository {
         fun getTodayAttitude(): MindfulnessAttitude = MindfulnessAttitude(
             id = 3,
             name = "Aceitação",
             description = "Reconheça e acolha o momento presente exatamente como ele é.",
             nameRes = R.string.attitude_3_name,
             descriptionRes = R.string.attitude_3_desc
         )
     }
   - ui/viewmodel/MindfulnessViewModel.kt: Generate as an INITIAL SKELETON ViewModel with MindfulnessUiState (attitude, aiReflection, isLoadingAi) and StateFlow matching Module 3:
     // TODO: Connect Gemini API integration in Module 3
     data class MindfulnessUiState(
         val attitude: MindfulnessAttitude,
         val aiReflection: String = "“Acolher o presente não é conformismo, é o ponto de partida para qualquer transformação real.”",
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
                 delay(1000) // Simulated delay for UI preview
                 val reflection = geminiService.generateReflection(_uiState.value.attitude.name)
                 _uiState.update {
                     it.copy(
                         aiReflection = reflection,
                         isLoadingAi = false
                     )
                 }
             }
         }
     }

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
│   │   ├── Color.kt                  <- Tokens Material 3 oficiais (Modo Claro e Modo Escuro)
│   │   ├── Theme.kt                  <- Configuração de DarkColorScheme e LightColorScheme semânticos
│   │   └── Type.kt
│   └── viewmodel/
│       └── MindfulnessViewModel.kt   <- Esqueleto inicial de estado para a UI
└── MainActivity.kt                   <- Ponto de entrada e navegação básica entre as telas
```

Com a estrutura do projeto sincronizada e compilando no **Android Studio Stable**, avançamos para o **Módulo 3: Diretrizes com AGENTS.md, Implementação da UI em Compose e Integração com Gemini API**.
