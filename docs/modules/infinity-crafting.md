# Infinity Crafting Module

Infinity Crafting is NexusPrism's **multiblock crafting system**. Players build physical multiblock structures in the world and use them as advanced crafting stations. Recipes are defined entirely in YAML.

---

## Overview

| Feature | Description |
| --- | --- |
| **Multiblock structures** | Crafting stations built from specific block patterns |
| **YAML recipes** | No Java required — define recipes in `data/crafting/infinity_table/` |
| **GUI interface** | Drag-and-drop recipe input/output via inventory GUI |
| **Research gate** | Recipes can require specific research to unlock |
| **Machine integration** | Some infinity recipes require energy or machine output as ingredients |

---

## Multiblock Setup

Multiblocks are physical structures placed in the world. Their layout is defined in `multiblocks.yml`.

### Building a Multiblock

1. Gather the required blocks listed in the multiblock's definition
2. Build the structure in the exact shape shown in the guide
3. Right-click the controller block to open the crafting GUI
4. Insert ingredients and collect the output

### `multiblocks.yml` Example

```yaml
INFINITY_TABLE:
  display-name: "&bInfinity Crafting Table"
  description: "The core multiblock for Infinity-tier crafting."
  controller: CRAFTING_TABLE
  structure:
    # Layer definitions: Y=0 is the base, Y=1 is the middle, etc.
    layers:
      0:
        - "DDD"
        - "DCD"
        - "DDD"
      1:
        - "   "
        - " C "
        - "   "
    legend:
      D: DEEPSLATE_BRICKS
      C: CRAFTING_TABLE   # Controller block
```

---

## Recipe YAML Format

Recipes are placed in `plugins/NexusPrism/data/crafting/infinity_table/` as individual `.yml` files. The filename serves as the recipe ID.

### Shaped Recipe

```yaml
# data/crafting/infinity_table/nexus_core.yml
type: SHAPED
station: INFINITY_TABLE
output:
  item: NEXUS_CORE
  amount: 1

shape:
  - "GEG"
  - "EDE"
  - "GEG"

ingredients:
  G: GOLD_INGOT
  E: ENDER_PEARL
  D: DIAMOND

research-required: ADVANCED_METALLURGY    # Optional research gate
energy-cost: 500                          # Optional energy cost (RF/FE)
```

### Shapeless Recipe

```yaml
# data/crafting/infinity_table/star_dust.yml
type: SHAPELESS
station: INFINITY_TABLE
output:
  item: STAR_DUST
  amount: 4

ingredients:
  - GLOWSTONE_DUST
  - GLOWSTONE_DUST
  - BLAZE_POWDER
  - ENDER_PEARL
```

### Smelting Recipe (via Machine)

```yaml
# data/crafting/infinity_table/copper_ingot.yml
type: MACHINE_SMELT
station: ELECTRIC_FURNACE
output:
  item: COPPER_INGOT
  amount: 1

input:
  item: RAW_COPPER
  amount: 1

energy-cost: 100
processing-ticks: 200
```

### Field Reference

| Field | Description |
| --- | --- |
| `type` | `SHAPED`, `SHAPELESS`, `MACHINE_SMELT` |
| `station` | The multiblock ID required to craft this recipe |
| `output.item` | Output item ID (NexusPrism custom or vanilla Material) |
| `output.amount` | Stack size of the output |
| `shape` | 3-row grid pattern for shaped recipes (3 chars per row) |
| `ingredients` | Map of char → item ID (shaped) or list of item IDs (shapeless) |
| `research-required` | Research ID that must be unlocked before this recipe appears |
| `energy-cost` | Energy (RF) consumed per craft |
| `processing-ticks` | Ticks taken by machine recipes |

---

## In-Game Guide

All infinity recipes are visible in the in-game guide. Open it with `/nexusprism guide` and navigate to the **Infinity** tier section.

The guide shows:

- Required multiblock station
- Ingredient list with counts
- Research requirement (if any)
- Energy cost (if any)

---

## Commands

| Command | Usage | Permission |
| --- | --- | --- |
| `/recipe <item>` | Show recipe(s) for an item | `nexusprism.recipe` |
| `/nexusprism guide` | Open item guide GUI | `nexusprism.command` |
| `/nexusprism reload` | Reload all recipes and multiblocks | `nexusprism.admin.reload` |

---

## Permissions

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.recipe` | View recipes with `/recipe` | true |
| `nexusprism.craft` | Use crafting stations | true |
| `nexusprism.admin.reload` | Reload plugin configs/recipes | OP |
