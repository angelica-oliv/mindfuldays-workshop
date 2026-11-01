# 📽️ Presentación: MindfulDays — Taller Práctico de Android con IA (Guía de 1 Hora)

Guía completa y estructurada para impartir el taller o charla de **60 minutos** en DevFest o conferencias de tecnología. Incluye cronómetro sugerido, notas de la oradora (*speaker notes*), acciones en vivo y salvaguardas para la demo.

---

## ⏱️ Cronograma Maestro de 60 Minutos

| Bloque | Minutos | Diapositivas | Enfoque y Dinámica |
| :--- | :---: | :---: | :--- |
| **01. Intro & Concepto** | 00:00 – 05:00 *(5 min)* | Diapos 1 – 4 | Bienvenida, bio, disclaimer y concepto de las 9 Actitudes. |
| **02. Stitch & Design Tokens** | 05:00 – 15:00 *(10 min)* | Diapos 5 – 6 | Prototipado visual con IA, exportación de tokens Sage Green. |
| **03. Setup Android Studio** | 15:00 – 30:00 *(15 min)* | Diapo 7 | Proyecto con Create with AI + Prompt multimodal (3 pantallas). |
| **04. Compose, Gemini & AGENTS.md** | 30:00 – 45:00 *(15 min)* | Diapo 8 | **Prompt único**: API Key, rotación de actitudes, Retrofit y estado. |
| **05. Calidad y Robot Pattern** | 45:00 – 55:00 *(10 min)* | Diapo 9 | Pruebas unitarias de la regla de 9 días y UI tests expresivos. |
| **06. Q&A y Cierre** | 55:00 – 60:00 *(5 min)* | Diapos 10 – 11 | Preguntas, recursos, código QR al repositorio y despedida. |

---

## Diapositiva 1 — Portada `[00:00 - 02:00]`
* **Título:** Taller Práctico: De Cero a App de Mindfulness con IA
* **Subtítulo:** Construyendo la App "MindfulDays" en 60 minutos
* **Badge:** ANDROID & IA GENERATIVA
* **Enfoque:** Desarrollo Android Moderno, Rápido y Consciente
* **Pie de página:** *Taller MindfulDays // Android*
* 🎙️ **Notas de la Oradora:**
  > *"¡Hola a todos y bienvenidos! En esta hora no solo vamos a hablar de IA teórica; vamos a construir y ver funcionando una aplicación nativa de Android de alta fidelidad, con Jetpack Compose, Material 3 y Gemini API, usando IA como copiloto en cada etapa del ciclo de vida."*

---

## Diapositiva 2 — Sobre Mí `[02:00 - 03:30]`
* **Título:** Sobre Mí
* **Nombre:** Angélica Oliveira
* **Bio:** Ingeniera de Software apasionada por crear soluciones de alto impacto para ecosistemas móviles.
* **Trayectoria:**
  * • 14 años de experiencia en desarrollo Android.
  * • Actualmente desempeñándose como Ingeniera de Automatización Senior en Airbnb.
* **AVISO / DISCLAIMER:**
  > *Las opiniones y puntos de vista expresados en esta charla son estrictamente personales y no reflejan la posición de Airbnb, Inc. (o de sus afiliadas). Todo el contenido tiene fines puramente educativos.*
* 🎙️ **Notas de la Oradora:**
  > *"Comparto con ustedes mi experiencia de 14 años en Android y cómo la IA generativa ha transformado drásticamente mi flujo diario de desarrollo de prototipos a producción."*

---

## Diapositiva 3 — Flujo de Trabajo de 60 Minutos `[03:30 - 04:30]`
* **Título:** El Flujo del Taller (4 Etapas Ágiles)
* **Subtítulo:** Del Prototipo al Código Verificado
* **Las 4 Etapas:**
  * **01 // Diseño (10 min):** Google Stitch + Design Tokens (Light/Dark).
  * **02 // Setup (15 min):** Android Studio + Prompt Multimodal (3 pantallas).
  * **03 // Lógica e IA (15 min):** AGENTS.md + **Prompt Único** de Gemini API.
  * **04 // Calidad (10 min):** Pruebas Unitarias + Robot Pattern en Compose.
