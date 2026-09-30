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

Abra o painel do **Gemini** no Android Studio (**View → Tool Windows → Gemini**) ou utilize a janela **Create with AI**. Anexe as capturas de tela geradas no **Stitch** e cole o seguinte prompt estruturado:

```text
Create a modern Android application named 'MindfulDays' with package name 'dev.mindfuldays.app' using Jetpack Compose and Material Design 3.

Using the attached UI screenshots generated in Stitch as the visual source of truth, implement the following screens and functionality:

1. Home Screen: Implement a dashboard with a soft sage green (#6B8E23) and warm off-white (#FBF9F5) color palette. Include a top header displaying the current date and the 'Attitude of the Day' (cycling through 9 Jon Kabat-Zinn mindfulness attitudes). Place a central elevated card for daily AI reflections with a prompt button, and a bottom action to open the Timer.

2. Meditation Timer Screen: Implement a circular countdown timer starting at 10:00. Add Play, Pause, and Reset controls with clean Material 3 IconButton composables.

3. Settings Screen: Implement switches for 'Daily Attitude Reminder' and 'Meditation Time' with TimePicker dialogs for scheduling local notifications.

Core Architecture Requirements:
- Use Clean Architecture with MVVM pattern (ViewModel + StateFlow).
- Implement Material Design 3 Theme in ui/theme/ (Color.kt, Theme.kt, Type.kt).
- Create a service interface GeminiApiService for fetching reflections via Google Gemini API.
- Prepare string resources in res/values/strings.xml for Portuguese and English localization.

Ensure code is written in clean, idiomatic Kotlin using jetpack compose state management.
```

---

## 📁 2.4. Visão da Estrutura de Pacotes do Projeto

Após a execução do prompt e geração inicial, seu projeto em `dev.mindfuldays.app` estará organizado da seguinte forma:

```text
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
```

Com a estrutura do projeto sincronizada e compilando no **Android Studio Stable**, avançamos para o **Módulo 3: Diretrizes com AGENTS.md, Implementação da UI em Compose e Integração com Gemini API**.
