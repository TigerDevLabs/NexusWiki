# Security Module

The Security module provides **BCrypt-based player authentication**, CAPTCHA anti-bot protection, session management, anti-duplication, and anti-lag tools — all designed for **offline/cracked servers**.

---

## Sub-systems

| Sub-system | Description |
| --- | --- |
| **Auth** | Register/login with BCrypt passwords, persistent sessions |
| **Anti-Bot** | IP rate-limiting, CAPTCHA map challenge, name blacklisting, VPN detection |
| **Mod Detection** | Plugin-channel scanner — kicks hacked clients, alerts staff on Forge/NeoForge |
| **Anti-Dupe** | Detects and prevents common item duplication exploits |
| **Anti-Lag** | Scheduled world cleaner, entity stacker |

---

## Authentication

Players on cracked servers must `/register` on first join and `/login` on subsequent joins. Premium accounts are verified via the Mojang API and bypass auth entirely.

### Commands

| Command | Usage | Permission |
| --- | --- | --- |
| `/register <password> <confirm>` | Register an account | *(all players)* |
| `/login <password>` | Log into your account | *(all players)* |
| `/changepassword <old> <new>` | Change password | *(authenticated)* |

### Auth Configuration (`security/auth.yml`)

```yaml
storage: sqlite           # sqlite | postgres

postgres:
  url: "jdbc:postgresql://localhost:5432/nexusslime"
  user: nexus
  password: changeme

session-timeout-minutes: 30      # Re-login required after 30min idle
persistent-session-hours: 2      # Auto-login within 2h of last session

max-failed-attempts: 5           # Lockout after 5 wrong passwords
lockout-minutes: 10

login-spawn:
  enabled: false                 # Teleport to lobby while unauthenticated
  world: world
  x: 0.0
  y: 64.0
  z: 0.0
```

---

## Anti-Bot

### How It Works

1. **Join rate limiter** — blocks IPs that join more than `max-joins` times within the time window
2. **Name blacklist** — regex patterns block bot-like usernames at login
3. **CAPTCHA** — new players receive a map with a random 5-char code they must type in chat
4. **Premium check** — premium (paid) accounts bypass CAPTCHA entirely
5. **VPN detection** — optional proxycheck.io / iphub.info integration
6. **Alt detection** — alerts admins when one IP has too many linked accounts

### Anti-Bot Configuration (`security/antibot.yml`)

```yaml
rate-limit:
  window-seconds: 10
  max-joins: 3

name-blacklist-patterns:
  - "[A-Za-z]{1,3}[0-9]{5,}"
  - "bot[0-9]+"
  - "^[0-9]+$"

vpn-detection:
  enabled: false
  api-url: "https://proxycheck.io/v2/{ip}?key={key}&vpn=1"
  api-key: ""
  cache-minutes: 60

captcha:
  enabled: true
  timeout-seconds: 60
  session-hours: 24            # Skip CAPTCHA for 24h after first pass

premium-check:
  enabled: true

alt-detection:
  max-accounts-per-ip: 3      # Alert admins if an IP has 3+ accounts
```

---

## Anti-Lag

### World Cleaner

Automatically removes old ground items and excess entities on a schedule.

### Command

| Command | Usage | Permission |
| --- | --- | --- |
| `/cleanworld` | Manually trigger a world clean | `nexusslime.security.cleanworld` |

### Anti-Lag Configuration (`security/antilag.yml`)

```yaml
cleaner:
  interval-seconds: 300        # Auto-clean every 5 minutes
  warn-seconds: 5              # Broadcast warning before cleaning
  item-age-ticks: 6000         # Remove items older than 5 minutes
  worlds:
    - world
    - world_nether
    - world_the_end
  entity-whitelist:
    - ARMOR_STAND
    - ITEM_FRAME

stacker:
  radius: 5.0                  # Merge mobs within 5 blocks
  max-stack: 50                # Max 50 mobs per stack
  entity-types:
    - COW
    - PIG
    - SHEEP
    - ZOMBIE
    - SKELETON
    - CREEPER
    - BLAZE
```

