# 🧪 Módulo 4 — Qualidade de Código, Testes Automatizados e CI/CD no GitHub

Neste último módulo do workshop, garantiremos a qualidade de engenharia do aplicativo **MindfulDays**. Vamos criar suítes de testes unitários para a regra de negócio das 9 atitudes, implementar testes de UI com **Jetpack Compose** e configurar uma pipeline automatizada de CI/CD usando **GitHub Actions**.

---

## 🔬 4.1. Testes Unitários com JUnit 5 e MockK

Crie o arquivo de teste em `app/src/test/java/dev/mindfuldays/app/AttitudeRepositoryTest.kt`:

```kotlin
package dev.mindfuldays.app

import dev.mindfuldays.app.data.repository.AttitudeRepository
import org.junit.Assert.assertEquals
import org.junit.Assert.assertNotNull
import org.junit.Before
import org.junit.Test

class AttitudeRepositoryTest {

    private lateinit var repository: AttitudeRepository

    @Before
    fun setUp() {
        repository = AttitudeRepository()
    }

    @Test
    fun `garantir que a lista possui exatamente 9 atitudes de mindfulness`() {
        val attitudes = repository.attitudes
        assertEquals(9, attitudes.size)
    }

    @Test
    fun `garantir que a atitude do dia retorna um valor valido dentro das 9 opções`() {
        val todayAttitude = repository.getTodayAttitude()
        assertNotNull(todayAttitude)
        assert(todayAttitude.id in 1..9)
    }
}
```

---

## 📱 4.2. Testes de Interface Declarativa no Jetpack Compose

Crie o teste de UI em `app/src/androidTest/java/dev/mindfuldays/app/HomeScreenTest.kt`:

```kotlin
package dev.mindfuldays.app

import androidx.compose.ui.test.junit4.createComposeRule
import androidx.compose.ui.test.onNodeWithText
import androidx.compose.ui.test.performClick
import dev.mindfuldays.app.data.model.MindfulnessAttitude
import dev.mindfuldays.app.ui.home.HomeScreen
import dev.mindfuldays.app.ui.theme.MindfulDaysTheme
import org.junit.Rule
import org.junit.Test

class HomeScreenTest {

    @get:Rule
    val composeTestRule = createComposeRule()

    @Test
    fun exibirTituloDaAtitudeEBotaoDeIaNaHomeScreen() {
        val attitude = MindfulnessAttitude(3, "Aceitação", "Acolha o momento presente.")
        var clickedAi = false

        composeTestRule.setContent {
            MindfulDaysTheme {
                HomeScreen(
                    attitude = attitude,
                    aiReflection = "Reflexão de teste",
                    isLoadingAi = false,
                    onGenerateAiReflection = { clickedAi = true },
                    onNavigateToTimer = {}
                )
            }
        }

        // Verifica renderização dos nós
        composeTestRule.onNodeWithText("Aceitação").assertExists()
        composeTestRule.onNodeWithText("Reflexão de teste").assertExists()

        // Dispara clique no botão da IA
        composeTestRule.onNodeWithText("✨ Nova Reflexão (Gemini IA)").performClick()
        assert(clickedAi)
    }
}
```

---

## ⚙️ 4.3. Pipeline de CI/CD com GitHub Actions

Crie o arquivo de workflow do GitHub Actions em `.github/workflows/ci.yml` na raiz do seu repositório:

```yaml
name: MindfulDays Android CI

on:
  push:
    branches: [ "main", "develop" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do Repositório
        uses: actions/checkout@v4

      - name: Configurar Java 17 (JDK)
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'
          cache: 'gradle'

      - name: Conceder Permissões de Execução ao Gradle Wrapper
        run: chmod +x gradlew

      - name: Executar Lint e Análise Estática
        run: ./gradlew lintDebug

      - name: Executar Testes Unitários
        run: ./gradlew testDebugUnitTest

      - name: Compilar o Aplicativo (Build APK)
        run: ./gradlew assembleDebug

      - name: Upload dos Artefatos de Build (APK)
        uses: actions/upload-artifact@v4
        with:
          name: MindfulDays-Debug-APK
          path: app/build/outputs/apk/debug/app-debug.apk
```

---

## 🚀 4.4. Checklist para Publicação do Workshop no GitHub

Para disponibilizar o repositório oficial para os seus alunos:

1. **Inicie o Git na raiz do projeto**:
   ```bash
   git init
   git add .
   git commit -m "feat: estrutura inicial do workshop MindfulDays"
   ```
2. **Crie um repositório público no GitHub**:
   ```bash
   git remote add origin https://github.com/seu-usuario/mindful-days-workshop.git
   git branch -M main
   git push -u origin main
   ```
3. **Valide a execução da aba Actions**: Confirme se o workflow do GitHub Actions rodou com sucesso (status verde) para a compilação e os testes.
4. **Instrua os participantes**: No dia do workshop, peça para os alunos darem um `git clone` no repositório ou acompanharem a criação passo a passo seguindo os arquivos `.md`.

---

🎉 **Parabéns!** Você tem agora o material didático completo em Markdown e o repositório estruturado para conduzir seu workshop prático em outubro com **Android Studio Stable**, **Stitch**, **Jetpack Compose** e **Gemini API**!
