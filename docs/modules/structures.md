# Structures Module

The Structures module **injects custom loot** into vanilla structure chests. When the server generates loot for any supported structure, the module appends (or replaces) the chest contents with items defined in `structures/loot-tables.yml` — including custom NexusPrism items.

---

## How It Works

The module listens to Paper's `LootGenerateEvent`. When a structure chest is populated, it:
1. Identifies the structure by its loot table key
2. Looks up the configured entry in `loot-tables.yml`
3. Rolls the `min`–`max` additional item count and injects items by weight

No commands are needed — loot injection is fully passive.

---

## Supported Structures

| Structure | Default Injection |
| --- | --- |
| `minecraft:dungeon` | Research Parchment (Basic) |
| `minecraft:mineshaft` | Research Parchment (Basic) |
| `minecraft:desert_pyramid` | Research Parchment (Basic) |
| `minecraft:jungle_temple` | Research Parchment (Basic) |
| `minecraft:ocean_ruin` | Research Parchment (Basic) |
| `minecraft:shipwreck` | Research Parchment (Basic) |
| `minecraft:pillager_outpost` | Research Parchment (Basic) |
| `minecraft:stronghold` | Research Parchment (Advanced) |
| `minecraft:woodland_mansion` | Research Parchment (Advanced) |
| `minecraft:bastion_remnant` | Research Parchment (Advanced) |
| `minecraft:end_city` | Research Parchment (Infinity) |

---

## Configuration (`structures/loot-tables.yml`)

```yaml
minecraft:dungeon:
  mode: APPEND      # APPEND (add to vanilla loot) | REPLACE (clear vanilla loot first)
  rolls:
    min: 1
    max: 2
  items:
    - material: EMERALD           # Vanilla Minecraft material
      weight: 40
      amount:
        min: 1
        max: 5
    - material: ENCHANTED_BOOK
      weight: 8
      amount:
        min: 1
        max: 1
      random-enchant: true        # Applies a random vanilla enchant to the book
    - nexusprism-item: RESEARCH_PARCHMENT_BASIC   # Custom NexusPrism item by ID
      weight: 5
      amount:
        min: 1
        max: 1
```

### Configuration Fields

| Field | Description |
| --- | --- |
| `mode` | `APPEND` — add to vanilla loot. `REPLACE` — clear vanilla loot and use only this table. |
| `rolls.min` / `rolls.max` | Number of additional item stacks injected per chest open |
| `items[].material` | Vanilla `Material` name |
| `items[].nexusprism-item` | Custom NexusPrism item ID (from `items.yml`) |
| `items[].weight` | Relative probability; higher = more common |
| `items[].amount.min` / `.max` | Stack size range |
| `items[].random-enchant` | If `true` and material is `ENCHANTED_BOOK`, applies a random vanilla enchantment |

### Random Enchant Pool

When `random-enchant: true` is set, one of these enchantments is applied at a random valid level:

`SHARPNESS`, `PROTECTION`, `EFFICIENCY`, `SILK_TOUCH`, `FORTUNE`, `LOOTING`, `FLAME`, `POWER`, `INFINITY`, `MENDING`, `UNBREAKING`

---

## Addon API

Other plugins can register custom loot providers via the `StructureRegistry`:

```java
// Register during onEnable
StructureRegistry.register(new MyStructureProvider());

// Unregister during onDisable
StructureRegistry.unregister(provider);
```

The provider receives the loot table ID, the inventory holder, and a `Random` instance, and returns additional `ItemStack` additions alongside the YAML-defined entries.