* 🎙️ **Notas de la Oradora:**
  > *"Para hacer un taller de 60 minutos sin fricción, eliminamos el boilerplate repetitivo: usamos un prompt multimodal en el setup y un solo prompt maestro para la lógica y la API de Gemini."*

---

## Diapositiva 4 — Concepto Base: MindfulDays `[04:30 - 05:00]`
* **Título:** El Concepto MindfulDays
* **Pilares de la App:**
  * **Rotación Diaria:** Basada en las 9 Actitudes de Mindfulness de Jon Kabat-Zinn (`(dia - 1) % 9`).
  * **Reflexión Diaria con IA:** Gemini API (`gemini-3.8-flash`) genera reflexiones serenas en tiempo real.
  * **Temporizador Circular Minimalista:** Canvas con cuenta regresiva, controles Play/Pause/Reset y timbre sonoro suave.
  * **Configuración y Recordatorios:** Switches accesibles para recordatorios locales.
* 🎙️ **Notas de la Oradora:**
  > *"MindfulDays resuelve un caso de uso real: una experiencia minimalista, sin pantallas innecesarias ni configuraciones complejas."*

---

## Diapositiva 5 — Paso 01 // Google Stitch y Design Tokens `[05:00 - 10:00]`
* **Título:** Paso 01 // Prototipado Visual en Google Stitch
* **Subtítulo:** Generación Rápida de Interfaz y Tokens
* **Contenido:**
  * Prototipado ultra-rápido en Google Stitch con prompts descriptivos.
  * Exportación de capturas de pantalla para alimentar el flujo multimodal de Android Studio.
* **PROMPT STITCH:**
  > *"Design Tokens MD3: Verde Salvia (#6B8E23), Blanco Cálido (#FBF9F5). Interfaz limpia y mindful para Android."*
* **Design Tokens Extraídos:**
  * **Verde Salvia:** `#6B8E23` (Primario) / `#A8C673` (Dark Primario)
  * **Blanco Cálido / Fondo:** `#FBF9F5` (Light) / `#15201A` (Bosque Nocturno Dark)
  * **Texto OnSurface:** `#2C3E35` (Verde Bosque) / `#F1EFEA` (Texto Claro)
* 💻 **Acción en Vivo:**
  * Mostrar en el navegador la pantalla generada en Stitch durante 2 minutos.
  * Descargar o mostrar los 3 screenshots (`home`, `timer`, `settings`).

---

## Diapositiva 6 — De Stitch a Android Studio `[10:00 - 15:00]`
* **Título:** La Conexión Multimodal
* **Subtítulo:** Cómo la IA Traduce Diseño en Código Limpio
* **Puntos Clave:**
  * Adjuntar las imágenes de Stitch en **Gemini en Android Studio** o **Create with AI**.
  * Guiar a la IA con guardrails estrictos: **Material 3 nativo**, **sin colores hex hardcodeados** y **exactamente 3 pantallas**.
* 🎙️ **Notas de la Oradora:**
  > *"El secreto para no perder tiempo en el taller es ser hiper-prescriptivos: le decimos a la IA qué componentes usar, qué excluir y que cree esqueletos vacíos para la lógica que conectaremos después."*

---

## Diapositiva 7 — Paso 02 // Setup en Android Studio Estable `[15:00 - 30:00]`
* **Título:** Paso 02 // Setup del Proyecto con IA
* **Subtítulo:** Inicialización y Arquitectura MVVM
* **Parámetros del Proyecto:**
  * **Package Name:** `dev.mindfuldays.app`
  * **UI Toolkit:** Jetpack Compose + Material 3
  * **Modo de Ejecución Rápida:** Limitado a 2 tareas de código + verificación con `./gradlew assembleDebug` (evita bucles largos de linters o emuladores lentos).
* **Estructura Generada:**
  * `ui/home/HomeScreen.kt`, `ui/timer/TimerScreen.kt`, `ui/settings/SettingsScreen.kt`
  * `ui/theme/Color.kt`, `Theme.kt`, `Type.kt`
  * Esqueletos: `AttitudeRepository`, `GeminiApiService`, `MindfulnessViewModel`
