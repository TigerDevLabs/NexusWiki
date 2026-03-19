# NexusPrism Developer API

This guide walks through integrating with NexusPrism from an external Bukkit/Paper plugin or a native addon JAR. You only ever compile against `nexusprism-api` — never against concrete module JARs.

---

## Step 1 — Add the dependency

NexusPrism is published through **JitPack**. Add the repository and the API artifact to your `pom.xml`:

```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>

<dependencies>
    <dependency>
        <groupId>com.github.O-Tiger.NexusPrismModularizado</groupId>
        <artifactId>nexusprism-api</artifactId>
        <version>master-SNAPSHOT</version> <!-- or a specific commit hash -->
        <scope>provided</scope>
    </dependency>
</dependencies>
```

> **`provided` scope is required.** NexusPrism ships the API at runtime — do not shade it into your JAR.

For Gradle (Kotlin DSL):

```kotlin
repositories {
    maven("https://jitpack.io")
}

dependencies {
    compileOnly("com.github.O-Tiger.NexusPrismModularizado:nexusprism-api:master-SNAPSHOT")
}
```

---

## Step 2 — Declare the dependency in `plugin.yml`

Because NexusPrism is optional for most integrations, use `softdepend`. Use `depend` only if your plugin cannot function at all without it.

```yaml
name: MyPlugin
version: 1.0.0
main: com.example.MyPlugin
api-version: "1.21"

softdepend:
  - NexusPrism
```

---

## Step 3 — Get the API instance

Always obtain the API inside `onEnable()`, **after** the server is fully started (or listen for `ServerLoadEvent`). Never call it from a static initializer or constructor.

```java
import io.github.otiger.nexusprism.api.NexusPrismAPI;

public class MyPlugin extends JavaPlugin {

    private NexusPrismAPI nexus;

    @Override
    public void onEnable() {
        nexus = NexusPrismAPI.get();

        if (nexus == null) {
            getLogger().warning("NexusPrism not found — integration disabled.");
            return;
        }

        if (!nexus.isReady()) {
            // NexusPrism loaded but hasn't finished startup yet
            // Listen to ServerLoadEvent or use Bukkit.getScheduler().runTaskLater(...)
            getLogger().warning("NexusPrism is still starting up.");
            return;
        }

        getLogger().info("Hooked into NexusPrism " + nexus.getVersion());
    }
}
```

---

## Step 4 — Module providers

Each optional NexusPrism module exposes a typed provider through a static registry. All providers return `Optional` — if the module is disabled or not installed, the Optional is empty. Always use `ifPresent` or `orElse` to handle this safely.

### Economy

```java
import io.github.otiger.nexusprism.api.NexusPrismAPI;

UUID uuid = player.getUniqueId();

// Read balance
double balance = NexusPrismAPI.economy()
        .map(eco -> eco.getBalance(uuid))
        .orElse(0.0);

// Add money
NexusPrismAPI.economy().ifPresent(eco -> eco.addMoney(uuid, 500.0));

// Charge player (returns false if insufficient funds)
boolean success = NexusPrismAPI.economy()
        .map(eco -> eco.withdrawMoney(uuid, 100.0))
        .orElse(false);

// Top balances
NexusPrismAPI.economy().ifPresent(eco -> {
    eco.getTopBalances(10).forEach(entry ->
        System.out.println(entry.uuid() + " → " + entry.balance()));
});
```

### Authentication / Security

```java
// Check if a player is logged in (defaults to true when auth module absent)
boolean loggedIn = NexusPrismAPI.auth()
        .map(auth -> auth.isAuthenticated(uuid))
        .orElse(true);
```

### Clans

```java
// Get a player's clan tag
String tag = NexusPrismAPI.clans()
        .flatMap(c -> c.getClanTag(uuid))
        .orElse("");

// Check clan membership
boolean hasClan = NexusPrismAPI.clans()
        .map(c -> c.isInClan(uuid))
        .orElse(false);
```

### Essentials

```java
// Teleport a player to their home named "base"
NexusPrismAPI.essentials().ifPresent(ess ->
        ess.teleportHome(player, "base"));

// Check AFK status
boolean isAfk = NexusPrismAPI.essentials()
        .map(ess -> ess.isAfk(uuid))
        .orElse(false);
```

### Votes

```java
// Get a player's total vote count
int votes = NexusPrismAPI.votes()
        .map(v -> v.getTotalVotes(uuid))
        .orElse(0);

// Get current vote streak
int streak = NexusPrismAPI.votes()
        .map(v -> v.getStreak(uuid))
        .orElse(0);
```

### Custom Enchantments

