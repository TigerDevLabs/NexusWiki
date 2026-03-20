# API para Desarrolladores NexusPrism

Esta guía explica cómo integrarse con NexusPrism desde un plugin externo de Bukkit/Paper o un addon nativo. Solo compilas contra `nexusprism-api` — nunca contra los JARs concretos de los módulos.

---

## Paso 1 — Agregar la dependencia

NexusPrism se publica a través de **JitPack**. Agrega el repositorio y el artefato de la API a tu `pom.xml`:

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
        <version>master-SNAPSHOT</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

> **El alcance `provided` es obligatorio.** NexusPrism incluye la API en tiempo de ejecución — no la incluyas (shade) en tu JAR.

Para Gradle (Kotlin DSL):

```kotlin
repositories {
    maven("https://jitpack.io")
}

dependencies {
    compileOnly("com.github.O-Tiger.NexusPrismModularizado:nexusprism-api:master-SNAPSHOT")
}
```

---

## Paso 2 — Declarar la dependencia en `plugin.yml`

Como NexusPrism es opcional para la mayoría de las integraciones, usa `softdepend`. Usa `depend` solo si tu plugin no puede funcionar sin él.

```yaml
name: MiPlugin
version: 1.0.0
main: com.ejemplo.MiPlugin
api-version: "1.21"

softdepend:
  - NexusPrism
```

---

## Paso 3 — Obtener la instancia de la API

Siempre obtén la API dentro de `onEnable()`, **después** de que el servidor esté completamente iniciado. Nunca la llames desde un inicializador estático o constructor.

```java
import io.github.otiger.nexusprism.api.NexusPrismAPI;

public class MiPlugin extends JavaPlugin {

    private NexusPrismAPI nexus;

    @Override
    public void onEnable() {
        nexus = NexusPrismAPI.get();

        if (nexus == null) {
            getLogger().warning("NexusPrism no encontrado — integración desactivada.");
            return;
        }

        if (!nexus.isReady()) {
            getLogger().warning("NexusPrism todavía está iniciando.");
            return;
        }

        getLogger().info("Conectado a NexusPrism " + nexus.getVersion());
    }
}
```

---

## Paso 4 — Proveedores de módulos

Cada módulo opcional de NexusPrism expone un proveedor tipado a través de un registro estático. Todos los proveedores devuelven `Optional` — si el módulo está desactivado o no instalado, el Optional estará vacío. Siempre usa `ifPresent` u `orElse` para manejarlo de forma segura.

### Economía

```java
UUID uuid = player.getUniqueId();

// Leer saldo
double saldo = NexusPrismAPI.economy()
        .map(eco -> eco.getBalance(uuid))
        .orElse(0.0);

// Añadir dinero
NexusPrismAPI.economy().ifPresent(eco -> eco.addMoney(uuid, 500.0));

// Cobrar al jugador (devuelve false si saldo insuficiente)
boolean exito = NexusPrismAPI.economy()
        .map(eco -> eco.withdrawMoney(uuid, 100.0))
        .orElse(false);

// Top saldos
NexusPrismAPI.economy().ifPresent(eco ->
    eco.getTopBalances(10).forEach(entry ->
        System.out.println(entry.uuid() + " → " + entry.balance())));
```

### Autenticación / Seguridad

```java
// Verificar si el jugador ha iniciado sesión (por defecto true si el módulo está ausente)
boolean logueado = NexusPrismAPI.auth()
        .map(auth -> auth.isAuthenticated(uuid))
        .orElse(true);
```

### Clanes

```java
// Obtener la etiqueta del clan del jugador
String etiqueta = NexusPrismAPI.clans()
        .flatMap(c -> c.getClanTag(uuid))
        .orElse("");

// Verificar si pertenece a un clan
boolean tieneClan = NexusPrismAPI.clans()
        .map(c -> c.isInClan(uuid))
        .orElse(false);
```

### Essentials

