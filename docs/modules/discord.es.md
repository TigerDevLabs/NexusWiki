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
| **Voto del Servidor** | Votación comunitaria para reiniciar el servidor vía slash command |
| **Control del Panel** | Comandos admin de inicio/parada vía API de Pterodactyl |

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

## Voto del Servidor y Control del Panel

### `/server vote` — Votación Comunitaria

Cualquier miembro de Discord (opcionalmente restringido a roles específicos) puede iniciar una votación para reiniciar el servidor.

1. El miembro ejecuta `/server vote` en Discord.
2. El bot publica un embed con botones **✅ Sí** y **❌ No**.
3. Cada miembro puede cambiar su voto durante la ventana de votación.
4. Al cerrar la ventana, el bot evalúa el resultado:
   - Requiere `min-votes` votos **y** `threshold`% de sí para aprobar.
   - Si aprueba: RCON transmite aviso en el juego, luego Pterodactyl envía señal `restart` tras `warn-seconds`.
   - Si falla: el embed se actualiza con el resultado, no se toma ninguna acción.
5. Un cooldown configurable impide votaciones consecutivas.

### `/server start` / `/server stop` — Comandos Admin

Restringido a roles listados en `server-vote.admin-roles` (o permiso de Administrador de Discord si la lista está vacía).

| Slash Command Discord | Acción |
| --- | --- |
| `/server vote` | Iniciar votación comunitaria de reinicio |
| `/server start` | Enviar señal `start` a Pterodactyl |
| `/server stop` | Transmitir aviso RCON y enviar señal `stop` |

### Configuración — `discord/panel.yml`

```yaml
panel: pterodactyl

pterodactyl:
  base-url: "https://panel.example.com"
  client-api-key: ""
  server-uuid: ""

rcon:
  host: "127.0.0.1"
  port: 25575
  password: ""
  timeout-seconds: 5

server-vote:
  enabled: true
  voter-roles: []
  admin-roles: []
  min-votes: 3
  threshold: 0.6
  window-seconds: 120
  cooldown-minutes: 30
  warn-seconds: 60
  channel: "default"
```

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.discord.link` | Vincular cuenta de Discord | true |
| `nexusprism.admin` | Comandos administrativos de Discord | OP |