---

## Mod Detection

The mod detection system scans the **plugin-message channels** that clients register during the login handshake. This reveals the mod loader and specific mods being used.

### How It Works

- **Blacklisted channels** → player is kicked immediately and staff are notified (e.g. Wurst, Meteor Client, LiquidBounce)
- **Watch-list channels** → staff are notified but the player is **never kicked** (e.g. Forge, NeoForge — may be legitimate mod users)
- All channel registrations are stored per-player for the session; use `/modcheck <player>` to inspect them

### Configuration (`security/mods.yml`)

```yaml
mod-detector:
  enabled: true
  action: KICK           # LOG | NOTIFY | KICK (applies to blacklisted channels)
  notify-staff: true     # Always alert staff regardless of action
  kick-message: "§cYou are using a blacklisted modification."

  # Channels that trigger the configured action (kick by default)
  blacklisted-channels:
    - "wurst:*"
    - "meteor-client:*"
    - "impact:*"
    - "liquidbounce:*"
    - "aristois:*"
    - "labymod:*"
    - "hacked:*"
    - "cheat:*"

  # Watch-list: always notifies staff, NEVER kicks
  # Used for mod loaders that may be legitimate
  watch-channels:
    - "forge:*"
    - "fml:*"
    - "fmlhandshake:*"
    - "fmlnetworking:*"
    - "neoforge:*"
    - "FML|HS"
    - "FML|MP"
    - "FML"

  # Allowed channels (safe — logged for info only, no action)
  allowed-channels:
    - "minecraft:*"
    - "fabric:*"
    - "bungeecord:*"
    - "velocity:*"
```

### Pattern Syntax

| Pattern | Matches |
| --- | --- |
| `"wurst:*"` | Any channel whose namespace starts with `wurst:` |
| `"FML\|HS"` | Exact channel name `FML\|HS` (legacy Forge handshake) |

!!! tip "Forge / NeoForge"
    Forge and NeoForge users are put on the **watch-list**, not kicked. A `§e[ModWatch]` alert is sent to staff with the `nexusslime.security.notify` permission so they can manually verify whether the player is cheating.

### Staff Permissions for Mod Detection

| Permission | Description | Default |
| --- | --- | --- |
| `nexusslime.security.notify` | Receive mod-detection and watch-list alerts | OP |

---

## Anti-Dupe

Prevents common duplication exploits. Configuration in `security/antidupe.yml`.

```yaml
# security/antidupe.yml
enabled: true
log-attempts: true             # Log detected dupe attempts to console
alert-admins: true             # Notify online admins in-game
```

---

## Staff Commands

| Command | Usage | Permission |
| --- | --- | --- |
| `/vanish` | Toggle visibility | `nexusslime.staff.vanish` |
| `/vanish <player>` | Vanish another player | `nexusslime.staff.vanish.others` |
| `/invsee <player>` | Inspect a player's inventory | `nexusslime.staff.invsee` |
| `/spy` | Toggle chat spy mode | `nexusslime.staff.spy` |

---

## Permissions

| Permission | Description | Default |
| --- | --- | --- |
| `nexusslime.security.cleanworld` | Manual world clean | OP |
| `nexusslime.staff.vanish` | Vanish yourself | OP |
| `nexusslime.staff.vanish.others` | Vanish other players | OP |
| `nexusslime.staff.vanish.see` | See vanished players | OP |
| `nexusslime.staff.invsee` | Inspect inventories | OP |
| `nexusslime.staff.spy` | Chat spy mode | OP |

---

## PlaceholderAPI

| Placeholder | Description |
| --- | --- |
| `%nexusslime_authenticated%` | `true` / `false` — is the player logged in? |
| `%nexusslime_auth_status%` | Human-readable status (`Authenticated`, `Pending`) |