```java
// Teleportar al jugador a su home "base"
NexusPrismAPI.essentials().ifPresent(ess ->
        ess.teleportHome(player, "base"));

// Verificar estado AFK
boolean estaAfk = NexusPrismAPI.essentials()
        .map(ess -> ess.isAfk(uuid))
        .orElse(false);
```

### Votos

```java
// Total de votos del jugador
int votos = NexusPrismAPI.votes()
        .map(v -> v.getTotalVotes(uuid))
        .orElse(0);

// Racha actual de votos
int racha = NexusPrismAPI.votes()
        .map(v -> v.getStreak(uuid))
        .orElse(0);
```

### Encantamientos Personalizados

```java
// Verificar si un ítem tiene un encantamiento personalizado
boolean tieneEncant = NexusPrismAPI.enchants()
        .map(e -> e.hasEnchant(item, "SOUL_MENDER"))
        .orElse(false);

// Obtener el nivel de un encantamiento
int nivel = NexusPrismAPI.enchants()
        .map(e -> e.getLevel(item, "SOUL_MENDER"))
        .orElse(0);
```

### Cofres (Crates)

```java
// Dar una llave de cofre al jugador
NexusPrismAPI.crates().ifPresent(c ->
        c.giveKey(player, "VOTE_CRATE", 1));
```

### MMO

```java
MmoRegistry.get().ifPresent(mmo -> {
    int nivel  = mmo.getLevel(uuid);
    int mana   = mmo.getCurrentMana(uuid);
    if (mmo.hasMana(uuid, 20) && mmo.consumeMana(uuid, 20)) {
        // habilidad activada
    }
    mmo.addSkillXp(player, "warrior", 100L);
    mmo.addProfessionXp(player, "mining", 50L);
    int fuerza = mmo.getStat(uuid, "STRENGTH");
});
```

### Chat

```java
ChatRegistry.get().ifPresent(chat -> {
    boolean silenciado = chat.isMuted(uuid);
    chat.mute(uuid, 10 * 60 * 1000L, "Spam", "Consola");
    chat.broadcastToChannel("global", "[MiAddon] ¡Anuncio del servidor!");
    String canalActivo = chat.getActiveChannel(uuid);
});
```

### Protecciones

```java
ProtectionsRegistry.get().ifPresent(prot -> {
    boolean pvp = prot.isPvpAllowed(location);
    boolean enDuelo = prot.isInDuel(uuid);
    prot.getDuelOpponent(uuid).ifPresent(oponente -> { /* ... */ });
    List<String> regiones = prot.getRegionNamesAt(location);
});
```

### Eventos (Luna de Sangre, Arco del Sacrificio, Jefe Isekai)

```java
EventsRegistry.get().ifPresent(events -> {
    boolean lunaActiva   = events.isBloodMoonActive();
    int racha            = events.getSacrificeStreak(uuid);
    boolean enSacrificio = events.isInSacrifice(uuid);
    boolean tienJefe     = events.hasActiveBossFight(uuid);
});
```

### Hologramas

```java
HologramRegistry.get().ifPresent(holo -> {
    holo.create("mi_holo", location);
    holo.addLine("mi_holo", "§a¡Hola desde mi addon!");
    holo.setLine("mi_holo", 0, "§eLínea actualizada");
    holo.showToPlayer("mi_holo", player);
    holo.delete("mi_holo");
});
```

### Mochilas

```java
BackpackRegistry.get().ifPresent(bp -> {
    int cantidad = bp.getBackpackCount(uuid);
    bp.openFirstBackpack(player);
    bp.openBackpack(player, ids.get(0));
});
```

### Traits (Cartas del Tarot)

```java
TraitsRegistry.get().ifPresent(traits -> {
    List<String> cartas = traits.getCards(uuid);
    boolean tieneCarta  = traits.hasCard(uuid, "The Tower");
    int nivelInvestigacion = traits.getResearchLevel(uuid);
});
```

