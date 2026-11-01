# 📽️ Apresentação: MindfulDays — Workshop Prático de Android com IA (Guia de 1 Hora)

Guia completo e estruturado para ministrar o workshop ou palestra de **60 minutos** no DevFest ou conferências de tecnologia. Inclui cronômetro sugerido, notas da palestrante (*speaker notes*), ações ao vivo e dicas de segurança para a demo.

---

## ⏱️ Cronograma Mestre de 60 Minutos

| Bloco | Minutos | Slides | Foco e Dinâmica |
| :--- | :---: | :---: | :--- |
| **01. Intro & Conceito** | 00:00 – 05:00 *(5 min)* | Slides 1 – 4 | Boas-vindas, bio, disclaimer e conceito das 9 Atitudes. |
| **02. Stitch & Design Tokens** | 05:00 – 15:00 *(10 min)* | Slides 5 – 6 | Prototipagem visual com IA, extração de tokens Verde Sálvia. |
| **03. Setup Android Studio** | 15:00 – 30:00 *(15 min)* | Slide 7 | Projeto com Create with AI + Prompt multimodal (3 telas). |
| **04. Compose, Gemini & AGENTS.md** | 30:00 – 45:00 *(15 min)* | Slide 8 | **Prompt único**: API Key, rotação de atitudes, Retrofit e estado. |
| **05. Qualidade e Robot Pattern** | 45:00 – 55:00 *(10 min)* | Slide 9 | Testes unitários da regra de 9 dias e UI tests expressivos. |
| **06. Q&A e Encerramento** | 55:00 – 60:00 *(5 min)* | Slides 10 – 11 | Perguntas, recursos, QR code para o repositório e encerramento. |

---

## Slide 1 — Capa `[00:00 - 02:00]`
* **Título:** Workshop Prático: Do Zero a um App de Mindfulness com IA
* **Subtítulo:** Construindo o App "MindfulDays" em 60 minutos
* **Badge:** ANDROID & IA GENERATIVA
* **Foco:** Desenvolvimento Android Moderno, Rápido e Consciente
* **Rodapé:** *Workshop MindfulDays // Android*
* 🎙️ **Notas da Palestrante:**
  > *"Olá a todos e sejam muito bem-vindos! Nesta hora não vamos apenas falar de teoria sobre IA; vamos construir e ver funcionando um aplicativo nativo Android completo, com Jetpack Compose, Material 3 e Gemini API, usando IA como copiloto em cada etapa do ciclo de vida."*

---

## Slide 2 — Sobre Mim `[02:00 - 03:30]`
* **Título:** Sobre Mim
* **Nome:** Angélica Oliveira
* **Bio:** Engenheira de Software apaixonada por criar soluções de alto impacto para ecossistemas mobile.
* **Trajetória:**
  * • 14 anos de experiência em desenvolvimento Android.
  * • Atualmente atuando como Engenheira de Automação Sênior no Airbnb.
* **AVISO / DISCLAIMER:**
  > *As opiniões e pontos de vista expressos nesta palestra são estritamente pessoais e não refletem a posição do Airbnb, Inc. (ou de suas afiliadas). Todo o conteúdo tem finalidade puramente educacional.*
* 🎙️ **Notas da Palestrante:**
  > *"Compartilho com vocês minha bagagem de 14 anos no ecossistema Android e como a IA generativa acelerou radicalmente meu fluxo diário de prototipagem à produção."*

---

## Slide 3 — Fluxo de Trabalho de 60 Minutos `[03:30 - 04:30]`
* **Título:** O Fluxo do Workshop (4 Etapas Ágeis)
* **Subtítulo:** Do Protótipo ao Código Verificado
* **As 4 Etapas:**
  * **01 // Design (10 min):** Google Stitch + Design Tokens (Light/Dark).
  * **02 // Setup (15 min):** Android Studio + Prompt Multimodal (3 telas).
  * **03 // Lógica e IA (15 min):** AGENTS.md + **Prompt Único** da Gemini API.
  * **04 // Qualidade (10 min):** Testes Unitários + Robot Pattern em Compose.
