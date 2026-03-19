# API para Desenvolvedores NexusPrism

Este guia mostra como integrar com o NexusPrism a partir de um plugin Bukkit/Paper externo ou de um addon nativo. Você compila apenas contra `nexusprism-api` — nunca contra os JARs concretos dos módulos.

---

## Passo 1 — Adicionar a dependência

O NexusPrism é publicado via **JitPack**. Adicione o repositório e o artefato da API ao seu `pom.xml`:

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

> **O escopo `provided` é obrigatório.** O NexusPrism inclui a API em tempo de execução — não a inclua (shade) no seu JAR.

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

## Passo 2 — Declarar a dependência no `plugin.yml`

Como o NexusPrism é opcional para a maioria das integrações, use `softdepend`. Use `depend` somente se o seu plugin não funcionar de forma alguma sem ele.

```yaml
name: MeuPlugin
version: 1.0.0
main: com.exemplo.MeuPlugin
api-version: "1.21"

softdepend:
  - NexusPrism
```

---

## Passo 3 — Obter a instância da API

Sempre obtenha a API dentro do `onEnable()`, **após** o servidor estar completamente iniciado. Nunca a chame de um inicializador estático ou construtor.

```java
import io.github.otiger.nexusprism.api.NexusPrismAPI;

public class MeuPlugin extends JavaPlugin {

    private NexusPrismAPI nexus;

    @Override
    public void onEnable() {
        nexus = NexusPrismAPI.get();

        if (nexus == null) {
            getLogger().warning("NexusPrism não encontrado — integração desativada.");
            return;
        }

        if (!nexus.isReady()) {
            getLogger().warning("NexusPrism ainda está inicializando.");
            return;
        }

        getLogger().info("Conectado ao NexusPrism " + nexus.getVersion());
    }
}
```

---

## Passo 4 — Provedores de módulos

Cada módulo opcional do NexusPrism expõe um provedor tipado através de um registro estático. Todos os provedores retornam `Optional` — se o módulo estiver desativado ou não instalado, o Optional estará vazio. Sempre use `ifPresent` ou `orElse` para lidar com isso com segurança.

### Economia

```java
UUID uuid = player.getUniqueId();

// Ler saldo
double saldo = NexusPrismAPI.economy()
        .map(eco -> eco.getBalance(uuid))
        .orElse(0.0);

// Adicionar dinheiro
NexusPrismAPI.economy().ifPresent(eco -> eco.addMoney(uuid, 500.0));

// Cobrar jogador (retorna false se saldo insuficiente)
boolean sucesso = NexusPrismAPI.economy()
        .map(eco -> eco.withdrawMoney(uuid, 100.0))
        .orElse(false);

// Top saldos
NexusPrismAPI.economy().ifPresent(eco ->
    eco.getTopBalances(10).forEach(entry ->
        System.out.println(entry.uuid() + " → " + entry.balance())));
```

### Autenticação / Segurança

```java
// Verificar se o jogador está logado (padrão true quando módulo ausente)
boolean logado = NexusPrismAPI.auth()
        .map(auth -> auth.isAuthenticated(uuid))
        .orElse(true);
```

### Clãs

```java
// Obter tag do clã do jogador
String tag = NexusPrismAPI.clans()
        .flatMap(c -> c.getClanTag(uuid))
        .orElse("");

// Verificar se está em um clã
boolean temCla = NexusPrismAPI.clans()
        .map(c -> c.isInClan(uuid))
        .orElse(false);
```

### Essentials

```java
// Teleportar jogador para a home "base"
NexusPrismAPI.essentials().ifPresent(ess ->
        ess.teleportHome(player, "base"));

// Verificar status AFK
boolean estaAfk = NexusPrismAPI.essentials()
        .map(ess -> ess.isAfk(uuid))
        .orElse(false);
```

### Votos

```java
// Total de votos do jogador
int votos = NexusPrismAPI.votes()
        .map(v -> v.getTotalVotes(uuid))
        .orElse(0);

// Sequência atual de votos
int sequencia = NexusPrismAPI.votes()
        .map(v -> v.getStreak(uuid))
        .orElse(0);
```