### Discord

```java
DiscordRegistry.get().ifPresent(discord -> {
    boolean vinculado = discord.isLinked(uuid);
    discord.sendMessage("server-log", "[MiAddon] ¡Algo ocurrió!");
    discord.sendWebhook("server-log", "Bot MiAddon", null, "El jugador hizo algo.");
});
```

### Empleos

```java
JobRegistry.get().ifPresent(empleos -> {
    Optional<String> empleoId = empleos.getActiveJob(uuid);
    boolean tieneEmpleo = empleos.hasJob(uuid);
    if (tieneEmpleo) {
        int nivel = empleos.getLevel(uuid, empleoId.get());
    }
    empleos.joinJob(uuid, "miner");
    empleos.leaveJob(uuid);
});
```

### Redes de Energía

```java
EnergyRegistry.get().ifPresent(energia -> {
    energia.getNetworkAt(location).ifPresent(red -> {
        long almacenado = red.getTotalStoredEnergy();
        long cap        = red.getTotalCapacity();
        int  flujo      = red.getNetFlow();
    });
    energia.registerComponent(miComponente);
    energia.unregisterComponent(miComponente);
});
```

---

## Paso 10 — Carga de Contenido desde Addons

Los addons nativos pueden registrar **ítems**, **máquinas**, **recetas de crafteo** y **recetas de infinity** directamente desde archivos YAML empaquetados en el JAR.

```java
ContentLoadResult result = content()
        .items("items.yml")
        .machines("machines.yml")
        .recipes("recipes.yml")
        .infinityRecipes("infinity_recipes")
        .register();

result.logTo(getLogger());
```

### Recetas de Procesamiento de Máquinas (programático)

```java
MachineProcessingRegistry.register(
    MachineProcessingRecipe.builder("mi_receta", "EXAMPLE_FURNACE")
            .input("DIAMOND", 1)
            .output("EXAMPLE_INGOT", 3)
            .time(120)
            .source(getId())
            .build()
);

// En onDisable — siempre limpia:
MachineProcessingRegistry.unregisterBySource(getId());
```

---

## Paso 5 — Ítems personalizados

Usa `NexusItemBuilder` para inspeccionar cualquier `ItemStack` y verificar si es un ítem personalizado de NexusPrism.

```java
import io.github.otiger.nexusprism.api.items.builder.NexusItemBuilder;

ItemStack item = player.getInventory().getItemInMainHand();

// Obtener el ID interno del ítem (ej: "COPPER_DUST", "CELESTIAL_SWORD")
String id = NexusItemBuilder.getItemId(item); // null si no es ítem NexusPrism

if ("CELESTIAL_SWORD".equals(id)) {
    player.sendMessage("¡Estás sosteniendo la Espada Celestial!");
}
```

Para crear un ítem del registro:

```java
import io.github.otiger.nexusprism.api.registry.ItemRegistry;

ItemRegistry registro = nexus.getService(ItemRegistry.class);
if (registro != null) {
    registro.getItem("COPPER_DUST").ifPresent(nexusItem -> {
        ItemStack stack = nexusItem.buildStack(1);
        player.getInventory().addItem(stack);
    });
}
```

---

## Paso 6 — API de Territorio

Si estás construyendo un sistema de reclamación de tierras, implementa `TerritoryProvider` y regístralo para que se integre con las verificaciones de protección de NexusPrism.

```java
import io.github.otiger.nexusprism.api.territory.TerritoryProvider;
import io.github.otiger.nexusprism.api.territory.TerritoryRegistry;

public class MiProveedorRegion implements TerritoryProvider {

    @Override
    public boolean isClaimed(Location location) {
        return MiGestorRegion.isClaimed(location);
    }

    @Override
    public boolean canBuild(Player player, Location location) {
        return MiGestorRegion.canBuild(player, location);
    }

    @Override
    public boolean canInteract(Player player, Location location) {
        return MiGestorRegion.canInteract(player, location);
    }

    @Override
    public Optional<String> getClaimName(Location location) {
        return MiGestorRegion.getRegionName(location);
    }
}
```

