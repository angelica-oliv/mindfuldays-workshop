# 🧪 Módulo 4 — Calidad de Código, Pruebas Automatizadas y CI/CD en GitHub

En este último módulo del workshop, garantizaremos la calidad de ingeniería de la aplicación **MindfulDays**. Crearemos suites de pruebas unitarias para la regla de negocio de las 9 actitudes, implementaremos pruebas de UI con **Jetpack Compose** y configuraremos un pipeline automatizado de CI/CD utilizando **GitHub Actions**.

---

## 🔬 4.1. Pruebas Unitarias con JUnit y MockK

Crea el archivo de prueba en `app/src/test/java/dev/mindfuldays/app/AttitudeRepositoryTest.kt`:

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
    fun `garantizar que la lista contiene exactamente 9 actitudes de mindfulness`() {
        val attitudes = repository.attitudes
        assertEquals(9, attitudes.size)
    }

    @Test
    fun `garantizar que la actitud del dia retorna un valor valido dentro de las 9 opciones`() {
        val todayAttitude = repository.getTodayAttitude()
        assertNotNull(todayAttitude)
        assert(todayAttitude.id in 1..9)
    }
}
```

---

## 📱 4.2. Pruebas de Interfaz Declarativa en Jetpack Compose

Crea la prueba de UI en `app/src/androidTest/java/dev/mindfuldays/app/HomeScreenTest.kt`:

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
    fun mostrarTituloDeActitudYBotonDeIaEnHomeScreen() {
        val attitude = MindfulnessAttitude(3, "Aceptación", "Acoge el momento presente.")
        var clickedAi = false

        composeTestRule.setContent {
            MindfulDaysTheme {
                HomeScreen(
                    attitude = attitude,
                    aiReflection = "Reflexión de prueba",
                    isLoadingAi = false,
                    onGenerateAiReflection = { clickedAi = true },
                    onNavigateToTimer = {}
                )
            }
        }

        // Verifica la representación de los nodos
        composeTestRule.onNodeWithText("Aceptación").assertExists()
        composeTestRule.onNodeWithText("Reflexión de prueba").assertExists()

        // Dispara el clic en el botón de IA
        composeTestRule.onNodeWithText("✨ Nueva Reflexión (Gemini IA)").performClick()
        assert(clickedAi)
    }
}
```

---

## ⚙️ 4.3. Pipeline de CI/CD con GitHub Actions

Crea el archivo de workflow de GitHub Actions en `.github/workflows/ci.yml` en la raíz de tu repositorio:

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
      - name: Checkout del Repositorio
        uses: actions/checkout@v4

      - name: Configurar Java 17 (JDK)
        uses: actions/setup-java@v4
        with:
          distribution: 'temurin'
          java-version: '17'
          cache: 'gradle'

      - name: Conceder Permisos de Ejecución a Gradle Wrapper
        run: chmod +x gradlew

      - name: Ejecutar Lint y Análisis Estático
        run: ./gradlew lintDebug

      - name: Ejecutar Pruebas Unitarias
        run: ./gradlew testDebugUnitTest

      - name: Compilar la Aplicación (Build APK)
        run: ./gradlew assembleDebug

      - name: Subir los Artefactos de Build (APK)
        uses: actions/upload-artifact@v4
        with:
          name: MindfulDays-Debug-APK
          path: app/build/outputs/apk/debug/app-debug.apk
```

---

## 🚀 4.4. Checklist para Publicación del Workshop en GitHub

Para poner a disposición el repositorio oficial a tus asistentes:

1. **Inicializa Git en la raíz del proyecto**:
   ```bash
   git init
   git add .
   git commit -m "feat: estructura inicial del workshop MindfulDays"
   ```
2. **Crea un repositorio público en GitHub**:
   ```bash
   git remote add origin https://github.com/tu-usuario/mindful-days-workshop.git
   git branch -M main
   git push -u origin main
   ```
3. **Valida la ejecución en la pestaña Actions**: Confirma que el workflow de GitHub Actions se haya ejecutado exitosamente (estado verde) para la compilación y las pruebas.
4. **Instruye a los participantes**: El día del workshop, pide a los asistentes que hagan `git clone` del repositorio o que sigan la creación paso a paso a través de los archivos `.md`.

---

🎉 **¡Felicitaciones!** ¡Ahora cuentas con el material didáctico completo en Markdown y el repositorio estructurado para impartir tu workshop práctico con **Android Studio Estable**, **Stitch**, **Jetpack Compose** y **Gemini API**!
