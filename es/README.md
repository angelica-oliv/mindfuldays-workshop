# 🧘 MindfulDays — App de Meditación y Mindfulness desde Cero con IA

> 🌐 **Idiomas:** 🇪🇸 **Español (Perú)** | 🇧🇷 **[Português (Brasil)](../pt/README.md)**

¡Te damos la bienvenida al repositorio oficial del workshop **MindfulDays**! Este entrenamiento práctico fue estructurado para guiar a desarrolladores paso a paso en la creación de una aplicación Android moderna y funcional, combinando prototipado asistido por Inteligencia Artificial y desarrollo de vanguardia con **Jetpack Compose** y **Android Studio (versión Estable)**.

---

## 🎯 Objetivo del Workshop

Construir desde cero una aplicación completa de mindfulness enfocada en mostrar diariamente reflexiones basadas en las **9 Actitudes de Mindfulness de Jon Kabat-Zinn**, integrada con la **Gemini API** para la generación de consejos personalizados y equipada con un **Temporizador de Meditación** intuitivo.

En este workshop, los participantes aprenderán a:
1. Prototipar la interfaz gráfica y extraer tokens de diseño usando **Google Stitch**.
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
* **Internacionalización (i18n)**: Soporte nativo para Español e Inglés.

---

## 🛠️ Requisitos Técnicos Previos

Antes de iniciar los módulos prácticos, asegúrate de contar con los siguientes programas instalados y cuentas configuradas:

* **Android Studio**: Versión **Estable** más reciente (ej.: Iguana, Jellyfish o superior).
* **JDK**: Java Development Kit 17 o superior.
* **Llave de API de Gemini**: Obtén gratuitamente una API Key en [Google AI Studio](https://aistudio.google.com/).
* **Cuenta en Google Stitch / Figma**: Para generación e inspección de prototipos visuales.
* **Git y Cuenta en GitHub**: Para control de versiones del código y ejecución de pipelines de CI/CD.

---

## 📂 Módulos del Workshop (Guía Paso a Paso)

Sigue los archivos `.md` en la secuencia propuesta para completar el workshop:

1. [**`01-diseno-ui-stitch.md`**](./01-diseno-ui-stitch.md) — *Paso 1: Prototipado Visual, Sitemap y Design System en Google Stitch (Versión Sintética)*
2. [**`02-setup-android-studio-ia.md`**](./02-setup-android-studio-ia.md) — *Paso 2: Configuración de Android Studio Estable e Inicialización con Create with AI*
3. [**`03-implementacion-compose-y-logica.md`**](./03-implementacion-compose-y-logica.md) — *Paso 3: Directrices con AGENTS.md, Interfaz en Jetpack Compose, Reglas de las 9 Actitudes y Gemini API*
4. [**`04-calidad-pruebas-cicd.md`**](./04-calidad-pruebas-cicd.md) — *Paso 4: Pruebas Unitarias/UI, Pipeline en GitHub Actions y Buenas Prácticas*

---

## 🎨 Paleta de Colores del Proyecto (Material Design 3)

| Elemento | Nombre del Color | Hexadecimal |
| :--- | :--- | :--- |
| **Primary** | Verde Salvia | `#6B8E23` |
| **Secondary** | Arena Muted | `#E8DFD8` |
| **Background** | Blanco Cálido (Off-White) | `#FBF9F5` |
| **Surface** | Blanco Puro | `#FFFFFF` |
| **Text Primary** | Verde Bosque Oscuro | `#2C3E35` |

---

## 📄 Licencia

Este material se distribuye bajo la licencia MIT. Siéntete libre de utilizarlo y adaptarlo para tus charlas y workshops.