```java
// Check if a tool has a specific custom enchant applied
boolean hasEnchant = NexusPrismAPI.enchants()
        .map(e -> e.hasEnchant(item, "SOUL_MENDER"))
        .orElse(false);

// Get the level of a custom enchant on an item
int level = NexusPrismAPI.enchants()
        .map(e -> e.getLevel(item, "SOUL_MENDER"))
        .orElse(0);
```

### Crates

```java
// Give a player a crate key
NexusPrismAPI.crates().ifPresent(c ->
        c.giveKey(player, "VOTE_CRATE", 1));
```

---

## Step 5 — Custom items

Use `NexusItemBuilder` to inspect any `ItemStack` and check whether it is a NexusPrism custom item.

```java
import io.github.otiger.nexusprism.api.items.builder.NexusItemBuilder;

ItemStack item = player.getInventory().getItemInMainHand();

// Get the internal item ID (e.g. "COPPER_DUST", "CELESTIAL_SWORD")
String id = NexusItemBuilder.getItemId(item); // null if not a NexusPrism item

if ("CELESTIAL_SWORD".equals(id)) {
    player.sendMessage("You are holding the Celestial Sword!");
}
```

You can also resolve a custom item from the registry via `getService`:

```java
import io.github.otiger.nexusprism.api.registry.ItemRegistry;

ItemRegistry registry = nexus.getService(ItemRegistry.class);
if (registry != null) {
    registry.getItem("COPPER_DUST").ifPresent(nexusItem -> {
        ItemStack stack = nexusItem.buildStack(1);
        player.getInventory().addItem(stack);
    });
}
```

---

## Step 6 — Territory API

If you are building a land-claiming or region system and want it to integrate with NexusPrism's protection checks (machine placement, clan building rules, etc.), implement `TerritoryProvider` and register it.

```java
import io.github.otiger.nexusprism.api.territory.TerritoryProvider;
import io.github.otiger.nexusprism.api.territory.TerritoryRegistry;
import org.bukkit.Location;
import org.bukkit.entity.Player;

public class MyRegionProvider implements TerritoryProvider {

    @Override
    public boolean isClaimed(Location location) {
        return MyRegionManager.isClaimed(location);
    }

    @Override
    public boolean canBuild(Player player, Location location) {
        return MyRegionManager.canBuild(player, location);
    }

    @Override
    public boolean canInteract(Player player, Location location) {
        return MyRegionManager.canInteract(player, location);
    }

    @Override
    public java.util.Optional<String> getClaimName(Location location) {
        return MyRegionManager.getRegionName(location);
    }
}
```

Register and unregister in your plugin's lifecycle:

```java
private final MyRegionProvider provider = new MyRegionProvider();

@Override
public void onEnable() {
    TerritoryRegistry.register(provider);
}

@Override
public void onDisable() {
    TerritoryRegistry.unregister(provider);
}
```

> NexusPrism uses **deny-wins** aggregation: if any registered provider denies `canBuild`, the action is blocked.

---

## Step 7 — Event flags

`EventFlags` exposes live server-state flags from the Events module. Read these to react to Blood Moon and economy multipliers.

```java
import io.github.otiger.nexusprism.api.events.EventFlags;

// Is the Blood Moon currently active?
if (EventFlags.bloodMoonActive) {
    // Double your boss spawn rates, apply particle effects, etc.
}

// Current economy kill-pay multiplier (1.0 = normal, 1.5 = +50% during Blood Moon)
double multiplier = EventFlags.killPayMultiplier;
double reward = baseReward * multiplier;
```

---

## Step 8 — Structure loot injection

Register a `StructureProvider` to inject custom loot into vanilla structures when they are generated.

```java
import io.github.otiger.nexusprism.api.structures.StructureProvider;
import io.github.otiger.nexusprism.api.structures.StructureRegistry;
import org.bukkit.NamespacedKey;
import org.bukkit.inventory.ItemStack;
import java.util.List;

public class MyLootProvider implements StructureProvider {

    @Override
    public NamespacedKey structure() {
        return NamespacedKey.minecraft("village/plains/houses/plains_small_house_1");
    }

    @Override
    public List<ItemStack> loot() {
        // Return items to inject into chests inside this structure
        return List.of(new ItemStack(Material.DIAMOND, 1));
    }
}
```

```java
// Register on enable, unregister on disable
StructureRegistry.register(new MyLootProvider());
```

---

## Step 9 — Writing a native addon

Native addons are JAR files dropped into `plugins/NexusPrism/addons/`. They are loaded by NexusPrism directly and do not need their own `plugin.yml`.

### 1. Create the addon class

