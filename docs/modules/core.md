# Core Module

The Core module is the foundation of NexusPrism. It manages the custom item registry, PDC (PersistentDataContainer) tagging system, machine engine, research tree, backpacks, and waypoints.

---

## Custom Item System

All custom items are defined in `plugins/NexusPrism/items.yml`. The plugin ships with **235+ items** out of the box.

### `items.yml` Example

```yaml
COPPER_DUST:
  category: DUST
  tier: BASIC
  display-name: "&fCopper Dust"
  lore:
    - "&7A fine copper powder."
  material: PAPER
  custom-model-data: 1001
  glow: false
  stackable: true
  max-stack: 64

NEXUS_PICKAXE:
  category: TOOL
  tier: ADVANCED
  display-name: "&bNexus Pickaxe"
  lore:
    - "&7Mines at incredible speed."
    - "&8Tier: Advanced"
  material: DIAMOND_PICKAXE
  custom-model-data: 2005
  glow: true
  enchantments:
    EFFICIENCY: 5
    UNBREAKING: 3
```

### Item Categories

| Category | Description |
| --- | --- |
| `DUST` | Crafting dusts (copper, tin, silver…) |
| `INGOT` | Processed metal ingots |
| `TOOL` | Custom tools and weapons |
| `MACHINE` | Placeable machine blocks |
| `COMPONENT` | Circuit boards, gears, etc. |
| `RESOURCE` | Raw crafting resources |
| `ENERGY` | Energy components |
| `BACKPACK` | Backpack items |

### Item Tiers (`NexusTier`)

| Tier | Description |
| --- | --- |
| `BASIC` | Starter tier — no research required |
| `ADVANCED` | Requires basic research |
| `INFINITY` | Endgame tier — requires parchments |

---

## PDC System

NexusPrism uses Minecraft's **PersistentDataContainer** to tag custom items, machines, and player data. Each NexusPrism item carries a `nexusprism:id` PDC key that identifies it uniquely.

Key classes:

- `CustomItemRegistry` — registers and resolves all custom items
- `NexusItemIdResolver` — resolves item IDs from PDC
- `NexusItemMigrator` — migrates legacy items to new IDs

---

## Research System

Players unlock items and machines by spending XP on research. Research is tiered — **Basic → Advanced → Infinity**.

```yaml
# researches.yml
COPPER_PROCESSING:
  tier: BASIC
  xp-cost: 10
  display-name: "&fCopper Processing"
  description: "Unlock copper dust, copper ingots, and basic machines."
  unlocks:
    - COPPER_DUST
    - COPPER_INGOT
    - BASIC_CRUSHER
```

| Permission | Description |
| --- | --- |
| `nexusprism.research` | Use the research system (default: true) |
| `nexusprism.research.all` | Unlock all research instantly (OP) |

---

## Backpacks

Backpacks are portable storage containers. Players start with a basic backpack and can upgrade it.

### Commands

| Command | Usage | Permission |
| --- | --- | --- |
| `/backpack open` | Open your backpack | `nexusprism.essentials.backpack` |
| `/backpack open <id>` | Open a specific backpack | `nexusprism.essentials.backpack` |
| `/backpack list` | List all backpacks | `nexusprism.essentials.backpack` |

### Permissions

| Permission | Description |
| --- | --- |
| `nexusprism.backpack.create` | Create backpacks (default: true) |
| `nexusprism.backpack.upgrade` | Upgrade backpacks (default: true) |
| `nexusprism.backpack.unlimited` | Unlimited backpack slots (OP) |

---

## Waypoints

Waypoints are personal fast-travel points saved by the player.

### Waypoints Commands

| Command | Usage | Permission |
| --- | --- | --- |
| `/waypoint create <name>` | Create a waypoint | `nexusprism.essentials.waypoint` |
| `/waypoint delete <name>` | Delete a waypoint | `nexusprism.essentials.waypoint` |
| `/waypoint list` | List all waypoints | `nexusprism.essentials.waypoint` |
| `/waypoint tp <name>` | Teleport to a waypoint | `nexusprism.essentials.waypoint` |
| `/waypoint info <name>` | Show waypoint details | `nexusprism.essentials.waypoint` |

Aliases: `/wp`

### Slot Limit Permissions

| Permission | Slots |
| --- | --- |
| `nexusprism.essentials.waypoints.1` | 1 (default) |
| `nexusprism.essentials.waypoints.5` | 5 |
| `nexusprism.essentials.waypoints.25` | 25 |
| `nexusprism.essentials.waypoints.unlimited` | Unlimited (OP) |

---

## Main Plugin Commands

| Command | Usage | Permission |
| --- | --- | --- |
| `/nexusprism help` | Show help | `nexusprism.command` |
| `/nexusprism info` | Plugin info | `nexusprism.command` |
| `/nexusprism reload` | Reload all configs | `nexusprism.admin.reload` |
| `/nexusprism give <player> <item>` | Give a custom item | `nexusprism.admin.give` |
| `/nexusprism guide` | Open the item guide | `nexusprism.command` |
| `/nexusprism modules` | List loaded modules | `nexusprism.command` |
| `/nexusprism machine info <id>` | Machine info | `nexusprism.command` |
| `/nexusprism machine list` | List machines | `nexusprism.command` |
| `/nexusprism energy info <loc>` | Energy node info | `nexusprism.command` |
| `/nexusprism energy network` | Energy network view | `nexusprism.command` |

Aliases: `/ns`, `/nexus`, `/slime`, `/nslime`

---

## Language Support

NexusPrism ships with four language files:

| File | Language |
| --- | --- |
| `lang/en_US.yml` | English (default) |
| `lang/pt_BR.yml` | Brazilian Portuguese |
| `lang/es_ES.yml` | Spanish |
| `lang/zh_CN.yml` | Chinese (Simplified) |

Set the active language in `config.yml`:

```yaml
settings:
  language: en_US
```
