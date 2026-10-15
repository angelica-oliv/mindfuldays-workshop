# 🧘 MindfulDays — App de Meditação e Mindfulness do Zero com IA

> 🌐 **Idiomas:** 🇧🇷 **Português** | 🇪🇸 **[Español (Perú)](../es/README.md)**

Bem-vindo ao repositório oficial do workshop **MindfulDays**! Este treinamento prático foi estruturado para guiar desenvolvedores passo a passo na criação de um aplicativo Android moderno e funcional, unindo prototipagem assistida por Inteligência Artificial e desenvolvimento de ponta com **Jetpack Compose** e **Android Studio (versão Stable)**.

---

## 🎯 Objetivo do Workshop

Construir do zero um aplicativo completo de mindfulness focado na exibição diária de reflexões baseadas nas **9 Atitudes de Mindfulness de Jon Kabat-Zinn**, integrado à **Gemini API** para geração de conselhos personalizados e equipado com um **Timer de Meditação** intuitivo.

Neste workshop, os participantes aprenderão a:
1. Prototipar a interface gráfica e extrair tokens de design usando o **[Google Stitch](https://stitch.withgoogle.com/)**.
2. Criar a estrutura do projeto com assistentes de IA diretamente na versão **Stable do Android Studio**.
3. Padronizar o contexto para agentes de IA com **AGENTS.md** e construir interfaces declarativas com **Jetpack Compose** e **Material Design 3**.
4. Integrar chamadas dinâmicas de IA generativa com **Gemini**.
5. Configurar suítes de testes e pipelines automatizados de CI/CD via **GitHub Actions**.

---

## 📱 Visão Geral do App *MindfulDays*

* **Card da Atitude do Dia**: Apresenta diariamente uma das 9 atitudes de mindfulness (ex: *Aceitação*, *Mente de Principiante*, *Paciência*) com rotação cíclica automática baseada na data do sistema.
* **Reflexão com Gemini API**: Botão para gerar conselhos e meditações guiadas em tempo real via IA generativa.
* **Timer de Meditação**: Contador circular minimalista de foco com controles de Play, Pause e Reset, além de emissão de sinal sonoro suave ao término.
* **Configurações & Notificações**: Opção de agendamento de lembretes diários para manter a prática.
* **Internacionalização (i18n)**: Suporte nativo a Português, Inglês e Espanhol.
* **Suporte a Dark Mode**: Tema escuro integrado com Material Design 3 e alto contraste.

---

## 🛠️ Pré-requisitos Técnicos

Antes de iniciar os módulos práticos, certifique-se de ter os seguintes softwares instalados e contas configuradas:

* **Android Studio**: Versão **Stable** mais recente (ex: Ladybug, Jellyfish ou superior).
* **JDK**: Java Development Kit 17 ou superior.
* **Chave de API do Gemini**: Obtenha gratuitamente uma API Key no [Google AI Studio](https://aistudio.google.com/).
* **Conta no [Google Stitch](https://stitch.withgoogle.com/) / Figma**: Para geração e inspeção de protótipos visuais.
* **Git & Conta no GitHub**: Para versionamento de código e acompanhamento das branches.

---

## 📂 Módulos do Workshop (Guia Passo a Passo)

Siga os arquivos `.md` na sequência proposta para concluir o workshop:

1. [**`01-design-ui-stitch.md`**](./01-design-ui-stitch.md) — *Passo 1: Prototipagem Visual, Sitemap e Design System no Google Stitch (Modo Claro & Escuro)*
2. [**`02-setup-android-studio-ai.md`**](./02-setup-android-studio-ai.md) — *Passo 2: Configuração do Android Studio Stable e Inicialização com Create with AI*
3. [**`03-implementacao-compose-e-logica.md`**](./03-implementacao-compose-e-logica.md) — *Passo 3: Diretrizes com AGENTS.md, Interface em Jetpack Compose, Suporte Dual-Theme, 9 Atitudes e Gemini API*
4. [**`04-qualidade-testes-cicd.md`**](./04-qualidade-testes-cicd.md) — *Passo 4: Qualidade de Software, Testes com IA e Robot Pattern (+ Passos Opcionais: Ícone do App com IA e Publicação na Play Store)*

---

## 🎨 Paleta de Cores do Projeto (Material Design 3)

| Token M3 | Modo Claro (Light) | Modo Escuro (Dark) | Descrição |
| :--- | :--- | :--- | :--- |
| **Primary** | `#6B8E23` (Verde Sálvia) | `#A8C673` (Sálvia Luminoso) | Destaques e botões principais |
| **Primary Container** | `#8FA853` (Sálvia Claro) | `#2E4239` (Floresta Noturno Elevado) | Contêineres de destaque |
| **Secondary** | `#E8DFD8` (Areia Muted) | `#A3B5A8` (Sálvia Muted Suave) | Elementos secundários |
| **Background** | `#FBF9F5` (Off-White Calmo) | `#15201A` (Floresta Noturno Profundo) | Fundo da tela inteira |
| **Surface** | `#FFFFFF` (Branco Puro) | `#22322A` (Floresta Noturno Elevado) | Fundo de cards elevados |
| **OnSurface / Text** | `#2C3E35` (Verde Floresta) | `#F1EFEA` (Off-White Claro) | Textos e títulos de alto contraste |

---

## 📄 Licença

Este material é disponibilizado sob a licença MIT. Sinta-se à vontade para utilizar e adaptar para suas palestras e workshops.
