<div align="center">

![JavaScript](https://img.shields.io/badge/Made%20with-JavaScript-yellow)
![Last Commit](https://img.shields.io/github/last-commit/ErickWendel/semana-javascript-expert09)

# Chatbot Inteligente 100% Offline com Prompt API do Chrome

Construindo um widget de chatbot embarcado que roda totalmente no navegador, explorando os recursos experimentais de AI locais da Chrome Prompt API.

</div>

---

## 📚 Sumário

- [Semana JS Expert 09](#-semana-js-expert-09)
- [Preview](#-preview)
- [Objetivo](#-objetivo)
- [Recursos Principais](#-recursos-principais)
- [Arquitetura e Estrutura](#-arquitetura-e-estrutura)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação Rápida](#-instalação-rápida)
- [Executando](#-executando)
- [Embutindo o Widget em Outro Site](#-embutindo-o-widget-em-outro-site)
- [Customização](#-customização)
- [Limitações e Avisos](#-limitações-e-avisos)
- [Roadmap / Próximos Passos](#-roadmap--próximos-passos)
- [FAQ](#-faq)

---

## 📢 Semana JS Expert 09

Este repositório faz parte da **Semana JS Expert 09**, evento gratuito ministrado entre **25/08/2025 e 31/08/2025**.

---

## 🎥 Preview

<img width="100%" src="./assets/output.gif" alt="Preview do chatbot em funcionamento" />

---

## 🎯 Objetivo

Aprender, de forma prática, como criar um chatbot que usa **modelos de IA locais / embarcados** via recursos experimentais do Chrome, sem depender de um backend externo. Você terá um widget reutilizável que pode ser plugado em qualquer página.

## 🚀 Recursos Principais

- 100% offline (sem chamadas para servidores – ideal para protótipos e privacidade).
- API moderna do Chrome (Prompt API / AI APIs experimentais).
- Arquitetura simples com separação entre Controller, View e Services.
- Suporte a mensagens streaming simuladas / indicador de digitação.
- Fácil de estilizar via CSS custom properties.
- Preparado para abortar requisições (ex: botão Stop nas aulas avançadas).

## 🧱 Arquitetura e Estrutura do Widget

```

sdk/
    ew-chatbot.html      # Snippet para embutir
    ew-chatbot.css       # Estilos e variáveis CSS
    src/
        index.js           # Bootstrapping
        controllers/chatBotController.js
        views/chatBotView.js
        services/promptService.js (adapta chamadas de IA)
    botData/
        systemPrompt.txt
        chatbot-config.json
        avatar.webp
```

- Cada aula possui evolução incremental (ex: abortar requests, streaming, melhorias UX...).

## ✅ Pré-requisitos

- Node.js 22+ (para scripts utilitários e servidor estático simples).
- Navegador **Chrome** (versão compatível com as AI / Prompt APIs experimentais).
- Habilitar flags experimentais:
  - [chrome://flags/#prompt-api-for-gemini-nano](chrome://flags/#prompt-api-for-gemini-nano)

## ⚡ Instalação Rápida

Clone o repositório e instale as dependências dentro da pasta desejada.

Exemplo:

```bash
git clone https://github.com/rafaelreisramos/semana-javascript-expert-09.git

cd semana-javascript-expert-09

npm ci
npm start
```

E então interaja pelo widget no canto da tela.

## 🔌 Embutindo o Widget em Outro Site

Crie a pasta `botData` no projeto em que queira embutir o widget e customize `botData/chatbot-config.json` para alterar nome, avatar e cores.

Você publicar os arquivos da pasta `sdk/` na Web (um cdn talvez) e referenciar o arquivo, algo como:

```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>EW Academy AI Chatbot</title>
    <link rel="icon" type="image/x-icon" href="./botData/avatar.webp" />
  </head>

  <body>
    <script type="module" src="https://SEU_CDN/chatbot/src/index.js"></script>
  </body>
</html>
```

E então o widget aparecerá automaticamente na inicialização na página.

## 🎨 Customização

Conteúdo inicial / comportamento:

- `systemPrompt.txt`: instruções de sistema para o modelo.
- `chatbot-config.json`: metadados (nome, avatar, cores, welcomeBubble etc).

## ⚠️ Limitações e Avisos

- As Chrome AI / Prompt APIs ainda são experimentais e podem mudar ou exigir flags.
- Recursos offline dependem do suporte do navegador / hardware local.
- Este projeto é educacional – não destina-se a produção sem revisões de segurança.

## ❓ FAQ

**Funciona em Firefox / Safari?** Atualmente o foco é Chrome (APIs experimentais específicas).

**Preciso de servidor backend?** Não para o núcleo demonstrado; tudo roda no cliente.

**Como altero o prompt inicial?** Edite `botData/systemPrompt.txt`.

---

Feito com 💜 durante a Semana JS Expert 09.
