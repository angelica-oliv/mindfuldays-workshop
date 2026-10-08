# 🎨 Módulo 1 — Prototipagem Visual e Design System no [Google Stitch](https://stitch.withgoogle.com/)

Neste módulo, vamos definir o fluxo de telas do app **MindfulDays** e utilizar o **[Google Stitch](https://stitch.withgoogle.com/)** para gerar a interface visual e extrair os *design tokens* em Material Design 3.

---

## 🗺️ 1.1. Estrutura das Telas (Sitemap)

O aplicativo possui um fluxo simples centrado em 3 telas:

1. **Home Screen**: Exibe a data atual, a indicação da atitude do dia (em ciclo de 1 a 9), card com frase reflexiva, botão de IA (*AI Sparkle*) para buscar um conselho via Gemini API e atalho para o timer.
2. **Timer Screen**: Contador regressivo circular e minimalista para meditação com controles de play, pause e reset.
3. **Settings Screen**: Opções de lembretes e notificações diárias com seletor de horário.

---

## 💬 1.2. Prompt de UI para o [Google Stitch](https://stitch.withgoogle.com/)

Copie e cole o prompt abaixo no **[Google Stitch](https://stitch.withgoogle.com/)** para gerar as telas do app. O contexto das 9 atitudes e as diretrizes de design já estão embarcados diretamente no prompt:

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

## 🎨 1.3. Extração de Assets e Tokens

Após gerar as telas no [Google Stitch](https://stitch.withgoogle.com/):
1. Capture screenshots em alta resolução das 3 telas geradas (você usará essas imagens no Módulo 2 no Android Studio).
2. Anote os tokens de cores para configuração no **Jetpack Compose**:
   * `Primary`: `#6B8E23` (Sage Green)
   * `Secondary`: `#E8DFD8` (Sand)
   * `Background`: `#FBF9F5` (Warm Off-White)
   * `OnBackground`: `#2C3E35` (Dark Forest Green)

---

Pronto! Com a interface prototipada no [Google Stitch](https://stitch.withgoogle.com/) e os tokens em mãos, avance para o **`02-setup-android-studio-ai.md`**.
