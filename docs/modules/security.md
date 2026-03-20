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
  url: "jdbc:postgresql://localhost:5432/nexusprism"
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

### Premium Verification

When `premium-check.enabled` is `true`, NexusPrism validates premium accounts using a two-step process so cracked players cannot impersonate paid accounts:

1. **UUID version check** — offline-mode servers assign version-3 UUIDs to all players. A genuine premium player authenticated via FastLogin/JPremium receives their real Mojang UUID (version 4). Version 3 = cracked, immediately rejected.
2. **Mojang API comparison** — even for version-4 UUIDs, the name is looked up via `api.mojang.com` and the returned UUID is compared against the player's actual UUID. Any mismatch is flagged as an impersonation attempt and the player is treated as cracked.

#### Cache & Resilience

Results are cached to avoid hammering the Mojang API on every join:

| Layer | Detail |
| --- | --- |
| **In-memory cache** | 24-hour TTL; cleared on restart |
| **SQLite persistent cache** | Survives restarts — file: `security/premium-cache.db` |
| **Rate limiter** | Max 50 Mojang API calls per 10-minute window |
| **Exponential backoff** | Backs off up to 60 s on repeated API failures |
| **Fallback** | Uses last cached result when the API is unreachable |

If the Mojang API is down, the system falls back gracefully to cached data. If no cache exists for the player, they are treated as cracked.

!!! warning "Impersonation detection"
    If a player connects with a version-3 (offline) UUID but the cache shows that username owns a Mojang account, a warning is logged: `IMPERSONATION DETECTED`. The player is still allowed in but is treated as cracked (must `/login`).

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
| `/cleanworld` | Manually trigger a world clean | `nexusprism.security.cleanworld` |

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
    Forge and NeoForge users are put on the **watch-list**, not kicked. A `§e[ModWatch]` alert is sent to staff with the `nexusprism.security.notify` permission so they can manually verify whether the player is cheating.

### Staff Permissions for Mod Detection

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.security.notify` | Receive mod-detection and watch-list alerts | OP |

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
| `/vanish` | Toggle visibility | `nexusprism.staff.vanish` |
| `/vanish <player>` | Vanish another player | `nexusprism.staff.vanish.others` |
| `/invsee <player>` | Inspect a player's inventory | `nexusprism.staff.invsee` |
| `/spy` | Toggle chat spy mode | `nexusprism.staff.spy` |

---

## Permissions

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.security.cleanworld` | Manual world clean | OP |
| `nexusprism.staff.vanish` | Vanish yourself | OP |
| `nexusprism.staff.vanish.others` | Vanish other players | OP |
| `nexusprism.staff.vanish.see` | See vanished players | OP |
| `nexusprism.staff.invsee` | Inspect inventories | OP |
| `nexusprism.staff.spy` | Chat spy mode | OP |

---

## Leveled Mobs

Every hostile mob that spawns in the world is automatically assigned a **level** that scales with how dangerous the environment is. Higher-level mobs deal more damage, have more health, and drop more XP.

### Level Roll Table

Levels are rolled at spawn based on Y-height, dimension, and biome. Bonuses stack.

| Condition | Level Range / Bonus |
| --- | --- |
| Y > 64 (surface) | Lv. 1–4 |
| Y ≤ 64 | Lv. 3–6 |
| Y ≤ 30 | Lv. 5–8 |
| Y ≤ 0 (deep underground) | Lv. 8–12 |
| Nether dimension | +3 to roll |
| The End dimension | +4 to roll |
| Deep Dark biome | +5 to roll |
| Blood Moon active | +2 to all rolls |

All results are clamped to `[1, max-level]` from config.

### Name Format

| Situation | Display Name |
| --- | --- |
| Stacked + leveled | `3x [Lv.5] Zombie` |
| Single + leveled | `[Lv.5] Zombie` |
| Level 1 (any stack) | `3x Zombie` *(no level tag)* |

### Stat Formulas

| Stat | Formula |
| --- | --- |
| **Damage** | `baseDamage × (1 + (level-1) × damageMultiplierPerLevel) × stackCount` |
| **XP** | `baseXP × stackCount × (1 + (level-1) × xpMultiplierPerLevel)` |
| **Health** | Scaled by `healthMultiplierPerLevel` per level above 1 |

### Configuration (`security/antilag.yml`)

```yaml
leveled-mobs:
  enabled: true
  max-level: 20
  xp-multiplier-per-level: 0.20      # +20% XP per level above 1
  damage-multiplier-per-level: 0.15  # +15% damage per level above 1
  health-multiplier-per-level: 0.10  # +10% health per level above 1
```

!!! note "Blood Moon Integration"
    When the **Blood Moon** is active (see the [Events module](events.md)), all level rolls receive a **+2 bonus**, making surface mobs significantly more dangerous at night.

---

## PlaceholderAPI

| Placeholder | Description |
| --- | --- |
| `%nexusprism_authenticated%` | `true` / `false` — is the player logged in? |
| `%nexusprism_auth_status%` | Human-readable status (`Authenticated`, `Pending`) |
