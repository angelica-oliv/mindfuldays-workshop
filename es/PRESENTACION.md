# 📽️ Presentación: MindfulDays — Taller Práctico de Android con IA (Versión en Español)

Guía completa y traducida al español de todas las diapositivas de la presentación para DevFest / conferencias en Perú.

---

## Diapositiva 1 — Portada
* **Título:** Taller Práctico
* **Subtítulo:** Construyendo la App "MindfulDays"
* **Badge:** ANDROID & IA
* **Enfoque:** Desarrollo Android Moderno y Consciente
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 2 — Sobre Mí
* **Título:** Sobre Mí
* **Nombre:** Angélica Oliveira
* **Bio:** Ingeniera de Software apasionada por crear soluciones de alto impacto para ecosistemas móviles.
* **Trayectoria:**
  * • 14 años de experiencia en desarrollo Android.
  * • Actualmente desempeñándose como Ingeniera de Automatización Senior en Airbnb.
* **AVISO / DISCLAIMER:**
  > Las opiniones y puntos de vista expresados en esta charla son estrictamente personales y no reflejan la posición de Airbnb, Inc. (o de sus afiliadas). Todo el contenido proporcionado tiene fines puramente informativos y no representa declaraciones, políticas o posiciones oficiales de Airbnb.
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 3 — Flujo de Trabajo
* **Título:** Flujo de Trabajo
* **Subtítulo:** Aplicación MindfulDays
* **Descripción:** Uniendo prácticas diarias de atención plena con Inteligencia Artificial en todo el ciclo de vida: modelos multimodales para UI, código declarativo y pruebas automatizadas.
* **Etapas Principales:**
  Del prototipo en Google Stitch al proyecto finalizado en Android Studio, dividido en 4 etapas principales:
  * **ETAPA 01 — Diseño:**
    * • Prototipo en Google Stitch
    * • Modelos multimodales para UI
  * **ETAPA 02 — Setup:**
    * • Proyecto en Android Studio
    * • Configuración de dependencias e IA
  * **ETAPA 03 — Código:**
    * • Código declarativo (Compose)
    * • Lógica y atención plena
  * **ETAPA 04 — CI/CD:**
    * • Pruebas automatizadas
    * • Integración y entrega continua con IA
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 4 — Concepto Base
* **Título:** El Concepto MindfulDays
* **Concepto Central:**
  * **Rotación Diaria:** Basado en las 9 Actitudes de Mindfulness de Jon Kabat-Zinn.
  * **Actitud del Día:** Tarjeta con mensajes reflexivos generados en tiempo real mediante Gemini API.
  * **Temporizador Minimalista:** Cronómetro predeterminado de 10:00 para meditación con sonido suave.
  * **Recordatorios Locales:** Notificaciones configurables para apoyar la práctica diaria.
* **Elemento Gráfico (Temporizador):**
  * `10:00`
  * Temporizador de Meditación
  * Sonido suave y avisos locales
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 5 — Flujo de Trabajo Asistido por IA
* **Título:** Flujo de Trabajo
* **Subtítulo:** Nuestro flujo asistido por IA se divide en cuatro etapas principales:
  * **01 — Etapa 1: Stitch (Design Tokens):** Prototipado ágil y extracción de Design Tokens.
  * **02 — Etapa 2: Studio (Android Studio):** Importación de pantallas con el asistente 'Create with AI' usando prompts multimodales.
  * **03 — Etapa 3: Compose (Jetpack Compose):** Construcción de la UI declarativa e integración de la lógica de negocio.
  * **04 — Etapa 4: Actions (GitHub Actions):** Pruebas automatizadas y pipeline de integración continua.
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 6 — Paso 01 // Stitch
* **Título:** Paso 01 // Stitch
* **Subtítulo:** Prototipado Visual
* **Contenido:**
  * El prototipado visual se acelera a partir de prompts descriptivos en Google Stitch.
  * El proceso involucra la captura de screenshots de las interfaces generadas para su posterior utilización en el flujo multimodal de Android Studio.
