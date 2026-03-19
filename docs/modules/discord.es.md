# Módulo Discord

El módulo Discord proporciona un **bot impulsado por JDA** con puente de chat Minecraft ↔ Discord, vinculación de cuentas de jugadores, sincronización de roles, entrega por webhooks y monitoreo de GitHub Actions.

---

## Funcionalidades

| Funcionalidad | Descripción |
| --- | --- |
| **Puente de Chat** | Retransmite el chat del juego a canales de Discord y viceversa |
| **Vinculación de Cuentas** | Vincula cuentas de Discord a cuentas de Minecraft vía DM |
| **Sincronización de Roles** | Asigna roles de Discord basados en grupos de LuckPerms |
| **Webhooks** | Envía eventos de jugadores (entrada, muerte, logro) a Discord |
| **Alertas de Mención** | Notifica a los jugadores en el juego cuando son mencionados en Discord |
| **GitHub Actions** | Monitorea y activa flujos de CI/CD desde Discord |

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/discord` | Muestra el enlace de invitación de Discord | *(todos los jugadores)* |
| `/discord link` | Inicia el proceso de vinculación de cuenta | *(todos los jugadores)* |
| `/discord unlink` | Desvincula tu cuenta de Discord | *(todos los jugadores)* |
| `/discord info` | Muestra tu cuenta de Discord vinculada | *(todos los jugadores)* |
| `/discordrr` | Administra mensajes de reacción-rol | `nexusprism.admin` |

---

## Configuración

### 1. Crear un Bot en Discord

1. Ve a [discord.com/developers/applications](https://discord.com/developers/applications)
2. Crea una nueva Aplicación → Bot
3. Copia el **Token del Bot**
4. Activa **Message Content Intent** y **Server Members Intent**
5. Invita el bot a tu servidor con los alcances `bot` + `applications.commands`

### 2. Configurar el Bot (`discord/config.yml`)

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

### 3. Configurar Ajustes del Bot (`discord/bot.yml`)

```yaml
token: "YOUR_BOT_TOKEN_HERE"
guild-id: "YOUR_GUILD_ID"

# IDs de canales para el puente
channels:
  global-chat: "CHANNEL_ID"
  announcements: "CHANNEL_ID"
  staff: "CHANNEL_ID"
```

### 4. Configurar Canales (`discord/channels.yml`)

```yaml
# Mapea canales de chat del juego a IDs de canales de Discord
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

## Webhooks de Eventos de Jugadores (`discord/playerEvents.yml`)

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

## Mapeo de Roles (`discord/roles.yml`)

```yaml
# Grupo de LuckPerms → ID de Rol de Discord
mappings:
  vip: "DISCORD_ROLE_ID"
  mvp: "DISCORD_ROLE_ID"
  staff: "DISCORD_ROLE_ID"
  admin: "DISCORD_ROLE_ID"
```

---

## Webhooks de Salida (`discord/outbound.yml`)

```yaml
webhooks:
  default: "https://discord.com/api/webhooks/..."
  deaths: "https://discord.com/api/webhooks/..."
  votes: "https://discord.com/api/webhooks/..."
```

---

## Integración con Tienda (`discord/webstore.yml`)

```yaml
enabled: true
webhook: "https://discord.com/api/webhooks/..."
message: "**{player}** just purchased **{package}** from the store! Thank you!"
```

---

## Integración con GitHub Actions

El módulo Discord puede monitorear flujos de trabajo de GitHub Actions y permitir que el staff los active desde Discord.

Clases principales: `GitHubActionsManager`, `WorkflowPoller`, `WorkflowTriggerRecord`

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.discord.link` | Vincular cuenta de Discord | true |
| `nexusprism.admin` | Comandos administrativos de Discord | OP |