```java
import io.github.otiger.nexusprism.api.addon.AbstractNexusAddon;
import io.github.otiger.nexusprism.api.NexusPrismAPI;

public class MyAddon extends AbstractNexusAddon {

    @Override
    public void onEnable() {
        // Load config (reads config.yml from JAR if not yet extracted)
        saveDefaultConfig();
        String welcomeMsg = getConfig().getString("welcome-message", "Hello!");
        getLogger().info(welcomeMsg);

        // Use the API
        NexusPrismAPI api = getAPI();
        getLogger().info("Hooked — NexusPrism " + api.getVersion());

        // Register a territory provider
        TerritoryRegistry.register(new MyRegionProvider());
    }

    @Override
    public void onDisable() {
        TerritoryRegistry.unregister(myProvider);
        getLogger().info(getName() + " disabled.");
    }
}
```

### 2. Create `addon.yml` inside the JAR

```yaml
id: my-addon
name: My Addon
version: 1.0.0
description: Demonstrates the NexusPrism addon API.
authors:
  - YourName
main: com.example.MyAddon
min-nexus-version: 1.0.0

# Hard dependencies (must be present):
dependencies: []

# Optional dependencies (loaded first if present):
soft-dependencies: []
```

### 3. Build and install

```
mvn package
cp target/my-addon-1.0.0.jar plugins/NexusPrism/addons/
```

Restart the server. You should see:

```
[NexusPrism] [MyAddon] Hello!
[NexusPrism] [MyAddon] Hooked — NexusPrism 1.0.0-DEV
```

---

## Complete integration example

Below is a full minimal plugin that hooks into NexusPrism, rewards players with money on kill, and respects Blood Moon multipliers.

```java
package com.example;

import io.github.otiger.nexusprism.api.NexusPrismAPI;
import io.github.otiger.nexusprism.api.events.EventFlags;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.entity.PlayerDeathEvent;
import org.bukkit.plugin.java.JavaPlugin;

public class KillRewardPlugin extends JavaPlugin implements Listener {

    @Override
    public void onEnable() {
        if (NexusPrismAPI.get() == null) {
            getLogger().warning("NexusPrism not found — disabling kill rewards.");
            return;
        }
        getServer().getPluginManager().registerEvents(this, this);
        getLogger().info("Kill rewards enabled.");
    }

    @EventHandler
    public void onPlayerKill(PlayerDeathEvent event) {
        if (!(event.getEntity().getKiller() instanceof Player killer)) return;

        double base = 25.0;
        double reward = base * EventFlags.killPayMultiplier; // scales with Blood Moon

        NexusPrismAPI.economy().ifPresent(eco -> {
            eco.addMoney(killer.getUniqueId(), reward);
            killer.sendMessage("§a+$" + String.format("%.0f", reward) + " §7for the kill!");
        });
    }
}
```

---

## Quick-reference

| API surface | Class / method |
|---|---|
| Get API instance | `NexusPrismAPI.get()` |
| Economy | `NexusPrismAPI.economy()` → `EconomyProvider` |
| Auth | `NexusPrismAPI.auth()` → `AuthProvider` |
| Clans | `NexusPrismAPI.clans()` → `ClanProvider` |
| Essentials | `NexusPrismAPI.essentials()` → `EssentialsProvider` |
| Votes | `NexusPrismAPI.votes()` → `VoteProvider` |
| Enchantments | `NexusPrismAPI.enchants()` → `CustomEnchantProvider` |
| Crates | `NexusPrismAPI.crates()` → `CrateProvider` |
| Item ID lookup | `NexusItemBuilder.getItemId(ItemStack)` |
| Item registry | `nexus.getService(ItemRegistry.class)` |
| Territory | `TerritoryRegistry.register(TerritoryProvider)` |
| Event state | `EventFlags.bloodMoonActive`, `EventFlags.killPayMultiplier` |
| Structures | `StructureRegistry.register(StructureProvider)` |
| Native addon base | `AbstractNexusAddon` + `addon.yml` |

---

## Best practices

- **Always null-check** `NexusPrismAPI.get()` before using any provider.
- **Use `softdepend`** unless your plugin is literally an addon JAR — this lets your plugin load even if NexusPrism is absent.
- **Never shade** `nexusprism-api` — use `provided`/`compileOnly` scope.
- **Unregister providers** in `onDisable()` to avoid ghost listeners after reload.
- **Use `Optional` chains** (`ifPresent`, `orElse`) — never call `.get()` on an empty Optional.
- **Check `isReady()`** if you call the API immediately on enable; NexusPrism loads modules asynchronously.