* **PROMPT STITCH:**
  > "Design Tokens MD3: Verde Salvia (#6B8E23), Blanco Cálido (#FBF9F5). Interfaz limpia y mindful para Android."
* **Design Tokens (Material 3):**
  * **Verde Salvia:** `#6B8E23` — Color Primario
  * **Blanco Cálido (Off-White):** `#FBF9F5` — Superficie / Fondo
  * **Negro Suave:** `#1E1E1E` — Tipografía / Contraste
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 7 — Setup del Proyecto
* **Título:** Setup del Proyecto
* **Subtítulo:** Configuración Inicial
* **Pasos:**
  * **01. IDE y Entorno:** Configuración inicial utilizando la versión Estable de Android Studio.
  * **02. Identificador Limpio:** Estándar de Package Name limpio y profesional: `dev.mindfuldays.app`.
  * **03. Asistente 'Create with AI':** Uso de Gemini adjuntando las capturas de pantalla de Stitch con un prompt multimodal.
* **Objetivo:** Generar estructura inicial y arquitectura MVVM.
* **Etiquetas:** Android Studio — Pixel 10 Pro | Gemini AI Multimodal
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 8 — Implementación
* **Título:** Implementación
* **Subtítulo:** Arquitectura e IA
* **Pilares:**
  * **Jetpack Compose:** Interfaz moderna implementada de forma declarativa y reactiva.
  * **Lógica de Negocio:** Ciclo de 9 días para alternar las actitudes en base a la fecha del sistema.
  * **Integración Gemini API:** Modelo `gemini-1.5-flash` para la generación de frases inspiradoras y reflexiones personalizadas en tiempo real.
* **Código de Ejemplo:**
  ```kotlin
  // Integración en Android Studio IDE
  val geminiFlash = GenerativeModel(
    modelName = "gemini-1.5-flash",
    apiKey = BuildConfig.apiKey
  )
  ```
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 9 — Calidad de Código
* **Título:** Calidad de Código
* **Subtítulo:** Garantía de Calidad y Automatización
* **Estrategia de Testing:**
  * **Pruebas Unitarias:** Validación de reglas de negocio y ViewModel. *(Stack: JUnit 5 + MockK)*
  * **Pruebas de UI:** Garantía de resiliencia visual y de comportamiento de la interfaz. *(Stack: Jetpack Compose Testing)*
  * **Pipeline de CI/CD:** Automatización continua ejecutada mediante GitHub Actions en cada commit (`.github/workflows/ci.yml`).
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 10 — Requisitos Previos y Material
* **Título:** Requisitos Previos y Material
* **Subtítulo:** Estructura del Repositorio y Requisitos Previos
* **Material Didáctico:** Estructurado en archivos Markdown modulares en GitHub, desde la introducción hasta CI/CD:
  ```text
  📂 repository-root/
  ├── 📄 README.md
  ├── 📂 es/
  │   ├── 📄 01-diseno-ui-stitch.md
  │   ├── 📄 02-setup-android-studio-ia.md
  │   ├── 📄 03-implementacion-compose-y-logica.md
  │   └── 📄 04-calidad-pruebas-cicd.md
  └── 📂 pt/
  ```
* **Checklist de Requisitos Previos:**
  * [x] **Android Studio Estable:** Versión Iguana, Jellyfish o superior instalada
  * [x] **JDK 17:** Configurado en el entorno
  * [x] **Cuenta en Google Stitch:** Activa
  * [x] **Clave Gratuita de Gemini API:** Obtenida directamente en Google AI Studio
* **Pie de página:** *Taller MindfulDays // Android*

---

## Diapositiva 11 — ¡Manos a la Obra!
* **Título:** ¡Manos a la Obra!
* **Subtítulo:** ¡Vamos a crear la app MindfulDays juntos!
* **Instrucciones para los Asistentes:**
  * **1.** Abre el repositorio del workshop en GitHub
  * **2.** Accede al archivo de orientaciones: `01-diseno-ui-stitch.md` (carpeta `es/`)
* **Acción:** Accede al Repositorio Ahora (Escanea el código QR para abrir en GitHub)
* **Pie de página:** *Taller MindfulDays // Android*
