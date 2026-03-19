# Módulo de Integración Twitch

El módulo Twitch conecta tu servidor Minecraft a Twitch. Los jugadores pueden **vincular sus cuentas de Twitch**, el staff es notificado cuando jugadores vinculados se ponen en directo, el chat de Twitch se retransmite en el juego y los admins pueden realizar **sorteos para espectadores**.

---

## Funcionalidades

| Funcionalidad | Descripción |
| --- | --- |
| **Vinculación de Cuentas** | Vincula Minecraft ↔ Twitch mediante un código de verificación en el chat |
| **Etiqueta [LIVE]** | Prefija el chat con `[LIVE]` cuando un jugador está transmitiendo |
| **Anuncios de Directo** | Anuncia cuando un jugador vinculado inicia/termina una transmisión |
| **Retransmisión de Chat** | Los mensajes del chat de Twitch aparecen en el juego |
| **Sorteos** | Selecciona aleatoriamente un espectador vinculado elegible y lo recompensa |
| **Recompensas para Espectadores** | Sorteo periódico automático para espectadores viendo streamers vinculados |

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/twitch link <usuario>` | Iniciar vinculación de cuenta Twitch | `nexusprism.twitch.use` |
| `/twitch unlink` | Desvincular cuenta Twitch | `nexusprism.twitch.use` |
| `/twitch status` | Verificar estado de vinculación | `nexusprism.twitch.use` |
| `/twitch approve <jugador>` | Aprobar una vinculación pendiente | `nexusprism.twitch.staff` |
| `/twitch reject <jugador>` | Rechazar una vinculación pendiente | `nexusprism.twitch.staff` |
| `/twitch pending` | Listar solicitudes de vinculación pendientes | `nexusprism.twitch.staff` |
| `/twitch giveaway <streamer>` | Realizar un sorteo | `nexusprism.twitch.staff` |
| `/twitch reload` | Recargar configuración de Twitch | `nexusprism.twitch.admin` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.twitch.use` | Comandos básicos de Twitch | true |
| `nexusprism.twitch.staff` | Aprobar vinculaciones, realizar sorteos | OP |
| `nexusprism.twitch.admin` | Recargar configuración | OP |

---

## Configuración

### 1. Crear una Aplicación de Twitch

1. Ve a [dev.twitch.tv/console](https://dev.twitch.tv/console) y crea una aplicación
2. Establece el redireccionamiento OAuth como `http://localhost`
3. Copia el **Client ID** y el **Client Secret**

### 2. Crear una Cuenta de Bot

1. Crea una cuenta Twitch para el bot (o usa la tuya propia)
2. Ve a [twitchapps.com/tmi/](https://twitchapps.com/tmi/) para obtener un token OAuth
3. Añade el bot como moderador en tu canal de verificación

### 3. Configurar (`twitch/config.yml`)

```yaml
bot:
  enabled: true
  oauth-token: "oauth:your_token_here"
  client-id: "your_client_id"
  client-secret: "your_client_secret"
  bot-username: "your_bot_account"
  verification-channel: "your_server_twitch_channel"

link:
  require-staff-approval: true  # El staff debe aprobar antes de que la vinculación se active
  code-expiry-seconds: 300

stream-poll:
  interval-seconds: 60          # Comprobar si los streamers están en directo cada 60s

live-tag:
  enabled: true
  format: "§c[LIVE] §r"         # Prefijado al formato de chat al transmitir

announcements:
  go-live:
    enabled: true
    message: "§6[Twitch] §e{player} §7is now live! §f{title} §7— §fttwitch.tv/{channel}"
    discord-channel: "announcements"   # Clave de canal de Discord para publicación cruzada
  go-offline:
    enabled: false
    message: "§6[Twitch] §e{player} §7finished their stream."

chat-relay:
  enabled: true
  format: "§6[Twitch] §b{user}§7: {message}"

giveaway:
  command: "crates key give {player} VOTE 1"
  key-item: "SERVER_KEY"
  active-viewer-window-minutes: 10
  announce-winner: "§6[Giveaway] §e{player} §7won a key! Congrats to @{twitch_name}!"
  twitch-announce: "Congrats @{twitch_name}! You won a key on our Minecraft server!"

viewer-reward:
  enabled: false
  interval-minutes: 30
  command: "crates key give {player} VOTE 1"
```

---

## Flujo de Vinculación de Cuenta

```cs
El jugador ejecuta /twitch link <usuario>
        │
        ▼
El bot envía un código de 5 caracteres en el canal Twitch de verificación
        │
        ▼
El jugador escribe !verify <código> en el chat de Twitch
        │
        ▼
[Si require-staff-approval: true]
El staff aprueba con /twitch approve <jugador>
        │
        ▼
Vinculación activa — etiqueta en directo y anuncios se aplican
```

---

## Sistema de Sorteos

El staff puede ejecutar `/twitch giveaway <streamer>` para:

1. Obtener todos los espectadores vinculados viendo el canal de ese streamer
2. Filtrar espectadores que enviaron un mensaje en los últimos `active-viewer-window-minutes`
3. Seleccionar aleatoriamente un espectador elegible
4. Ejecutar el `command` configurado (o dar el `key-item`) al ganador
5. Anunciar al ganador en el juego y en el chat de Twitch

!!! note "Permisos de Bot Requeridos"
    Para que el sistema de recompensas para espectadores obtenga la lista de chatters, la cuenta del bot debe tener el alcance OAuth `moderator:read:chatters` y ser moderador en el canal del streamer.

---

## Placeholders de Mensajes

| Placeholder | Descripción |
| --- | --- |
| `{player}` | Nombre de usuario de Minecraft |
| `{twitch_name}` | Nombre de visualización de Twitch |
| `{title}` | Título de la transmisión |
| `{channel}` | Nombre del canal de Twitch |
| `{user}` | Nombre de visualización del espectador en Twitch |
| `{message}` | Contenido del mensaje en el chat de Twitch |
