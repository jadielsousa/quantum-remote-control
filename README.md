# 📱 Quantum Remote Control for Antigravity IDE

[![Versão](https://img.shields.io/badge/version-1.0.10-blue.svg)](package.json)
[![Licença](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Compatibilidade](https://img.shields.io/badge/IDE-Antigravity%20IDE-purple.svg)](https://antigravity.google)
[![Protocolo](https://img.shields.io/badge/comunicação-WebSockets%20%7C%20RPC-orange.svg)]()
[![Acesso Remoto](https://img.shields.io/badge/túnel-Cloudflare%20Tunnel-yellow.svg)]()

> **Controle remoto mobile em tempo real para o painel de agentes da Antigravity IDE.**  
> Interaja com seus agentes, responda a questionários interativos, aprove alterações de código e cancele execuções diretamente pelo seu smartphone, via rede local ou 4G/5G com túnel seguro.

---

## 🌐 Idiomas / Languages
- [🇧🇷 Português (Documentação Principal)](#-documentação-em-português)
- [🇺🇸 English (Summary & Architecture)](#-english-documentation)

---

# 🇧🇷 Documentação em Português

## 📋 Sumário
1. [Visão Geral](#-visão-geral)
2. [Principais Recursos](#-principais-recursos)
3. [Guia Rápido de Instalação e Uso](#-guia-rápido)
4. [Guia dos Recursos Mobile](#-guia-dos-recursos-mobile)
5. [Arquitetura do Sistema e Fluxo de Dados](#-arquitetura-do-sistema)
6. [Túnel Remoto com Cloudflare (4G/5G)](#-túnel-remoto-com-cloudflare)
7. [Configurações e Comandos](#-configurações-e-comandos)
8. [Segurança e Privacidade](#-segurança-e-privacidade)
9. [Solução de Problemas (FAQ)](#-solução-de-problemas-faq)

---

## 🔭 Visão Geral

O **Quantum Remote Control** transforma seu smartphone em uma central de comando remota para a **Antigravity IDE**. Você não precisa ficar preso em frente ao computador enquanto o agente executa tarefas demoradas, faz pesquisas na web ou implementa alterações no código.

Através de uma interface web responsiva moderna (SPA) com tema escuro e feedback tátil, você acompanha o fluxo de trabalho do agente em tempo real, responde a perguntas interativas com suporte a carrossel de múltiplas opções, aprova/rejeita ações e envia novos prompts com facilidade.

---

## ✨ Principais Recursos

- 📲 **Sem necessidade de instalar app nativo**: Funciona em qualquer navegador moderno (Chrome, Safari, Firefox) no iOS e Android.
- ⚡ **Sincronização Bidirecional Ultrarrápida**: Comunicação em tempo real via WebSockets locais de baixa latência.
- ❓ **Questionários Interativos (`ask_question`)**:
  - Carrossel inteligente com paginação (`← 1 de N →`).
  - Navegação entre perguntas com validação (`Continuar →` e `Submit ↵`).
  - Suporte a seleção única, múltipla escolha e escrita livre (*Other*).
  - Resolução direta no Language Server da IDE sem poluir o histórico do chat.
- 🛡️ **Aprovação e Rejeição de Passos**: Pílulas flutuantes para Aceitar (`antigravity.acceptAgentStep`) ou Rejeitar diffs/passos do agente com um toque.
- 🛑 **Parada de Emergência (Kill Switch)**: Botão de cancelamento rápido para interromper loops ou tarefas indesejadas do agente imediatamente.
- 💬 **Novo Chat / Nova Sessão**: Inicie uma conversa limpa (`antigravity.startNewConversation`) diretamente pelo celular.
- 🌐 **Acesso Externo Seguro via Cloudflare**: Integre o Cloudflare Tunnel para acessar seu agente de qualquer lugar do mundo (4G/5G) sem abrir portas no roteador ou configurar DDNS.
- 🔒 **Autenticação por Token HMAC/UUID**: Conexões protegidas por token único gerado por sessão com expiração e capacidade de regeneração instantânea.
- 📳 **Haptic Feedback**: Vibrações táteis no smartphone ao selecionar opções, avançar perguntas e enviar comandos.

---

## 🚀 Guia Rápido

### Passo 1: Instalar a Extensão
Instale o pacote `.vsix` na sua IDE Antigravity:
1. Abra a paleta de comandos (`Ctrl+Shift+P` ou `Cmd+Shift+P`).
2. Digite e selecione **Extensions: Install from VSIX...**.
3. Selecione o arquivo `quantum-remote-control-1.0.10.vsix`.

### Passo 2: Abrir o Painel de Controle
1. Na barra lateral de atividades da IDE (Activity Bar), clique no ícone do **Quantum Remote** (ou abra pelo menu lateral).
2. O painel exibirá o status do servidor, os endereços IP locais disponíveis e um **QR Code**.

### Passo 3: Conectar pelo Smartphone
1. Certifique-se de que o celular está conectado na **mesma rede Wi-Fi** do computador (ou utilize a opção de Túnel Cloudflare para acesso via 4G/5G).
2. Aponte a câmera do celular para o **QR Code** e toque no link gerado.
3. A interface do controle remoto se abrirá automaticamente autenticada e conectada!

---

## 📱 Guia dos Recursos Mobile

### 1. Carrossel de Questionários (`ask_question`)
Quando uma skill do agente (ex: `/idea-refine`) faz perguntas com opções:
- **Cabeçalho com Paginação**: O indicador `← X de Y →` permite navegar livremente entre as perguntas.
- **Opções Numeradas**: Toque na opção desejada. A opção recomendada pelo agente é destacada com o badge `(Recommended)`.
- **Opção Personalizada ("Other")**: Ao selecionar *Other*, um campo de texto se abre para você digitar sua resposta customizada.
- **Botão "Continuar →"**: Valida a resposta da pergunta atual e avança para a próxima no carrossel.
- **Botão "Submit ↵"**: Habilitado na última pergunta; envia o conjunto completo de respostas para o Language Server da IDE simultaneamente.
- **Botão "Skip"**: Pula a pergunta atual ou conclui o questionário ignorando as restantes.

### 2. Pílulas de Aprovação / Rejeição
Quando o agente solicita autorização para executar comandos no terminal ou aplicar diffs:
- Pílulas flutuantes verde (**Aprovar**) e vermelha (**Rejeitar**) aparecem no topo do chat.
- Ao tocar em **Aprovar**, a IDE executa o passo sem que você precise tocar no mouse ou teclado.

### 3. Barra de Ações Rápidas
- **Parar Agente (Botão Vermelho)**: Interrompe imediatamente o pensamento e a execução do agente na IDE.
- **Nova Conversa (+)**: Arquiva a sessão atual e inicia um novo tópico do zero.
- **Campo de Prompt**: Permite digitar qualquer instrução, comando slash (ex: `/plan`, `/debugger`) ou colar trechos de código.

---

## 🏗️ Arquitetura do Sistema

```mermaid
flowchart TD
    subgraph MobileDevice["📱 Smartphone (Navegador Mobile)"]
        UI["Mobile SPA (HTML5/CSS3/Vanilla JS)"]
        WSClient["Cliente WebSocket + Reconexão"]
        UI <--> WSClient
    end

    subgraph HostPC["💻 Computador do Desenvolvedor (Antigravity IDE)"]
        subgraph Extension["Quantum Remote Control Extension"]
            Server["Servidor HTTP / WebSocket (Porta 8080)"]
            Auth["Validador de Token (UUID/HMAC)"]
            Session["SessionStore (Armazenamento Local)"]
            Watcher["BrainWatcher (Leitor de transcript.jsonl)"]
            LSClient["Antigravity LS Client (gRPC/ConnectRPC)"]
            Tunnel["Cloudflare Tunnel Service (cloudflared)"]
        end

        subgraph IDECore["Núcleo da IDE Antigravity"]
            Panel["Agent Side Panel (Chat & UI)"]
            LS["Language Server Process (Porta HTTPS + CSRF)"]
            BrainLogs["Brain Logs (.system_generated/logs)"]
        end
    end

    subgraph Internet["🌐 Nuvem (Opcional)"]
        CF["Rede Cloudflare (Túnel HTTPS Seguro)"]
    end

    WSClient <-->|Rede Local (Wi-Fi)| Server
    WSClient <-->|4G/5G via Internet| CF
    CF <--> Tunnel
    Tunnel <--> Server

    Server --> Auth
    Auth --> Session
    Server <--> Watcher
    Watcher <-->|Monitora em tempo real| BrainLogs

    Server -->|Aprovar/Rejeitar/Parar| Panel
    Server <-->|HandleCascadeUserInteraction| LSClient
    LSClient <-->|RPC Direto HTTPS| LS
```

### Componentes Internos
1. **`RemoteServer`**: Servidor Express/Node integrado que serve o HTML da interface mobile e mantém o canal WebSocket com reconexão resiliente.
2. **`AntigravityLSClient`**: Comunica-se diretamente com o binário `language_server` local da IDE Antigravity através de chamadas ConnectRPC seguras (`HandleCascadeUserInteraction`, `GetCascadeTrajectory`, `SendUserCascadeMessage`).
3. **`BrainWatcher`**: Monitora de forma contínua o arquivo `transcript.jsonl` da sessão ativa no diretório `.gemini/antigravity-ide/brain`, transmitindo instantaneamente atualizações de pensamento, ferramentas utilizadas e respostas do agente para o mobile.
4. **`CloudflareTunnelService`**: Baixa e gerencia o processo `cloudflared` sob demanda para expor o servidor local em uma URL pública HTTPS temporária ou dedicada.

---

## ☁️ Túnel Remoto com Cloudflare

Se o seu smartphone estiver em uma rede móvel (4G/5G) ou em uma rede Wi-Fi diferente da do computador, você pode ativar o **Cloudflare Tunnel**:

1. Abra as Configurações da IDE (`Ctrl+,` ou `Cmd+,`).
2. Pesquise por `quantumRemote.useCloudflareTunnel` e marque a caixa de seleção como `true`.
3. Ao iniciar o servidor pelo painel, o binário do `cloudflared` será detectado/baixado automaticamente e uma URL segura (ex: `https://xxxx.trycloudflare.com`) será gerada.
4. O QR Code do painel lateral passará a apontar diretamente para essa URL segura com seu token de acesso.

> [!TIP]
> Você também pode usar um **Named Tunnel** próprio informando o seu `quantumRemote.cloudflareTunnelToken` e `quantumRemote.cloudflareCustomDomain` nas configurações.

---

## ⚙️ Configurações e Comandos

### Comandos Registrados (`Ctrl+Shift+P`)

| Comando | Descrição |
| :--- | :--- |
| `quantumRemote.startServer` | Inicia o servidor HTTP/WebSocket e abre o painel com QR Code. |
| `quantumRemote.stopServer` | Encerra o servidor e fecha todas as conexões ativas. |
| `quantumRemote.restartServer` | Reinicia o servidor e recarrega os adaptadores de rede. |
| `quantumRemote.regenerateToken` | Gera um novo token de segurança, invalidando acessos anteriores. |

### Configurações (`settings.json`)

| Configuração | Padrão | Descrição |
| :--- | :--- | :--- |
| `quantumRemote.port` | `8080` | Porta local na qual o servidor HTTP e WebSocket irá escutar. |
| `quantumRemote.autoStart` | `true` | Se `true`, inicia o servidor automaticamente ao abrir a IDE. |
| `quantumRemote.useCloudflareTunnel` | `false` | Se `true`, cria um túnel HTTPS público via Cloudflare. |
| `quantumRemote.cloudflareTunnelToken` | `""` | Token de autenticação para Named Tunnel próprio da Cloudflare. |
| `quantumRemote.cloudflareCustomDomain` | `""` | Domínio customizado associado ao túnel próprio. |

---

## 🔐 Segurança e Privacidade

- **Isolamento de Token**: O acesso ao endpoint HTTP e WebSocket exige um token único de 32 caracteres gerado criptograficamente.
- **Rede Local Padrão**: Por padrão, o servidor escuta apenas na interface local e na rede Wi-Fi privada do usuário.
- **Zero Vazamento de Dados**: Nenhum dado ou código do seu projeto é enviado para servidores de terceiros. Na modalidade com Cloudflare, o tráfego é criptografado ponta-a-ponta (TLS) entre o seu smartphone e a sua máquina.
- **Regeneração com 1 Clique**: Se você suspeitar que alguém na rede visualizou seu QR Code, basta clicar em **Regenerar Token** para desconectar todos os dispositivos imediatamente.

---

## ❓ Solução de Problemas (FAQ)

### O celular não conecta mesmo na mesma rede Wi-Fi
- **Firewall do Windows/Mac**: Verifique se a porta `8080` (ou a configurada) está liberada no Firewall do sistema operacional para conexões de entrada na rede privada.
- **Isolamento de Ponto de Acesso (AP Isolation)**: Alguns roteadores Wi-Fi impedem a comunicação direta entre dispositivos conectados. Nesses casos, ative a opção `quantumRemote.useCloudflareTunnel` nas configurações para conectar pela internet sem depender de roteamento local.

### O questionário ficou preso na tela da IDE?
- A partir da versão **1.0.10**, a extensão implementa resposta multi-pergunta com o esquema exato do Language Server (`HandleCascadeUserInteraction`). Certifique-se de estar utilizando a versão 1.0.10 ou superior.

---
---

# 🇺🇸 English Documentation

## 🔭 Overview

**Quantum Remote Control** turns your smartphone into a full-featured remote management console for the **Google Antigravity IDE** agent system. Free yourself from sitting at your desk while your autonomous AI agent researches, refactors, and implements complex workflows.

Using a responsive, modern dark-themed web app, you can monitor the agent's step-by-step thoughts, answer multi-step questionnaires, approve or reject code changes, and trigger emergency stops from your mobile device.

---

## ⚡ Key Features

- 📱 **Zero Install on Mobile**: Runs in modern mobile browsers (Safari, Chrome, Firefox) on both iOS and Android.
- ⚡ **Real-Time WebSocket Sync**: Instant mirroring of agent thoughts, tool execution, and transcript updates.
- ❓ **Interactive Questionnaire Carousel (`ask_question`)**:
  - Full multi-question pagination (`← 1 of N →`).
  - Validation steps with `Continue →` and batch `Submit ↵`.
  - Single-choice, multi-select, and custom "Other" write-in support.
  - Native Language Server RPC integration (no chat prompt pollution).
- 🛡️ **One-Tap Step Approval**: Floating pills to quickly Accept or Reject agent tool calls and diffs.
- 🛑 **Emergency Stop (Kill Switch)**: Cancel stuck or runaway agent tasks with one touch.
- 💬 **New Session Trigger**: Clear context and start a new conversation right from your phone.
- ☁️ **Built-in Cloudflare Tunnel**: Seamless remote access over 4G/5G without router port forwarding.
- 🔒 **Secure Token Authentication**: Protected by unique session tokens with one-click revocation.

---

## 🚀 Quickstart

1. **Install VSIX**: Press `Ctrl+Shift+P` -> `Extensions: Install from VSIX...` -> Select `quantum-remote-control-1.0.10.vsix`.
2. **Open Sidebar**: Click the **Quantum Remote** icon in the Activity Bar.
3. **Scan QR Code**: Connect your phone to the same Wi-Fi, scan the QR code with your camera, and start commanding your agent!

---

## ⚙️ Settings Reference

| Setting | Default | Description |
| :--- | :--- | :--- |
| `quantumRemote.port` | `8080` | Local port for the HTTP/WebSocket server. |
| `quantumRemote.autoStart` | `true` | Automatically starts the server when Antigravity IDE launches. |
| `quantumRemote.useCloudflareTunnel` | `false` | Enables a secure public HTTPS tunnel via Cloudflare for 4G/5G access. |
| `quantumRemote.cloudflareTunnelToken` | `""` | Optional Cloudflare Named Tunnel token. |
| `quantumRemote.cloudflareCustomDomain` | `""` | Custom domain mapped to your named tunnel. |

---

## 📄 License
This project is licensed under the [MIT License](LICENSE).