```java
private final MiProveedorRegion proveedor = new MiProveedorRegion();

@Override
public void onEnable() {
    TerritoryRegistry.register(proveedor);
}

@Override
public void onDisable() {
    TerritoryRegistry.unregister(proveedor);
}
```

> NexusPrism usa agregación **deny-wins**: si cualquier proveedor deniega `canBuild`, la acción se bloquea.

---

## Paso 7 — Flags de eventos

`EventFlags` expone flags de estado en tiempo real del módulo de eventos.

```java
import io.github.otiger.nexusprism.api.events.EventFlags;

// ¿Está activa la Luna de Sangre?
if (EventFlags.bloodMoonActive) {
    // Aplica efectos especiales...
}

// Multiplicador de recompensa por kill (1.0 = normal, 1.5 = +50% en Luna de Sangre)
double multiplicador = EventFlags.killPayMultiplier;
double recompensa = baseRecompensa * multiplicador;
```

---

## Paso 8 — Inyección de loot en estructuras

Registra un `StructureProvider` para inyectar loot personalizado en estructuras vanilla durante la generación.

```java
import io.github.otiger.nexusprism.api.structures.StructureProvider;
import io.github.otiger.nexusprism.api.structures.StructureRegistry;

public class MiLootProvider implements StructureProvider {

    @Override
    public NamespacedKey structure() {
        return NamespacedKey.minecraft("village/plains/houses/plains_small_house_1");
    }

    @Override
    public List<ItemStack> loot() {
        return List.of(new ItemStack(Material.DIAMOND, 1));
    }
}

// Registrar en onEnable:
StructureRegistry.register(new MiLootProvider());
```

---

## Paso 9 — Escribiendo un addon nativo

Los addons nativos son JARs colocados en `plugins/NexusPrism/addons/`. Son cargados directamente por NexusPrism y no necesitan `plugin.yml` propio.

### 1. Crear la clase del addon

```java
import io.github.otiger.nexusprism.api.addon.AbstractNexusAddon;

public class MiAddon extends AbstractNexusAddon {

    @Override
    public void onEnable() {
        saveDefaultConfig();
        String msg = getConfig().getString("mensaje-bienvenida", "¡Hola!");
        getLogger().info(msg);
        getLogger().info("Conectado — NexusPrism " + getAPI().getVersion());
    }

    @Override
    public void onDisable() {
        getLogger().info(getName() + " desactivado.");
    }
}
```

### 2. Crear `addon.yml` dentro del JAR

```yaml
id: mi-addon
name: Mi Addon
version: 1.0.0
description: Demuestra la API de addon de NexusPrism.
authors:
  - TuNombre
main: com.ejemplo.MiAddon
min-nexus-version: 1.0.0
dependencies: []
soft-dependencies: []
```

### 3. Compilar e instalar

```
mvn package
cp target/mi-addon-1.0.0.jar plugins/NexusPrism/addons/
```

---

## Ejemplo completo de integración

Plugin que recompensa a los jugadores con dinero al matar, respetando el multiplicador de la Luna de Sangre:

```java
package com.ejemplo;

import io.github.otiger.nexusprism.api.NexusPrismAPI;
import io.github.otiger.nexusprism.api.events.EventFlags;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.entity.PlayerDeathEvent;
import org.bukkit.plugin.java.JavaPlugin;

public class RecompensaKillPlugin extends JavaPlugin implements Listener {

    @Override
    public void onEnable() {
        if (NexusPrismAPI.get() == null) {
            getLogger().warning("NexusPrism no encontrado — recompensas desactivadas.");
            return;
        }
        getServer().getPluginManager().registerEvents(this, this);
    }

    @EventHandler
    public void onMuerteJugador(PlayerDeathEvent event) {
        if (!(event.getEntity().getKiller() instanceof Player killer)) return;

        double base = 25.0;
        double recompensa = base * EventFlags.killPayMultiplier;

        NexusPrismAPI.economy().ifPresent(eco -> {
            eco.addMoney(killer.getUniqueId(), recompensa);
            killer.sendMessage("§a+$" + String.format("%.0f", recompensa) + " §7por la kill!");
        });
    }
}
```

