# 🎨 Módulo 1 — Prototipado Visual y Design System en [Google Stitch](https://stitch.withgoogle.com/)

En este módulo, definiremos el flujo de pantallas de la app **MindfulDays** y utilizaremos **[Google Stitch](https://stitch.withgoogle.com/)** para generar la interfaz visual y extraer los *design tokens* en Material Design 3.

---

## 🗺️ 1.1. Estructura de las Pantallas (Sitemap)

La aplicación cuenta con un flujo simple centrado en 3 pantallas:

1. **Home Screen**: Muestra la fecha actual, la indicación de la actitud del día (en un ciclo de 1 a 9), tarjeta con frase reflexiva, botón de IA (*AI Sparkle*) para solicitar un consejo mediante la Gemini API y acceso directo al temporizador.
2. **Timer Screen**: Contador regresivo circular y minimalista para meditación con controles de play, pause e reset.
3. **Settings Screen**: Opciones de recordatorios y notificaciones diarias con selector de hora.

---

## 💬 1.2. Prompt de UI para [Google Stitch](https://stitch.withgoogle.com/)

Copia y pega el siguiente prompt en **[Google Stitch](https://stitch.withgoogle.com/)** para generar las pantallas de la app. El contexto de las 9 actitudes y las directrices de diseño ya están incorporados directamente en el prompt:

```text
Design a calm, minimalist mobile app interface for a Mindfulness application named "MindfulDays", based on Material Design 3 guidelines.

Concept:
An application that rotates daily through 9 Mindfulness Attitudes (Beginner's Mind, Non-Judging, Acceptance, Letting Go, Trust, Non-Striving, Patience, Gratitude, Generosity) based on Jon Kabat-Zinn's principles.

Color Palette:
- Primary: Soft sage green (#6B8E23)
- Secondary: Sand / Muted beige (#E8DFD8)
- Background: Warm off-white (#FBF9F5)
- Text / Content: Dark forest green (#2C3E35)

Screens required:
1. Home Screen: Top header with date and attitude indicator ("Attitude 3 of 9: Acceptance"). Large central card with a quote, an AI Sparkle action button for Gemini reflections, and a bottom shortcut button to the Meditation Timer.
2. Timer Screen: Minimalist circular countdown timer (default 10:00) with clean play, pause, and reset controls.
3. Settings Screen: Clean list with toggles for daily reminders ("Daily Attitude" and "Meditation Time") with time selector pickers.
```

---

## 🎨 1.3. Extracción de Assets y Tokens

Después de generar las pantallas en [Google Stitch](https://stitch.withgoogle.com/):
1. Captura capturas de pantalla (screenshots) en alta resolución de las 3 pantallas generadas (usarás estas imágenes en el Módulo 2 dentro de Android Studio).
2. Anota los tokens de colores para la configuración en **Jetpack Compose**:
   * `Primary`: `#6B8E23` (Sage Green)
   * `Secondary`: `#E8DFD8` (Sand)
   * `Background`: `#FBF9F5` (Warm Off-White)
   * `OnBackground`: `#2C3E35` (Dark Forest Green)

---

¡Listo! Con la interfaz prototipada en [Google Stitch](https://stitch.withgoogle.com/) y los tokens a mano, avanza al archivo **`02-setup-android-studio-ia.md`**.