### Encantamentos Personalizados

```java
// Verificar se um item tem um encantamento personalizado
boolean temEnchant = NexusPrismAPI.enchants()
        .map(e -> e.hasEnchant(item, "SOUL_MENDER"))
        .orElse(false);

// Obter o nível de um encantamento
int nivel = NexusPrismAPI.enchants()
        .map(e -> e.getLevel(item, "SOUL_MENDER"))
        .orElse(0);
```

### Caixas (Crates)

```java
// Dar uma chave de caixa ao jogador
NexusPrismAPI.crates().ifPresent(c ->
        c.giveKey(player, "VOTE_CRATE", 1));
```

---

## Passo 5 — Itens personalizados

Use `NexusItemBuilder` para inspecionar qualquer `ItemStack` e verificar se é um item personalizado do NexusPrism.

```java
import io.github.otiger.nexusprism.api.items.builder.NexusItemBuilder;

ItemStack item = player.getInventory().getItemInMainHand();

// Obter o ID interno do item (ex: "COPPER_DUST", "CELESTIAL_SWORD")
String id = NexusItemBuilder.getItemId(item); // null se não for item NexusPrism

if ("CELESTIAL_SWORD".equals(id)) {
    player.sendMessage("Você está segurando a Espada Celestial!");
}
```

Para criar um item do registro:

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

## Passo 6 — API de Território

Se você estiver construindo um sistema de reivindicação de terrenos e quiser que ele se integre às verificações de proteção do NexusPrism, implemente `TerritoryProvider` e registre-o.

```java
import io.github.otiger.nexusprism.api.territory.TerritoryProvider;
import io.github.otiger.nexusprism.api.territory.TerritoryRegistry;

public class MeuProvedorRegiao implements TerritoryProvider {

    @Override
    public boolean isClaimed(Location location) {
        return MeuGerenciadorRegiao.isClaimed(location);
    }

    @Override
    public boolean canBuild(Player player, Location location) {
        return MeuGerenciadorRegiao.canBuild(player, location);
    }

    @Override
    public boolean canInteract(Player player, Location location) {
        return MeuGerenciadorRegiao.canInteract(player, location);
    }

    @Override
    public Optional<String> getClaimName(Location location) {
        return MeuGerenciadorRegiao.getRegionName(location);
    }
}
```

```java
private final MeuProvedorRegiao provedor = new MeuProvedorRegiao();

@Override
public void onEnable() {
    TerritoryRegistry.register(provedor);
}

@Override
public void onDisable() {
    TerritoryRegistry.unregister(provedor);
}
```

> O NexusPrism usa agregação **deny-wins**: se qualquer provedor negar `canBuild`, a ação é bloqueada.

---

## Passo 7 — Flags de eventos

`EventFlags` expõe flags de estado em tempo real do módulo de eventos.

```java
import io.github.otiger.nexusprism.api.events.EventFlags;

// A Lua de Sangue está ativa?
if (EventFlags.bloodMoonActive) {
    // Aplique efeitos especiais...
}

// Multiplicador de recompensa por kill (1.0 = normal, 1.5 = +50% na Lua de Sangue)
double multiplicador = EventFlags.killPayMultiplier;
double recompensa = baseRecompensa * multiplicador;
```

---

## Passo 8 — Injeção de loot em estruturas

Registre um `StructureProvider` para injetar loot personalizado em estruturas vanilla durante a geração.

```java
import io.github.otiger.nexusprism.api.structures.StructureProvider;
import io.github.otiger.nexusprism.api.structures.StructureRegistry;

public class MeuLootProvider implements StructureProvider {

    @Override
    public NamespacedKey structure() {
        return NamespacedKey.minecraft("village/plains/houses/plains_small_house_1");
    }

    @Override
    public List<ItemStack> loot() {
        return List.of(new ItemStack(Material.DIAMOND, 1));
    }
}

// Registrar no onEnable:
StructureRegistry.register(new MeuLootProvider());
```

