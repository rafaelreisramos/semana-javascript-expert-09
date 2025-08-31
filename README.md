<div align="center">

![JavaScript](https://img.shields.io/badge/Made%20with-JavaScript-yellow)
![Last Commit](https://img.shields.io/github/last-commit/rafaelreisramos/semana-javascript-expert-09)

# Chatbot Inteligente 100% Offline com Prompt API do Chrome

Construindo um widget de chatbot embarcado que roda totalmente no navegador, explorando os recursos experimentais de AI locais da Chrome Prompt API.

</div>

---

## 📚 Sumário

- [Semana JS Expert 09](#-semana-js-expert-09)
- [Preview](#-preview)
- [Objetivo](#-objetivo)
- [Recursos Principais](#-recursos-principais)
- [Arquitetura e Estrutura do Widget](#-arquitetura-e-estrutura-do-widget)
- [Pré-requisitos](#-pré-requisitos)
- [Instalação Rápida](#-instalação-rápida)
- [Embutindo o Widget em Outro Site](#-embutindo-o-widget-em-outro-site)
- [Customização](#-customização)
- [Limitações e Avisos](#-limitações-e-avisos)
- [FAQ](#-faq)
- [Referências](#-referências)

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
- Verificar se o seu dispositívo é compatível:
  - [chrome://on-device-internals](chrome://on-device-internals): em `Model Status -> Foundational model criteria` a propriedade `device capable` deve ter uma valor `true`.
- Carregar o modelo pela primeira vez através do console do browser usando o código a seguir. O modelo tem cerca de 4GB e estará disponível quando a resposta for `available`.

```js
setInterval(async () => console.log(await LanguageModel.availability()), 500)

const ai = await LanguageModel.create({
  expectedInputLanguages: ['pt'],
  monitor(m) {
    m.addEventListener('downloadprogress', (e) => {
      console.log(`Downloaded ${e.loaded * 100}%`)
    })
  },
})
```

- Gerar o arquivo `llms.txt` e colocar na diretório raiz do projeto. Uma opção para gerar este arquivo é usar o site [Wordlift](https://wordlift.io/generate-llms-txt/). Você pode revisar o arquivo final e também adicionar textos e faqs para facilitar a interpretação da inteligência artificial.

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

<!--## ⚠️ Limitações e Avisos-->
<h2 id="-limitações-e-avisos">⚠️ Limitações e Avisos</h2>

- As Chrome AI / Prompt APIs ainda são experimentais e podem mudar ou exigir flags.
- Recursos offline dependem do suporte do navegador / hardware local.
- Este projeto é educacional – não destina-se a produção sem revisões de segurança.

## ❓ FAQ

**Funciona em Firefox / Safari?** Atualmente o foco é Chrome (APIs experimentais específicas).

**Preciso de servidor backend?** Não para o núcleo demonstrado; tudo roda no cliente.

**Como altero o prompt inicial?** Edite `botData/systemPrompt.txt`.

## Desafios adicionais

<ol>
  <li>Baixar o modelo mediante à autorização dos usuários</li>
  <ul>
    <li>Pergunte ao usuário se ele deseja baixar o modelo, verificar que se caso o modelo não esteja disponível na máquina do cliente, para que no chat, ele clique em um botão, inicie o download e então o notifique que acabou.</li>
    <li>verificar que se caso o modelo não esteja disponível na máquina do cliente, para que no chat, ele clique em um botão, inicie o download e então o notifique que acabou</li>
  </ul>
  <li>Tornar disponível em outros navegadores</li>
  Se o cliente não está no Google Chrome, você pode trocar o modelo, usar o Hugging face ou até o modelo do Gemma do google e seguir o mesmo processo, perguntando se ele deseja baixar o modelo.

  <li>Tornar disponível em computadores incompatíveis / com menos poder de processamento</li>
  Implementar um backend para consumir as APIs gratuitas de AI, os modelos menores do Gemma do Google para responder aos usuários:
    <ul>
      <li>Recomendação é usar o <a href='https://openrouter.ai/'>OpenRouter</a>, um agregador de modelos de IA que funcionam na nuvem. Lá lá eles deixam você usar APIs de forma gratuita, com alguns limites mas pelos meus testes funciona muito bem.</li>
      <li>Dar uma olhada na <a href=https://openrouter.ai/docs/community/open-ai-sdk>documentação</a> para ver como integrar com o Node.js e garantir que suas chaves não vão ficar expostas no frontend.</li>
    </ul>
</ol>

## 📚 Referências

- [Consenso entre navegadores sobre a PromptAPI](https://chromestatus.com/feature/5134603979063296?_gl=1*8vjss6*_ga*ODUwNTYyMjczLjE3NTYyMTMxMjg.*_ga_37GXT4VGQK*czE3NTYyMTUyMjYkbzIkZzEkdDE3NTYyMTU0OTckajQ0JGwwJGgw)
- [Web Agents na Web com Jason Meyes](https://x.com/jason_mayes?lang=en&_gl=1*1n48vxk*_ga*ODUwNTYyMjczLjE3NTYyMTMxMjg.*_ga_37GXT4VGQK*czE3NTYyMTUyMjYkbzIkZzEkdDE3NTYyMTU0OTckajQ0JGwwJGgw)
- [Hugging face](https://huggingface.co/webml-community?_gl=1*rnrlo3*_ga*ODUwNTYyMjczLjE3NTYyMTMxMjg.*_ga_37GXT4VGQK*czE3NTYyMTUyMjYkbzIkZzEkdDE3NTYyMTU0OTckajQ0JGwwJGgw)
- [Text to Speech no navegador](https://x.com/jason_mayes?lang=en&_gl=1*1n48vxk*_ga*ODUwNTYyMjczLjE3NTYyMTMxMjg.*_ga_37GXT4VGQK*czE3NTYyMTUyMjYkbzIkZzEkdDE3NTYyMTU0OTckajQ0JGwwJGgw)
- [DeepSeek no Navegador](https://huggingface.co/spaces/webml-community/deepseek-r1-webgpu?_gl=1*1n71wse*_ga*ODUwNTYyMjczLjE3NTYyMTMxMjg.*_ga_37GXT4VGQK*czE3NTYyMTUyMjYkbzIkZzEkdDE3NTYyMTU0OTckajQ0JGwwJGgw)
- [APIs de Web AI no Chrome](https://developer.chrome.com/docs/ai/built-in?hl=pt-br&_gl=1*1n71wse*_ga*ODUwNTYyMjczLjE3NTYyMTMxMjg.*_ga_37GXT4VGQK*czE3NTYyMTUyMjYkbzIkZzEkdDE3NTYyMTU0OTckajQ0JGwwJGgw)
- [Web AI demos](https://chrome.dev/web-ai-demos/?_gl=1*1n71wse*_ga*ODUwNTYyMjczLjE3NTYyMTMxMjg.*_ga_37GXT4VGQK*czE3NTYyMTUyMjYkbzIkZzEkdDE3NTYyMTU0OTckajQ0JGwwJGgw)
- [Build a local and offline-capable chatbot with WebLLM](https://web.dev/articles/ai-chatbot-webllm)
- [Jason Mayes WebAIAgent GitHub repository](https://github.com/jasonmayes/WebAIAgent)
- [Google Chrome Built-in AI Challenge](https://googlechromeai.devpost.com/?linkId=11071015)
- [Google Chrome Built-in AI Challenge Winners](https://developer.chrome.com/blog/ai-challenge-winners)
- [Google Chrome Built-in AI Challenge Projects Gallery](https://googlechromeai.devpost.com/project-gallery)
- [Chrome for Developers Blog](https://developer.chrome.com/blog)

---

Feito com 💜 durante a Semana JS Expert 09.
