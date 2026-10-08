# 🎨 Módulo 1 — Prototipado Visual y Design System en [Google Stitch](https://stitch.withgoogle.com/)

En este módulo, definiremos el flujo de pantallas de la app **MindfulDays** y utilizaremos **[Google Stitch](https://stitch.withgoogle.com/)** para generar la interfaz visual y extraer los *design tokens* en Material Design 3.

---

## 🗺️ 1.1. Estructura de las Pantallas (Sitemap)

La aplicación cuenta con un flujo simple centrado en 3 pantallas:

1. **Home Screen**: Muestra la fecha actual, la indicación de la actitud del día (en un ciclo de 1 a 9), tarjeta con frase reflexiva, botón de IA (*AI Sparkle*) para solicitar un consejo mediante la Gemini API y acceso directo al temporizador.
2. **Timer Screen**: Contador regresivo circular y minimalista para meditación con controles de play, pause e reset.
3. **Settings Screen**: Opciones de recordatorios y notificaciones diarias con selector de hora.

---

## 💬 1.2. Prompt de UI Prescriptivo para [Google Stitch](https://stitch.withgoogle.com/)

Para asegurar que la IA genere un diseño limpio, didáctico y 100% alineado con los componentes nativos de Android (evitando que Stitch cree fuentes personalizadas o pantallas sobrecargadas con gráficos y reproductores de audio complejos), utiliza este prompt prescriptivo:

```text
Design an ultra-minimalist, clean Android mobile application interface for a tutorial app named "MindfulDays", strictly adhering to Material Design 3.

IMPORTANT DESIGN SYSTEM CONSTRAINTS (STRICT):
- Components: Use ONLY standard native Android Material 3 components (TopAppBar, ElevatedCard, Button, OutlinedButton, IconButton, Switch, OutlinedTextField, HorizontalDivider). DO NOT create custom complex components, custom pills, audio waveforms, habit streaks, or charts.
- Typography: Use standard Android system default typography (Roboto / system sans-serif). DO NOT use custom, serif, or imported fonts (no Newsreader, no Plus Jakarta Sans).
- Layout: Pure single-column layout with generous whitespace. Keep screens extremely simple and didactic for a live-coding workshop.
- Color Palette:
  * Primary: Soft sage green (#6B8E23)
  * Secondary / Dividers: Sand / Muted beige (#E8DFD8)
  * Background: Warm off-white (#FBF9F5)
  * Surface / Cards: Pure white (#FFFFFF)
  * Text / Icons: Dark forest green (#2C3E35)

REQUIRED SCREENS & EXACT ELEMENTS:

1. Screen 1 — Home Screen:
   - Header (Top): App title "MINDFULDAYS" in small uppercase label + subtitle "Atitude 3 de 9" + a single Settings gear IconButton on the top-right corner.
   - Central ElevatedCard:
     * Attitude title in bold headline: "Aceitação"
     * Attitude description: "Reconheça e acolha o momento presente exatamente como ele é."
     * A thin horizontal divider
     * AI reflection text block: "Acolher o presente não é conformismo, é o ponto de partida para qualquer transformação real."
     * Primary filled Button with sparkle icon: "✨ Nova Reflexão (Gemini IA)"
   - Bottom Action: A single OutlinedButton spanning the width: "⏱️ Iniciar Timer de Meditação".
   (DO NOT include: profile avatar, greetings, photo banners, audio player, streak tracker, or bottom navigation bar).

2. Screen 2 — Meditation Timer Screen:
   - TopAppBar: Title "Timer de Meditação" with a back navigation arrow.
   - Center Area:
     * Subtitle text: "Concentre-se na respiração"
     * Single minimalist circular progress ring with large digital countdown text in center: "10:00" and a status text below: "Pausado".
   - Bottom Controls: Exactly two buttons in a centered horizontal row:
     * Reset OutlinedIconButton (circular refresh icon)
     * Play/Pause large FilledIconButton (circular primary button with Play icon)
   (DO NOT include: multiple dials, duration selector chips, interval bells, background sounds, or chime pickers).

3. Screen 3 — Settings Screen:
   - TopAppBar: Title "Configurações" with a back navigation arrow.
   - Reminders Card (Surface):
     * Row with text "Lembrete da Atitude Diária" and standard native Material 3 Switch (checked).
     * Thin horizontal divider.
     * Row with text "Lembrete para Meditar" and standard native Material 3 Switch (unchecked).
   - Gemini API Card (Surface):
     * Text label: "Chave de API do Gemini"
     * Standard OutlinedTextField with placeholder "Cole sua API Key aqui..."
     * Primary Button: "Salvar Chave"
   (DO NOT include: time wheel dialogs, sound selectors, nested accordion cards, or multi-tab navigation).
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
