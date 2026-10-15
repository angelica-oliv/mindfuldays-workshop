# 🧘 MindfulDays — App de Meditación y Mindfulness desde Cero con IA

> 🌐 **Idiomas:** 🇪🇸 **Español (Perú)** | 🇧🇷 **[Português (Brasil)](../pt/README.md)**

¡Te damos la bienvenida al repositorio oficial del workshop **MindfulDays**! Este entrenamiento práctico fue estructurado para guiar a desarrolladores paso a paso en la creación de una aplicación Android moderna y funcional, combinando prototipado asistido por Inteligencia Artificial y desarrollo de vanguardia con **Jetpack Compose** y **Android Studio (versión Estable)**.

---

## 🎯 Objetivo del Workshop

Construir desde cero una aplicación completa de mindfulness enfocada en mostrar diariamente reflexiones basadas en las **9 Actitudes de Mindfulness de Jon Kabat-Zinn**, integrada con la **Gemini API** para la generación de consejos personalizados y equipada con un **Temporizador de Meditación** intuitivo.

En este workshop, los participantes aprenderán a:
1. Prototipar la interfaz gráfica y extraer tokens de diseño usando **[Google Stitch](https://stitch.withgoogle.com/)**.
2. Crear la estructura del proyecto con asistentes de IA directamente en la versión **Estable de Android Studio**.
3. Estandarizar el contexto para agentes de IA con **AGENTS.md** y construir interfaces declarativas con **Jetpack Compose** y **Material Design 3**.
4. Integrar llamadas dinámicas de IA generativa con **Gemini**.
5. Configurar suites de pruebas y pipelines automatizados de CI/CD mediante **GitHub Actions**.

---

## 📱 Visión General de la App *MindfulDays*

* **Tarjeta de la Actitud del Día**: Presenta diariamente una de las 9 actitudes de mindfulness (ej.: *Aceptación*, *Mente de Principiante*, *Paciencia*) con rotación cíclica automática basada en la fecha del sistema.
* **Reflexión con Gemini API**: Botón para generar consejos y meditaciones guiadas en tiempo real mediante IA generativa.
* **Temporizador de Meditación**: Contador circular minimalista de concentración con controles de Play, Pause y Reset, además de emitir una señal sonora suave al finalizar.
* **Configuración y Notificaciones**: Opción de programación de recordatorios diarios para mantener la práctica.
* **Internacionalización (i18n)**: Soporte nativo para Español, Portugués e Inglés.
* **Soporte para Modo Oscuro**: Tema oscuro integrado con Material Design 3 y alto contraste.

---

## 🛠️ Requisitos Técnicos Previos

Antes de iniciar los módulos prácticos, asegúrate de contar con los siguientes programas instalados y cuentas configuradas:

* **Android Studio**: Versión **Estable** más reciente (ej.: Iguana, Jellyfish o superior).
* **JDK**: Java Development Kit 17 o superior.
* **Llave de API de Gemini**: Obtén gratuitamente una API Key en [Google AI Studio](https://aistudio.google.com/).
* **Cuenta en [Google Stitch](https://stitch.withgoogle.com/) / Figma**: Para generación e inspección de prototipos visuales.
* **Git y Cuenta en GitHub**: Para control de versiones del código y ejecución de pipelines de CI/CD.

---

## 📂 Módulos del Workshop (Guía Paso a Paso)

Sigue los archivos `.md` en la secuencia propuesta para completar el workshop:

1. [**`01-diseno-ui-stitch.md`**](./01-diseno-ui-stitch.md) — *Paso 1: Prototipado Visual, Sitemap y Design System en Google Stitch (Modo Claro y Oscuro)*
2. [**`02-setup-android-studio-ia.md`**](./02-setup-android-studio-ia.md) — *Paso 2: Configuración de Android Studio Estable e Inicialización con Create with AI*
3. [**`03-implementacion-compose-y-logica.md`**](./03-implementacion-compose-y-logica.md) — *Paso 3: Directrices con AGENTS.md, Interfaz en Jetpack Compose, Soporte Dual-Theme, 9 Actitudes y Gemini API*
4. [**`04-calidad-pruebas-cicd.md`**](./04-calidad-pruebas-cicd.md) — *Paso 4: Calidad de Software, Pruebas con IA y Robot Pattern (+ Pasos Opcionales: Ícono de la App con IA y Publicación en Play Store)*

---

## 🎨 Paleta de Colores del Proyecto (Material Design 3)

| Token M3 | Modo Claro (Light) | Modo Oscuro (Dark) | Descripción |
| :--- | :--- | :--- | :--- |
| **Primary** | `#6B8E23` (Verde Salvia) | `#A8C673` (Salvia Luminoso) | Destacados y botones principales |
| **Primary Container** | `#8FA853` (Salvia Suave) | `#2E4239` (Bosque Nocturno Elevado) | Contenedores de realce |
| **Secondary** | `#E8DFD8` (Arena Muted) | `#A3B5A8` (Salvia Muted Suave) | Elementos secundarios |
| **Background** | `#FBF9F5` (Blanco Cálido) | `#15201A` (Bosque Nocturno Profundo) | Fondo de la pantalla completa |
| **Surface** | `#FFFFFF` (Blanco Puro) | `#22322A` (Bosque Nocturno Elevado) | Fondo de tarjetas elevadas |
| **OnSurface / Text** | `#2C3E35` (Verde Bosque) | `#F1EFEA` (Blanco Cálido Claro) | Textos y títulos de alto contraste |

---

## 📄 Licencia

Este material se distribuye bajo la licencia MIT. Siéntete libre de utilizarlo y adaptarlo para tus charlas y workshops.