* 🎙️ **Notas da Palestrante:**
  > *"Para tornar este workshop viável em 60 minutos sem atrito, eliminamos todo o boilerplate repetitivo: usamos um prompt multimodal no setup e um único prompt mestre para a lógica e a API do Gemini."*

---

## Slide 4 — Conceito Base: MindfulDays `[04:30 - 05:00]`
* **Título:** O Conceito MindfulDays
* **Pilares do App:**
  * **Rotação Diária:** Baseada nas 9 Atitudes de Mindfulness de Jon Kabat-Zinn (`(dia - 1) % 9`).
  * **Reflexão Diária com IA:** Gemini API (`gemini-3.8-flash`) gera reflexões serenas em tempo real.
  * **Timer Circular Minimalista:** Canvas com contagem regressiva, controles Play/Pause/Reset e sinal sonoro suave.
  * **Configurações e Lembretes:** Switches acessíveis para lembretes locais.
* 🎙️ **Notas da Palestrante:**
  > *"O MindfulDays resolve um caso de uso real: uma experiência minimalista, sem telas desnecessárias nem configurações complexas."*

---

## Slide 5 — Passo 01 // Google Stitch e Design Tokens `[05:00 - 10:00]`
* **Título:** Passo 01 // Prototipagem Visual no Google Stitch
* **Subtítulo:** Geração Rápida de Interface e Tokens
* **Conteúdo:**
  * Prototipagem ultra-rápida no Google Stitch a partir de prompts descritivos.
  * Exportação de capturas de tela para alimentar o fluxo multimodal do Android Studio.
* **PROMPT STITCH:**
  > *"Design Tokens MD3: Verde Sálvia (#6B8E23), Off-White (#FBF9F5). Interface limpa e mindful para Android."*
* **Design Tokens Extraídos:**
  * **Verde Sálvia:** `#6B8E23` (Primário Light) / `#A8C673` (Primário Dark)
  * **Off-White / Fundo:** `#FBF9F5` (Light) / `#15201A` (Floresta Noturno Dark)
  * **Texto OnSurface:** `#2C3E35` (Verde Floresta) / `#F1EFEA` (Texto Claro)
* 💻 **Ação ao Vivo:**
  * Mostrar no navegador a tela gerada no Stitch por 2 minutos.
  * Baixar ou mostrar os 3 screenshots (`home`, `timer`, `settings`).

---

## Slide 6 — Do Stitch ao Android Studio `[10:00 - 15:00]`
* **Título:** A Conexão Multimodal
* **Subtítulo:** Como a IA Converte Design em Código Limpo
* **Pontos-Chave:**
  * Anexar as imagens do Stitch no **Gemini no Android Studio** ou **Create with AI**.
  * Guiar a IA com guardrails rígidos: **Material 3 nativo**, **sem cores hex hardcoded** e **exatamente 3 telas**.
* 🎙️ **Notas da Palestrante:**
  > *"O segredo para não perder tempo no workshop é sermos hiper-prescritivos: dizemos à IA quais componentes usar, o que excluir e para criar stubs vazios da lógica que conectaremos depois."*

---

## Slide 7 — Passo 02 // Setup no Android Studio Stable `[15:00 - 30:00]`
* **Título:** Passo 02 // Setup do Projeto com IA
* **Subtítulo:** Inicialização e Arquitetura MVVM
* **Parâmetros do Projeto:**
  * **Package Name:** `dev.mindfuldays.app`
  * **UI Toolkit:** Jetpack Compose + Material 3
  * **Modo de Execução Rápida:** Limitado a 2 tarefas de código + verificação com `./gradlew assembleDebug` (evita loops longos de linters ou emuladores lentos).
* **Estrutura Gerada:**
  * `ui/home/HomeScreen.kt`, `ui/timer/TimerScreen.kt`, `ui/settings/SettingsScreen.kt`
  * `ui/theme/Color.kt`, `Theme.kt`, `Type.kt`
  * Esqueletos: `AttitudeRepository`, `GeminiApiService`, `MindfulnessViewModel`
