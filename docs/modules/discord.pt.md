# Módulo Discord

O módulo Discord fornece um **bot com JDA** com ponte de chat Minecraft ↔ Discord, vinculação de contas de jogadores, sincronização de cargos, entrega por webhooks e monitoramento de GitHub Actions.

---

## Funcionalidades

| Funcionalidade | Descrição |
| --- | --- |
| **Ponte de Chat** | Retransmite o chat do jogo para canais do Discord e vice-versa |
| **Vinculação de Contas** | Vincula contas do Discord a contas do Minecraft via DM |
| **Sincronização de Cargos** | Atribui cargos do Discord com base nos grupos do LuckPerms |
| **Webhooks** | Envia eventos de jogadores (entrada, morte, conquista) para o Discord |
| **Alertas de Menção** | Notifica jogadores no jogo quando são mencionados no Discord |
| **GitHub Actions** | Monitora e aciona fluxos de CI/CD a partir do Discord |

---

## Comandos

| Comando | Uso | Permissão |
| --- | --- | --- |
| `/discord` | Exibe o link de convite do Discord | *(todos os jogadores)* |
| `/discord link` | Inicia o processo de vinculação de conta | *(todos os jogadores)* |
| `/discord unlink` | Desvincula sua conta do Discord | *(todos os jogadores)* |
| `/discord info` | Exibe sua conta do Discord vinculada | *(todos os jogadores)* |
| `/discordrr` | Gerencia mensagens de reação-cargo | `nexusprism.admin` |

---

## Configuração

### 1. Criar um Bot no Discord

1. Acesse [discord.com/developers/applications](https://discord.com/developers/applications)
2. Crie uma nova Aplicação → Bot
3. Copie o **Token do Bot**
4. Ative **Message Content Intent** e **Server Members Intent**
5. Convide o bot para o seu servidor com os escopos `bot` + `applications.commands`

### 2. Configurar o Bot (`discord/config.yml`)

```yaml
enabled: true

default-webhook: "https://discord.com/api/webhooks/YOUR_WEBHOOK_URL"

admin:
  enabled: false
  port: 8765
  token: ""

mentions:
  style: actionbar           # chat | actionbar | bossbar
  message: "&e&l[Discord] &b{sender} &7mentioned you!"
  bossbar:
    color: YELLOW
    duration: 5

bot:
  enabled: true
```

### 3. Configurar Definições do Bot (`discord/bot.yml`)

```yaml
token: "YOUR_BOT_TOKEN_HERE"
guild-id: "YOUR_GUILD_ID"

# IDs de canais para a ponte
channels:
  global-chat: "CHANNEL_ID"
  announcements: "CHANNEL_ID"
  staff: "CHANNEL_ID"
```

### 4. Configurar Canais (`discord/channels.yml`)

```yaml
# Mapeia canais de chat do jogo para IDs de canais do Discord
global:
  discord-id: "123456789012345678"
  webhook: "https://discord.com/api/webhooks/..."
  relay-to-game: true
  relay-to-discord: true

staff:
  discord-id: "123456789012345679"
  relay-to-game: true
  relay-to-discord: true
```

---

## Webhooks de Eventos de Jogadores (`discord/playerEvents.yml`)

```yaml
join:
  enabled: true
  webhook: "https://discord.com/api/webhooks/..."
  message: "**{player}** joined the server!"

quit:
  enabled: true
  webhook: "https://discord.com/api/webhooks/..."
  message: "**{player}** left the server."

death:
  enabled: true
  webhook: "https://discord.com/api/webhooks/..."
  message: "**{player}** died: {death_message}"

achievement:
  enabled: true
  webhook: "https://discord.com/api/webhooks/..."
  message: "**{player}** earned **{achievement}**!"
```

---

## Mapeamento de Cargos (`discord/roles.yml`)

```yaml
# Grupo do LuckPerms → ID de Cargo do Discord
mappings:
  vip: "DISCORD_ROLE_ID"
  mvp: "DISCORD_ROLE_ID"
  staff: "DISCORD_ROLE_ID"
  admin: "DISCORD_ROLE_ID"
```

---

## Webhooks de Saída (`discord/outbound.yml`)

```yaml
webhooks:
  default: "https://discord.com/api/webhooks/..."
  deaths: "https://discord.com/api/webhooks/..."
  votes: "https://discord.com/api/webhooks/..."
```

---

## Integração com Loja (`discord/webstore.yml`)

```yaml
enabled: true
webhook: "https://discord.com/api/webhooks/..."
message: "**{player}** just purchased **{package}** from the store! Thank you!"
```

---

## Integração com GitHub Actions

O módulo Discord pode monitorar fluxos de trabalho do GitHub Actions e permitir que a equipe os acione a partir do Discord.

Classes principais: `GitHubActionsManager`, `WorkflowPoller`, `WorkflowTriggerRecord`

---

## Permissões

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.discord.link` | Vincular conta do Discord | true |
| `nexusprism.admin` | Comandos administrativos do Discord | OP |