* 💻 **Acción en Vivo:**
  * Enviar el prompt multimodal en Android Studio.
  * Mientras compila (1-2 min), explicar la regla de exclusión estricta (no inventar barras inferiores ni auth).

---

## Diapositiva 8 — Paso 03 // AGENTS.md, Lógica y Gemini API `[30:00 - 45:00]`
* **Título:** Paso 03 // Un Solo Prompt para Todo el Módulo 3
* **Subtítulo:** Conectando Dominio, IA Generativa y Seguridad
* **La Ventaja de `AGENTS.md`:**
  * Actúa como contexto operacional permanente: la IA no olvida tokens ni reglas de negocio.
* **El Prompt Maestro (Todo en Uno):**
  1. **Seguridad:** Inyección de `GEMINI_API_KEY` desde `local.properties` a `BuildConfig`.
  2. **i18n:** Cadenas en Inglés, Español y Portugués (`strings.xml`).
  3. **Regla de 9 Actitudes:** Fórmula cíclica `(dia - 1) % 9` en `AttitudeRepository`.
  4. **Gemini API:** Modelo `gemini-3.8-flash` vía Retrofit + Moshi codegen + fallback offline.
  5. **StateFlow:** Exposición limpia de `MindfulnessUiState` en el ViewModel.
* 💻 **Acción en Vivo:**
  * Mostrar el archivo `AGENTS.md` en la raíz.
  * Pegar el prompt maestro de Módulo 3.2 en Gemini.
  * Ejecutar `./gradlew assembleDebug` y correr la app en el emulador para ver la reflexión en vivo generada por Gemini.

---

## Diapositiva 9 — Paso 04 // Calidad de Software y Robot Pattern `[45:00 - 55:00]`
* **Título:** Paso 04 // Pruebas con IA y Robot Pattern
* **Subtítulo:** Calidad Sostenible sin Frustraciones
* **Estrategia en 2 Niveles:**
  * **1. Pruebas Unitarias (`AttitudeRepositoryTest`):**
    * Validación determinística de la rotación: día 1, día 9, reinicio en día 10 y fin de año (día 365).
  * **2. UI Testing con Robot Pattern (`HomeRobot`):**
    * Separa el *QUÉ* se prueba del *CÓMO* interactúa Compose Test Rule.
* **Código Fluido:**
  ```kotlin
  homeRobot(composeTestRule) {
      assertAttitudeName("Aceptación")
      clickGenerateReflection("✨ Nueva Reflexión")
  }
  ```
* 💻 **Acción en Vivo:**
  * Ejecutar `./gradlew testDebugUnitTest` en terminal y mostrar los tests pasando en verde.

---

## Diapositiva 10 — Resumen de Herramientas & Checklist `[55:00 - 57:00]`
* **Título:** Stack del Taller & Buenas Prácticas
* **Resumen:**
  * ✅ **Google Stitch:** Prototipos y tokens de color instantáneos.
  * ✅ **AGENTS.md:** Reducción del 90% de alucinaciones y contexto repetitivo.
  * ✅ **Prompting Prescriptivo:** Cero pantallas inventadas y stubs limpios.
  * ✅ **Gemini 3.8 Flash:** Respuestas rápidas con fallback seguro offline.
  * ✅ **Robot Pattern:** Pruebas de Compose legibles y desacopladas.

---

## Diapositiva 11 — ¡Manos a la Obra & Recursos! `[57:00 - 60:00]`
* **Título:** Recursos y Repositorio Oficial
* **Subtítulo:** ¡Todo el código, guías y prompts listos para usar!
* **Acciones:**
  * 🌐 **Repositorio GitHub:** `github.com/angelica-oliv/mindfuldays-workshop`
  * 📱 **Guías Modulares:** Carpetas `/es` y `/pt` con prompts listos para copiar.
  * ❓ **Preguntas y Respuestas (Q&A)**
* 🎙️ **Notas de la Oradora:**
  > *"¡Muchas gracias por acompañarme en este taller! Tienen todo el material disponible en el repositorio para recrearlo a su propio ritmo. ¿Qué preguntas tenemos?"*
