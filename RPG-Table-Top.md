# 🎲 Road to Valhalla — Plataforma de RPG de Mesa Virtual

<div align="center">

![RPG Banner](https://img.shields.io/badge/Road%20to%20Valhalla-RPG%20Virtual-blue?style=for-the-badge&logo=d-and-d&logoColor=white)
![Status](https://img.shields.io/badge/Status-Alpha-blueviolet?style=for-the-badge)
![Node](https://img.shields.io/badge/Node.js-v18+-green?style=for-the-badge&logo=node.js)
![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge)

**Uma plataforma completa de RPG de mesa virtual com engine 2D em Phaser 3, batalhas por turno, fichas customizáveis, cutscenes, fog of war e muito mais.**

[✨ Funcionalidades](#-funcionalidades) • [🛠️ Tecnologias](#️-tecnologias) • [🚀 Instalação](#-instalação) • [📖 Uso](#-uso) • [🗺️ Roadmap](#️-roadmap)

</div>

---

## 🎯 Sobre o Projeto

O **Road to Valhalla** é uma plataforma web de RPG de mesa virtual, pensada para mestres e jogadores que querem uma experiência imersiva online. A aplicação combina uma engine de jogo 2D (Phaser 3) com um servidor em tempo real (WebSocket), entregando mapas com períodos do dia, fog of war, personagens com sprites animados no padrão LPC, sistema de batalha por turnos, fichas de personagem com editor visual de 30+ tipos de campo, cutscenes com timeline, inventário com moedas, e um painel de mestre completo — tudo rodando no navegador.

### Por que usar?

- ✅ **Open Source e gratuito** — sem assinatura, sem paywall
- ✅ **Multiplayer em tempo real** — WebSocket nativo com sincronização instantânea
- ✅ **Engine de jogo 2D** — Phaser 3 com sprites animados, colisão e câmera dinâmica
- ✅ **Sistema agnóstico** — funciona com D&D, Tormenta, Call of Cthulhu ou qualquer sistema via fichas customizáveis
- ✅ **Internacionalizado** — 11 idiomas (PT, EN, ES, FR, DE, IT, JA, KO, RU, ZH)
- ✅ **Auto-hospedável** — rode no seu próprio servidor com Node.js + MySQL

---

## ✨ Funcionalidades

### 🗺️ Mapas e Exploração

- **Mapas com períodos do dia** — cada mapa possui variações visuais para Dia, Tarde e Noite (background, telhados, portas), trocáveis em tempo real pelo mestre
- **Colisão por imagem** — limites de colisão definidos por máscara PNG para formas orgânicas
- **Portas interativas** — teleporte entre mapas com spawn points configuráveis
- **Oclusão e Y-sorting** — telhados e paredes fatiados em strips com profundidade dinâmica (OcclusionManager), jogadores intercalados corretamente entre estruturas
- **Fog of War** — névoa de guerra com iluminação dinâmica por personagem (radial ou cone direcional), luz ambiente configurável por mapa, gradientes pré-computados em cache
- **Objetos interativos** — baús, alavancas e outros objetos com máquina de estados (estados JSON + transições), iluminação própria
- **Upload de mapas** — armazenamento via MinIO/S3 com proxy integrado para CORS
- **Escala e velocidade por mapa** — `char_scale` e `char_speed` configuráveis individualmente

### 🧙 Personagens e NPCs

- **Múltiplos personagens por jogador** — cada jogador pode ter vários personagens, com flag `is_current` para trocar
- **Stats D&D** — STR, DEX, CON, INT, WIS, CHA com persistência completa
- **Sprites LPC** — suporte nativo a spritesheets no padrão Liberated Pixel Cup (13 animações × 4 direções) + sprites customizados com configuração JSON
- **Criador de Sprites LPC** — editor integrado no painel admin para composição de sprites
- **NPCs com 6 tipos** — friendly (verde), neutral (amarelo), hostile (vermelho), quest (ciano), shop (magenta), decoration
- **Padrões de movimento** — NPCs com rotas configuráveis (mover, esperar, animar, virar) com loop e velocidade customizável
- **Sistema de diálogo** — árvore de diálogos com opções de resposta e ações (next, goto, close, dice_roll, message)
- **Interação por proximidade** — detecção de alcance com `interaction_range` configurável
- **Iluminação por entidade** — personagens e NPCs podem emitir luz (radial/cone) para o fog of war

### ⚔️ Sistema de Batalha por Turnos

- **Templates de batalha** — editor dedicado (Battle Editor) com posicionamento de NPCs e jogadores no mapa, overlay e câmera configuráveis
- **Instâncias com estados** — preparing, active, paused, finished
- **Ordem de iniciativa** — rolagem automática com bônus, turnos ordenáveis por drag-and-drop pelo mestre
- **Ações por turno** — 1 movimento + 1 ação por turno, com extras concedíveis pelo mestre
- **Ataques e HP** — sistema de dano com HP bars visuais sobre os sprites, sincronização bidirecional com fichas de personagem
- **Indicadores visuais** — círculo pulsante no participante ativo, círculos de alcance de movimento e ataque, barra de iniciativa no HUD
- **Battle Log** — registro completo de todas as ações da batalha
- **11 eventos WebSocket** — start, end_turn, reorder, set_turn, grant_extra, move, attack, end, sync, consume_move, consume_action

### 📜 Fichas de Personagem

- **Editor visual drag-and-drop** — posicionamento livre com seções, campos e elementos decorativos
- **30+ tipos de campo** — text, number, modifier, skill (com rolagem D20), attack, spell, hp_bar, mp_bar, checkbox, select, roll_button, calculated (fórmulas), currency (ouro/prata/cobre), listas dinâmicas (ataques, magias, equipamentos, habilidades)
- **Elementos visuais** — title_text, paragraph_text, styled_label, background_image, logo_image, decorative_image, shape_box, shape_circle, icon_display, linhas, bordas decorativas (celtic, medieval, ornate)
- **Sistema de fórmulas** — campos calculados que referenciam outros campos da ficha
- **Rolagem integrada** — botões de rolagem em skills e ataques que resolvem fórmulas com variáveis da ficha, enviando resultados com dados 3D para o chat
- **Histórico de rolagens** — log completo com detecção de critical e fumble
- **Fichas de NPC** — mesma estrutura das fichas de personagem, aplicável a NPCs
- **Templates por sistema RPG** — catálogo de sistemas (D&D, etc.) com template padrão por mesa
- **Sincronia de HP** — HP da ficha ↔ personagem ↔ batalha ativa sincronizados automaticamente

### 🎬 Sistema de Cutscenes

- **Editor com timeline** — interface inspirada no CapCut com régua temporal, playhead arrastável e zoom (Ctrl+Scroll)
- **Tracks por NPC** — cada NPC possui uma trilha independente na timeline com ações sequenciais
- **6 tipos de ação** — mover (por tiles), esperar, animar, virar, diálogo (balão), visibilidade
- **Track de câmera** — keyframes com posição, zoom e easing (Linear, Quad, Cubic, Sine, Back)
- **Preview inline** — playback completo no editor com barras cinematográficas e restauração de estado
- **Transição de mapa** — troca automática de mapa ao final da cutscene com spawn point configurável
- **Auto-save** — salvamento automático com debounce de 2s e indicador visual de status
- **Playback in-game** — CutscenePlayer.js integrado ao MapScene com controles via WebSocket (start/pause/resume/stop)

### 🎒 Inventário e Economia

- **Mochilas** — cada jogador possui mochila(s) com peso máximo e slots configuráveis
- **Itens com atributos** — tipo, raridade (5 níveis), slot de equipamento (10 slots), peso, atributos JSON
- **Ações de item** — equipar, usar, largar com registro de transações
- **Sistema monetário** — 3 moedas (cobre, prata, ouro) com transações registradas
- **Notificações em tempo real** — itens e dinheiro recebidos via WebSocket

### 💬 Chat e Dados

- **Chat por mesa** — mensagens persistidas com tipos: message, roll, system, whisper
- **Chat de lobby** — 3 salas fixas (Taverna, Praça, Guilda) in-memory
- **Formatação Markdown** — bold, italic, underline, strikethrough, code, blockquote, imagens com modal
- **Sintaxe de dados** — `{2d6}`, `{1d20+5}`, `{low(4d6)}`, `{high(3d8)}` + referências a campos da ficha
- **Dados 3D** — visualização com física (@3d-dice/dice-box) com 30+ colorsets, materiais e texturas configuráveis pelo mestre
- **Cards de rolagem** — estilo Roll20 com fórmula, resultado individual, soma e badges de critical/fumble
- **Histórico persistente** — todas as mensagens e rolagens salvas no banco

### 🏰 Painel do Mestre

- **Visão do jogo** — iframe do jogo com controles integrados via postMessage
- **Modo espectador** — mestre entra como fantasma invisível com câmera livre (WASD + Q/E zoom)
- **Controle de sessão** — pausar/continuar, trocar período do dia, trocar mapa para todos os jogadores
- **Gerenciamento completo** — jogadores, mapas (upload + configuração), personagens, NPCs, itens, fichas (templates + instâncias), convites, handouts, objetos interativos, cutscenes, batalhas, configurações da mesa
- **Handouts** — upload e broadcast de imagens, PDFs, áudio e vídeo (até 100MB)
- **Convites** — códigos com max_uses e expiração configuráveis

### 👤 Perfis e Social

- **Perfil público** — slug personalizado, avatar, banner, bio
- **Sistema social** — followers/following entre usuários
- **Sistemas favoritos** — catálogo de sistemas RPG com favoritos por usuário
- **Dashboard** — resumo de mesas, criação rápida, stats do usuário

### 🔐 Autenticação e Administração

- **Registro e login** — bcrypt + sessões com cookies
- **Reset de senha** — via email (SMTP/Nodemailer)
- **Roles** — owner, master, admin, player, spectator
- **Super Admin** — painel com stats globais, gerenciamento de usuários/mesas, analytics, feedback

### 🌐 Internacionalização

11 idiomas suportados: **Português** (principal), Inglês, Espanhol, Francês, Alemão, Italiano, Japonês, Coreano, Russo, Chinês

---

## 🛠️ Tecnologias

### Backend
| Tecnologia | Uso |
|---|---|
| **Node.js** | Runtime JavaScript |
| **Express.js** | Framework web (ambos servidores) |
| **Socket.IO** | WebSocket — servidor legado |
| **ws** | WebSocket nativo — servidor de jogo (new-rpg) |
| **Prisma** | ORM para MySQL |
| **MySQL** | Banco de dados relacional (57 modelos) |
| **MinIO** | Object storage S3-compatible (mapas, sprites, handouts) |
| **bcryptjs** | Hash de senhas |
| **Nodemailer** | Envio de emails (reset senha) |
| **Multer** | Upload de arquivos |
| **PM2** | Process manager em produção |

### Frontend
| Tecnologia | Uso |
|---|---|
| **Phaser 3** | Engine de jogo 2D (mapas, sprites, animações, câmera, colisão) |
| **@3d-dice/dice-box** | Dados 3D com física |
| **SweetAlert2** | Dialogs e modais |
| **Font Awesome 6** | Ícones |
| **HTML5 / CSS3 / ES6+** | Interface customizada (sem frameworks UI) |

### Infraestrutura
| Tecnologia | Uso |
|---|---|
| **PM2** | Gerenciamento de processos (cluster mode) |
| **Nginx** | Reverse proxy |
| **Linux** | Servidor de produção |
| **Git** | Controle de versão |

---

## 📐 Arquitetura

O projeto opera com **dois servidores coexistentes** acessando o mesmo banco MySQL:

```
┌─────────────────────────────────────────────────────────────┐
│                        NGINX                                 │
│  roadtovalhalla.com.br → :8083 (Legacy)                     │
│  rpgdev.bigbridge.com.br → :3084 (New-RPG)                 │
└──────────────┬───────────────────────┬──────────────────────┘
               │                       │
    ┌──────────▼──────────┐  ┌────────▼────────────┐
    │   server.js (Legacy) │  │  new-rpg/server/    │
    │   Express + Socket.IO│  │  Express + ws       │
    │   Auth, Admin, API   │  │  Game engine server │
    │   Uploads, Routes    │  │  Battle, Sheets,    │
    │                      │  │  Chat, Cutscenes    │
    └──────────┬───────────┘  └────────┬────────────┘
               │                       │
               └───────┬───────────────┘
                       │
              ┌────────▼────────┐
              │  MySQL (Prisma)  │
              │  57 modelos      │
              └────────┬────────┘
                       │
              ┌────────▼────────┐
              │  MinIO (S3)      │
              │  Assets storage  │
              └─────────────────┘
```

### Cenas Phaser (Cliente)
`LoginScene` → `LobbyScene` → `TableSelectScene` → `MapScene` (jogo principal)

Módulos do MapScene: `BattleManager`, `FogOfWarManager`, `OcclusionManager`, `CutscenePlayer`

---

## 🚀 Instalação

### Pré-requisitos

- Node.js v18+
- MySQL 8.0+
- MinIO ou AWS S3
- Git

### Setup

1. **Clone o repositório**
```bash
git clone <repo-url>
cd rpg-road-to-valhalla
```

2. **Instale as dependências**
```bash
npm install
cd new-rpg && npm install && cd ..
```

3. **Configure o banco de dados**

Configure a conexão MySQL em `config/database.js` e gere o client Prisma:
```bash
cd new-rpg
npx prisma generate
# Execute as migrations em ordem:
# prisma/migrations/001_init.sql até 014_npc_sheets.sql
cd ..
```

4. **Configure o MinIO/S3**

Edite `config/minio.js` com suas credenciais:
```javascript
const minioClient = new Minio.Client({
    endPoint: 'seu-endpoint.com',
    port: 9000,
    useSSL: true,
    accessKey: 'SUA_ACCESS_KEY',
    secretKey: 'SUA_SECRET_KEY'
});
```

5. **Inicie os servidores**
```bash
# Desenvolvimento
node server.js                    # Servidor legado (auth + admin + API)
cd new-rpg && node server/index.js  # Servidor de jogo (WebSocket + game logic)

# Produção (PM2)
pm2 start server.js --name rpg
pm2 start new-rpg/ecosystem.config.cjs
pm2 save
```

---

## 📖 Uso

### Controles do Jogador

| Ação | Desktop | Mobile |
|---|---|---|
| Mover | `WASD` ou setas | Joystick virtual |
| Chat | `Enter` | Botão 💬 |
| Interagir com NPC | `Espaço` (quando próximo) | Tap no NPC |
| Ficha do personagem | `C` | Botão na HUD |
| Inventário | Botão 🎒 | Botão 🎒 |

### Controles do Mestre (Modo Espectador)

| Ação | Tecla |
|---|---|
| Mover câmera | `WASD` |
| Zoom in/out | `Q` / `E` |
| Interagir com NPC | `Espaço` |

### Sintaxe de Dados no Chat

```
{1d20}          → rola 1d20
{2d6+3}         → rola 2d6 e soma 3
{low(4d6)}      → rola 4d6, pega o menor
{high(3d8)}     → rola 3d8, pega o maior
[field@nome]    → referência a campo da ficha
[mod@str]       → modificador de STR da ficha
```

---

## 📂 Estrutura do Projeto

```
├── server.js                  # Servidor legado (auth, admin, API, uploads)
├── new-rpg/
│   ├── server/
│   │   ├── index.js           # Servidor de jogo (WebSocket, REST)
│   │   ├── database.js        # Prisma client
│   │   └── services/
│   │       ├── mapService.js      # Mapas, estado do jogo, assets
│   │       ├── battleService.js   # Batalhas, turnos, ataques
│   │       └── sheetService.js    # Fichas, templates, rolagens
│   ├── prisma/
│   │   ├── schema.prisma      # 57 modelos
│   │   └── migrations/        # 14 migrations
│   └── public/
│       └── js/
│           ├── main.js                # Bootstrap Phaser
│           ├── websocket.js           # Gerenciamento WS
│           ├── BattleManager.js       # Batalha (HP bars, turnos, overlay)
│           ├── FogOfWarManager.js     # Fog of War (radial/cone)
│           ├── OcclusionManager.js    # Y-sorting de telhados
│           ├── CutscenePlayer.js      # Playback de cutscenes
│           ├── chatParser.js          # Parser de chat + dados
│           └── scenes/                # 8 cenas Phaser
├── admin.html                 # Painel do mestre (14 seções)
├── dashboard.html             # Dashboard do jogador
├── jogo-new.html              # Página do jogo (HUD + Master Panel + Phaser)
├── battle-editor.html         # Editor de templates de batalha
├── cutscene-editor.html       # Editor de cutscenes (timeline)
├── css/                       # Estilos customizados
├── js/                        # Scripts legados e utilitários
├── i18n/locales/              # 11 idiomas
└── config/                    # Database, MinIO, Table Manager
```

---

## 🗺️ Roadmap

### ✅ Implementado (Alpha)

- [x] Autenticação completa (registro, login, reset senha, sessões)
- [x] Perfis públicos com sistema social (follows)
- [x] Dashboard com gerenciamento de mesas
- [x] Mesas com membros, roles e convites
- [x] Mapas com 3 períodos do dia + colisão + portas
- [x] Fog of War com iluminação dinâmica (radial/cone)
- [x] Oclusão Y-sorting de telhados e paredes
- [x] Personagens com sprites LPC animados (13 animações × 4 direções)
- [x] Criador de sprites LPC integrado
- [x] NPCs com 6 tipos, rotas de movimento e diálogos
- [x] Fichas de personagem com editor visual (30+ tipos de campo)
- [x] Fichas de NPC
- [x] Sistema de batalha por turnos completo
- [x] Editor de batalhas (Battle Editor)
- [x] Inventário com mochilas, itens e moedas
- [x] Chat em tempo real com dados 3D
- [x] Cutscenes com editor timeline + playback in-game
- [x] Objetos interativos com máquina de estados
- [x] Handouts (imagens, PDF, áudio, vídeo)
- [x] Painel do mestre (14 seções de gerenciamento)
- [x] Modo espectador para mestres
- [x] Internacionalização (11 idiomas)
- [x] Super Admin com analytics
- [x] Upload de assets via MinIO/S3

### 🚧 Em Desenvolvimento

- [ ] Unificação dos dois servidores (legado + new-rpg)
- [ ] Sistema de quests
- [ ] Loja de NPCs (ação `open_shop` nos diálogos)
- [ ] Sistema de níveis/XP

### 📋 Planejado

- [ ] Som ambiente e música por mapa
- [ ] Voice chat integrado
- [ ] Marketplace de templates de fichas
- [ ] App mobile nativo
- [ ] Sistema de plugins/extensões

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Para contribuir:

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/NovaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/NovaFeature`)
5. Abra um Pull Request

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

<div align="center">

**⭐ Se você gostou deste projeto, considere dar uma estrela no GitHub! ⭐**

Feito com ❤️ para a comunidade RPG

[⬆ Voltar ao topo](#-road-to-valhalla--plataforma-de-rpg-de-mesa-virtual)

</div>