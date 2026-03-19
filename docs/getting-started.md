# Getting Started

This page covers everything you need to install and configure NexusPrism on your server.

---

## Requirements

| Requirement | Version |
| --- | --- |
| Minecraft Server | Paper / Spigot 1.21+ |
| Java | 17 or newer |
| Soft dependency | PlaceholderAPI (recommended) |
| Soft dependency | LuckPerms (recommended) |
| Soft dependency | SkinsRestorer (optional) |

!!! warning "Cracked Server Notice"
    If your server runs in offline mode (cracked), the **Security module** auth system is mandatory. Premium accounts are detected automatically via the Mojang API and bypass the login screen.

---

## Installation

1. Download the latest `NexusPrism.jar` from the [GitHub Releases](https://github.com/O-Tiger/NexusPrism/releases) page.
2. Place the JAR in your server's `plugins/` folder.
3. Start the server once to generate all default configuration files.
4. Stop the server, edit the generated configs (see below), then restart.

```tree
plugins/
└── NexusPrism/
    ├── config.yml
    ├── items.yml
    ├── machines.yml
    ├── lang/
    │   ├── en_US.yml
    │   ├── pt_BR.yml
    │   └── ...
    ├── security/
    ├── clans/
    ├── economy/
    ├── discord/
    ├── votifier/
    └── ...
```

---

## Main Configuration (`config.yml`)

```yaml
settings:
  language: en_US         # en_US | pt_BR | es_ES | zh_CN
  debug: false
  auto-save-interval: 300 # seconds

database:
  type: SQLITE            # SQLITE or MYSQL

  mysql:                  # Only used when type: MYSQL
    host: localhost
    port: 3306
    database: nexusprism
    username: root
    password: password
    pool-size: 10

resourcepack:
  enabled: false
  url: ""
  sha1: ""
  force: false
  send-on-join: true

energy:
  enabled: true
  max-transfer: 1000
  loss-percentage: 5
  tick-rate: 20

machines:
  enabled: true
  max-per-chunk: 50
  tick-rate: 20
```

---

## Maven Modules

NexusPrism is a **multi-module Maven project**.
All modules are bundled into the final plugin JAR automatically.

| Module | Description |
| --- | --- |
| `nexusprism-api` | Public API — interfaces for addon developers |
| `nexusprism-core` | Core managers, PDC registry, language system |
| `nexusprism-items` | Data-driven custom item storage |
| `nexusprism-machines` | Machine definitions and processing engine |
| `nexusprism-systems` | Energy network implementation |
| `nexusprism-integrations` | PlaceholderAPI, LuckPerms, SkinsRestorer hooks |
| `nexusprism-storage` | SQLite / PostgreSQL data persistence |
| `nexusprism-gui` | GUI framework (menus and interfaces) |
| `nexusprism-utils` | Utility helpers |
| `nexusprism-web` | Webstore bridge, VIP kits, payment handling, GDPR |
| `nexusprism-plugin` | Main entry point, command handler |
| `nexusprism-discord` | JDA Discord bot, webhooks, account linking |
| `nexusprism-chat` | 4-channel chat system with moderation |
| `nexusprism-tab` | TAB list header/footer, scoreboards, MOTD |
| `nexusprism-ae` | ME (Applied Energistics-style) network storage |
| `nexusprism-energy` | Energy generators and cable networks |
| `nexusprism-waila` | WAILA/HUD tooltips |
| `nexusprism-security` | BCrypt auth, anti-bot, mod detection, anti-lag, anti-dupe |
| `nexusprism-clans` | Clans, territory claiming, upgrades, alliance system |
| `nexusprism-economy` | Money, credits, /sell, /baltop |
| `nexusprism-essentials` | 40+ QoL commands |
| `nexusprism-crystaldefense` | Wave-based Crystal Defense minigame |
| `nexusprism-custommobs` | YAML-defined custom bosses |
| `nexusprism-dreams` | Sleep cutscene system |
| `nexusprism-protections` | WorldGuard-style region protection, flags, duel system |
| `nexusprism-ss` | Silk Spawner support |
| `nexusprism-votifier` | Standalone Votifier V1/V2 server |
| `nexusprism-twitch` | Twitch integration (live alerts, giveaways) |
| `nexusprism-holograms` | YAML-driven floating text and item displays |
| `nexusprism-traits` | Tarot card trait system with economy integration |
| `nexusprism-rng` | Daily spin, lucky blocks, gacha, server events |
| `nexusprism-crates` | Key-based loot crates with animated openings |
| `nexusprism-enchantments` | 175 custom enchants across 6 rarities and 10 trigger types |
| `nexusprism-structures` | Custom loot injection for 11 vanilla structure types |

---

## Developer API (Jitpack)

Add NexusPrism as a dependency in your addon or plugin using [Jitpack](https://jitpack.io/#O-Tiger/NexusPrism).
Jitpack status badge: [![](https://jitpack.io/v/O-Tiger/NexusPrism.svg)](https://jitpack.io/#O-Tiger/NexusPrism)

!!! info "API-only dependency"
    Depend on `nexusprism-api`, not `nexusprism-plugin`, to avoid pulling the full implementation into your project. Mark it as `provided` — the plugin JAR is already on the server at runtime.

=== "Maven"

    ```xml
    <repositories>
        <repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
        </repository>
    </repositories>

    <dependencies>
        <dependency>
            <groupId>com.github.O-Tiger.NexusPrism</groupId>
            <artifactId>nexusprism-api</artifactId>
            <version>TAG</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

=== "Gradle (Kotlin DSL)"

    ```kotlin
    repositories {
        maven("https://jitpack.io")
    }

    dependencies {
        compileOnly("com.github.O-Tiger.NexusPrism:nexusprism-api:TAG")
    }
    ```

=== "Gradle (Groovy)"

    ```groovy
    repositories {
        maven { url 'https://jitpack.io' }
    }

    dependencies {
        compileOnly 'com.github.O-Tiger.NexusPrism:nexusprism-api:TAG'
    }
    ```

Replace `TAG` with the release version (e.g. `2.0.0-BETA`) or a commit hash for snapshots.

### `plugin.yml` dependency

Declare NexusPrism as a soft or hard dependency in your addon's `plugin.yml`:

```yaml
# Hard dependency — your plugin won't load without NexusPrism
depend: [NexusPrism]

# Soft dependency — loads after NexusPrism if present
softdepend: [NexusPrism]
```

### Using the API

```java
import io.github.otiger.nexusprism.api.NexusPrismAPI;
import io.github.otiger.nexusprism.api.items.NexusItem;

public class MyAddon extends JavaPlugin {

    @Override
    public void onEnable() {
        NexusPrismAPI api = NexusPrismAPI.getInstance();

        // Access the item registry
        api.getItemRegistry().getItem("COPPER_DUST").ifPresent(item -> {
            getLogger().info("Found item: " + item.getId());
        });

        // Check territory at a location
        api.getTerritoryRegistry().getTerritory(someLocation).ifPresent(territory -> {
            getLogger().info("Location owned by: " + territory.getOwner());
        });
    }
}
```

!!! tip "Uploading to Jitpack"
    Push a tagged release to GitHub, then visit `https://jitpack.io/#O-Tiger/NexusPrism` and click **Look up** next to your tag to trigger the build. Once green, the dependency is ready to use.

---

## First Steps After Install

1. **Set your language** in `config.yml` → `settings.language`
2. **Configure the Security module** (`security/auth.yml`) if running offline/cracked
3. **Configure the Economy module** (`economy/sell-prices.yml`) with your item prices
4. **Set up Discord** (`discord/config.yml`) with your bot token and channel IDs
5. **Set up Votifier** (`votifier/config.yml`) with your vote links and rewards
6. Give yourself `nexusprism.admin.*` or use LuckPerms to assign permission groups

!!! tip "Reload command"
    After changing any config file, run `/nexusprism reload` to apply changes without restarting.