---

## Referencia Rápida

| Superficie de API | Clase / método |
|---|---|
| Obtener instancia de API | `NexusPrismAPI.get()` |
| **Proveedores principales** | |
| Economía | `NexusPrismAPI.economy()` → `EconomyProvider` |
| Auth | `NexusPrismAPI.auth()` → `AuthProvider` |
| Clanes | `NexusPrismAPI.clans()` → `ClanProvider` |
| Essentials | `NexusPrismAPI.essentials()` → `EssentialsProvider` |
| Votos | `NexusPrismAPI.votes()` → `VoteProvider` |
| Encantamientos | `NexusPrismAPI.enchants()` → `CustomEnchantProvider` |
| Cofres | `NexusPrismAPI.crates()` → `CrateProvider` |
| **Proveedores de módulos** | |
| MMO (nivel, stats, maná, skills, profesiones) | `MmoRegistry.get()` → `MmoProvider` |
| Chat (silencio, canales, broadcast) | `ChatRegistry.get()` → `ChatProvider` |
| Protecciones (PvP, regiones, duelos) | `ProtectionsRegistry.get()` → `ProtectionsProvider` |
| Eventos (Luna de Sangre, Sacrificio, Isekai) | `EventsRegistry.get()` → `EventsProvider` |
| Hologramas (crear, actualizar, mostrar/ocultar) | `HologramRegistry.get()` → `HologramProvider` |
| Mochilas (cantidad, abrir GUI) | `BackpackRegistry.get()` → `BackpackProvider` |
| Traits / Cartas del Tarot | `TraitsRegistry.get()` → `TraitsProvider` |
| Discord (vincular, enviar mensaje/webhook) | `DiscordRegistry.get()` → `DiscordProvider` |
| Empleos (empleo activo, nivel, XP) | `JobRegistry.get()` → `JobProvider` |
| Redes de energía | `EnergyRegistry.get()` → `EnergyProvider` |
| **Contenido y extensibilidad** | |
| Carga de contenido de addon | `content().items().machines().recipes().register()` |
| Recetas de procesamiento de máquinas | `MachineProcessingRegistry.register(MachineProcessingRecipe)` |
| ID de ítem | `NexusItemBuilder.getItemId(ItemStack)` |
| Registro de ítems | `nexus.getService(ItemRegistry.class)` |
| Territorio | `TerritoryRegistry.register(TerritoryProvider)` |
| Estado de eventos | `EventFlags.bloodMoonActive`, `EventFlags.killPayMultiplier` |
| Estructuras | `StructureRegistry.register(StructureProvider)` |
| Base de addon nativo | `AbstractNexusAddon` + `addon.yml` |
| Plantilla inicial | [O-Tiger/NexusPrism-Addon-Example](https://github.com/O-Tiger/NexusPrism-Addon-Example) |

---

## Buenas prácticas

- **Siempre verifica null** en `NexusPrismAPI.get()` antes de usar cualquier proveedor.
- **Usa `softdepend`** a menos que tu plugin sea literalmente un JAR de addon.
- **Nunca hagas shade** de `nexusprism-api` — usa alcance `provided`/`compileOnly`.
- **Cancela el registro de proveedores** en `onDisable()` para evitar listeners fantasma tras un reload.
- **Usa cadenas de `Optional`** (`ifPresent`, `orElse`) — nunca llames `.get()` en un Optional vacío.
- **Verifica `isReady()`** si llamas a la API inmediatamente en el enable.
