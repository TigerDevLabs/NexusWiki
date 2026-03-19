# Discord Module

The Discord module provides a **JDA-powered bot** with Minecraft ↔ Discord chat bridging, player account linking, role synchronization, webhook delivery, and GitHub Actions monitoring.

---

## Features

| Feature | Description |
| --- | --- |
| **Chat Bridge** | Relay in-game chat to Discord channels and vice versa |
| **Account Linking** | Link Discord accounts to Minecraft accounts via DM |
| **Role Sync** | Assign Discord roles based on LuckPerms groups |
| **Webhooks** | Push player events (join, death, achievement) to Discord |
| **Mention Alerts** | Notify in-game players when mentioned on Discord |
| **GitHub Actions** | Monitor and trigger CI/CD workflows from Discord |

---

## Commands

| Command | Usage | Permission |
| --- | --- | --- |
| `/discord` | Show Discord invite link | *(all players)* |
| `/discord link` | Start account linking process | *(all players)* |
| `/discord unlink` | Unlink your Discord account | *(all players)* |
| `/discord info` | Show your linked Discord account | *(all players)* |
| `/discordrr` | Manage reaction-role messages | `nexusprism.admin` |

---

## Setup

### 1. Create a Discord Bot

1. Go to [discord.com/developers/applications](https://discord.com/developers/applications)
2. Create a new Application → Bot
3. Copy the **Bot Token**
4. Enable **Message Content Intent** and **Server Members Intent**
5. Invite the bot to your server with `bot` + `applications.commands` scopes

### 2. Configure the Bot (`discord/config.yml`)

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

### 3. Configure Bot Settings (`discord/bot.yml`)

```yaml
token: "YOUR_BOT_TOKEN_HERE"
guild-id: "YOUR_GUILD_ID"

# Channel IDs for bridging
channels:
  global-chat: "CHANNEL_ID"
  announcements: "CHANNEL_ID"
  staff: "CHANNEL_ID"
```

### 4. Configure Channels (`discord/channels.yml`)

```yaml
# Map in-game chat channels to Discord channel IDs
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

## Player Event Webhooks (`discord/playerEvents.yml`)

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

## Role Mappings (`discord/roles.yml`)

```yaml
# LuckPerms group → Discord Role ID
mappings:
  vip: "DISCORD_ROLE_ID"
  mvp: "DISCORD_ROLE_ID"
  staff: "DISCORD_ROLE_ID"
  admin: "DISCORD_ROLE_ID"
```

---

## Outbound Webhooks (`discord/outbound.yml`)

```yaml
webhooks:
  default: "https://discord.com/api/webhooks/..."
  deaths: "https://discord.com/api/webhooks/..."
  votes: "https://discord.com/api/webhooks/..."
```

---

## Webstore Integration (`discord/webstore.yml`)

```yaml
enabled: true
webhook: "https://discord.com/api/webhooks/..."
message: "**{player}** just purchased **{package}** from the store! Thank you!"
```

---

## GitHub Actions Integration

The Discord module can monitor GitHub Actions workflows and allow staff to trigger them from Discord.

Key classes: `GitHubActionsManager`, `WorkflowPoller`, `WorkflowTriggerRecord`

---

## Permissions

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.discord.link` | Link Discord account | true |
| `nexusprism.admin` | Admin Discord commands | OP |