---

## Passo 9 — Escrevendo um addon nativo

Addons nativos são JARs colocados em `plugins/NexusPrism/addons/`. Eles são carregados diretamente pelo NexusPrism e não precisam de `plugin.yml` próprio.

### 1. Criar a classe do addon

```java
import io.github.otiger.nexusprism.api.addon.AbstractNexusAddon;

public class MeuAddon extends AbstractNexusAddon {

    @Override
    public void onEnable() {
        saveDefaultConfig();
        String msg = getConfig().getString("mensagem-boas-vindas", "Olá!");
        getLogger().info(msg);
        getLogger().info("Conectado — NexusPrism " + getAPI().getVersion());
    }

    @Override
    public void onDisable() {
        getLogger().info(getName() + " desativado.");
    }
}
```

### 2. Criar `addon.yml` dentro do JAR

```yaml
id: meu-addon
name: Meu Addon
version: 1.0.0
description: Demonstra a API de addon do NexusPrism.
authors:
  - SeuNome
main: com.exemplo.MeuAddon
min-nexus-version: 1.0.0
dependencies: []
soft-dependencies: []
```

### 3. Compilar e instalar

```
mvn package
cp target/meu-addon-1.0.0.jar plugins/NexusPrism/addons/
```

---

## Exemplo completo de integração

Plugin que recompensa jogadores com dinheiro ao matar, respeitando o multiplicador da Lua de Sangue:

```java
package com.exemplo;

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
            getLogger().warning("NexusPrism não encontrado — recompensas desativadas.");
            return;
        }
        getServer().getPluginManager().registerEvents(this, this);
    }

    @EventHandler
    public void onMorteJogador(PlayerDeathEvent event) {
        if (!(event.getEntity().getKiller() instanceof Player killer)) return;

        double base = 25.0;
        double recompensa = base * EventFlags.killPayMultiplier;

        NexusPrismAPI.economy().ifPresent(eco -> {
            eco.addMoney(killer.getUniqueId(), recompensa);
            killer.sendMessage("§a+$" + String.format("%.0f", recompensa) + " §7pela kill!");
        });
    }
}
```

---

## Referência rápida

| Superfície da API | Classe / método |
|---|---|
| Obter instância | `NexusPrismAPI.get()` |
| Economia | `NexusPrismAPI.economy()` → `EconomyProvider` |
| Autenticação | `NexusPrismAPI.auth()` → `AuthProvider` |
| Clãs | `NexusPrismAPI.clans()` → `ClanProvider` |
| Essentials | `NexusPrismAPI.essentials()` → `EssentialsProvider` |
| Votos | `NexusPrismAPI.votes()` → `VoteProvider` |
| Encantamentos | `NexusPrismAPI.enchants()` → `CustomEnchantProvider` |
| Caixas | `NexusPrismAPI.crates()` → `CrateProvider` |
| ID de item | `NexusItemBuilder.getItemId(ItemStack)` |
| Registro de itens | `nexus.getService(ItemRegistry.class)` |
| Território | `TerritoryRegistry.register(TerritoryProvider)` |
| Estado de eventos | `EventFlags.bloodMoonActive`, `EventFlags.killPayMultiplier` |
| Estruturas | `StructureRegistry.register(StructureProvider)` |
| Base de addon nativo | `AbstractNexusAddon` + `addon.yml` |

---

## Boas práticas

- **Sempre verifique null** em `NexusPrismAPI.get()` antes de usar qualquer provedor.
- **Use `softdepend`** a menos que seu plugin seja literalmente um JAR de addon.
- **Nunca faça shade** de `nexusprism-api` — use escopo `provided`/`compileOnly`.
- **Cancele o registro de provedores** no `onDisable()` para evitar listeners fantasma após reload.
- **Use cadeias de `Optional`** (`ifPresent`, `orElse`) — nunca chame `.get()` em um Optional vazio.
- **Verifique `isReady()`** se você chamar a API imediatamente no enable.