* 💻 **Ação ao Vivo:**
  * Enviar o prompt multimodal no Android Studio.
  * Enquanto compila (1-2 min), explicar a regra de exclusão rígida (não inventar barras inferiores nem autenticação).

---

## Slide 8 — Passo 03 // AGENTS.md, Lógica e Gemini API `[30:00 - 45:00]`
* **Título:** Passo 03 // Um Único Prompt para Todo o Módulo 3
* **Subtítulo:** Conectando Domínio, IA Generativa e Segurança
* **A Vantagem do `AGENTS.md`:**
  * Atua como contexto operacional permanente: a IA não esquece tokens nem regras de negócio.
* **O Prompt Mestre (Tudo em Um):**
  1. **Segurança:** Injeção da `GEMINI_API_KEY` do `local.properties` no `BuildConfig`.
  2. **i18n:** Strings em Inglês, Português e Espanhol (`strings.xml`).
  3. **Regra das 9 Atitudes:** Fórmula cíclica `(dia - 1) % 9` no `AttitudeRepository`.
  4. **Gemini API:** Modelo `gemini-3.8-flash` via Retrofit + Moshi codegen + fallback offline.
  5. **StateFlow:** Exposição limpa de `MindfulnessUiState` no ViewModel.
* 💻 **Ação ao Vivo:**
  * Mostrar o arquivo `AGENTS.md` na raiz do projeto.
  * Colar o prompt mestre do Módulo 3 no Gemini.
  * Executar `./gradlew assembleDebug` e rodar o app no emulador para ver a reflexão gerada pelo Gemini em tempo real.

---

## Slide 9 — Passo 04 // Qualidade de Software e Robot Pattern `[45:00 - 55:00]`
* **Título:** Passo 04 // Testes com IA e Robot Pattern
* **Subtítulo:** Qualidade Sustentável sem Dores de Cabeça
* **Estratégia em 2 Níveis:**
  * **1. Testes Unitários (`AttitudeRepositoryTest`):**
    * Validação determinística da rotação: dia 1, dia 9, reinício no dia 10 e fim do ano (dia 365).
  * **2. UI Testing com Robot Pattern (`HomeRobot`):**
    * Separa o *O QUE* é testado do *COMO* o Compose Test Rule interage com os nós.
* **Código Fluido:**
  ```kotlin
  homeRobot(composeTestRule) {
      assertAttitudeName("Aceitação")
      clickGenerateReflection("✨ Nova Reflexão")
  }
  ```
* 💻 **Ação ao Vivo:**
  * Executar `./gradlew testDebugUnitTest` no terminal e mostrar os testes passando em verde.

---

## Slide 10 — Resumo de Ferramentas & Checklist `[55:00 - 57:00]`
* **Título:** Stack do Workshop & Boas Práticas
* **Resumo:**
  * ✅ **Google Stitch:** Protótipos e tokens de cor instantâneos.
  * ✅ **AGENTS.md:** Redução de 90% das alucinações e do contexto repetitivo.
  * ✅ **Prompting Prescritivo:** Zero telas inventadas e stubs limpos.
  * ✅ **Gemini 3.8 Flash:** Respostas ágeis com fallback seguro offline.
  * ✅ **Robot Pattern:** Testes em Compose legíveis e desacoplados.

---

## Slide 11 — Mãos à Obra & Recursos! `[57:00 - 60:00]`
* **Título:** Recursos e Repositório Oficial
* **Subtítulo:** Todo o código, guias e prompts prontos para usar!
* **Ações:**
  * 🌐 **Repositório GitHub:** `github.com/angelica-oliv/mindfuldays-workshop`
  * 📱 **Guias Modulares:** Pastas `/pt` e `/es` com prompts prontos para copiar.
  * ❓ **Perguntas e Respostas (Q&A)**
* 🎙️ **Notas da Palestrante:**
  > *"Muito obrigada pela presença de todos neste workshop! Vocês têm todo o material disponível no repositório para recriar no próprio ritmo. Quais perguntas temos?"*
