# Events Module

The Events module adds **world-scale dynamic events** that affect all players simultaneously — starting with the **Blood Moon**, which transforms nights into increasingly dangerous survival challenges tied to a per-player streak and a **Sacrifice Arc**.

---

## Blood Moon

The Blood Moon automatically activates each night when world time crosses **tick 13000** and deactivates at dawn (**tick 23000**). Server operators can also control it manually.

### Effects While Active

| Effect | Detail |
| --- | --- |
| Mob level bonus | All Leveled Mob rolls receive **+2** |
| Hunter job pay | Multiplied by the configured `kill-pay-multiplier` (default ×1.5) |
| Particle rain | Red DUST particles spawn around every online player every 3 seconds |
| Horde waves | A mob horde spawns every `horde-interval-ticks` (default 5 min) |

At **dawn** (deactivation), every online player who survived earns **+1** to their survival streak.

### Horde Waves

Each horde interval, a random online player is chosen as the target. **30 mobs** spawn in a ring 18 blocks around them from this pool: Zombie, Skeleton, Creeper, Spider, Witch, Husk, Drowned. All horde mobs are named `[Blood Moon]` in dark red.

### Commands

| Command | Description | Permission |
| --- | --- | --- |
| `/bloodmoon` | Show current Blood Moon status | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon start` | Force-activate the Blood Moon | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon stop` | Force-deactivate the Blood Moon | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon status` | Detailed status output | `nexusslime.events.bloodmoon.admin` |

### Configuration (`events/config.yml`)

```yaml
blood-moon:
  enabled: true
  world: world                   # The world to watch for time changes
  kill-pay-multiplier: 1.5       # Hunter job pay multiplier during Blood Moon
  particle-interval-ticks: 60   # How often (ticks) to spawn particles per player
  horde-interval-ticks: 6000    # How often (ticks) to fire a horde wave (6000 = 5 min)
  horde-size: 30                 # Number of mobs per horde wave
```

---

## Survival Streak

Every player has a personal **Blood Moon survival streak** stored persistently in SQLite (`events/events.db`).

| Event | Streak Change |
| --- | --- |
| Survive a full Blood Moon night | **+1** (awarded at dawn) |
| Die during a Blood Moon | **Reset to 0** |

When the streak reaches a **multiple of 7** (7, 14, 21, 28...), the player receives a **Sacrifice Invitation** the next time they sleep.

---

## Sacrifice Arc

The Sacrifice Arc is a high-stakes optional challenge triggered by the survival streak. It hooks into the [Dreams module](dreams.md): when the streak qualifies, sleeping opens a **choice GUI** instead of a dream cutscene.

### Choice GUI

A 3-row GUI with two options:

| Slot | Item | Action |
| --- | --- | --- |
| 11 | Green Wool — **Accept** | Teleport to arena, 90-second survival trial |
| 15 | Red Wool — **Decline** | Reset streak, no other penalty |

Closing the GUI without clicking counts as **Decline**.

### Arena Trial

1. The player is teleported to the configured arena (or stays in their current location if unconfigured)
2. **5 arena mobs** spawn: Zombie, Skeleton, Wither Skeleton, Blaze, Cave Spider
3. A **90-second countdown** begins with warnings at 30s, 10s, and 5s

### Outcomes

| Outcome | Result |
| --- | --- |
| **Survive** | Reward granted (default: 3 Diamond Blocks), server-wide broadcast, streak reset |
| **Die** | Streak reset to 0 |
| **Quit/disconnect** | Session cleaned up, treated as failure |

### Configuration (`events/config.yml`)

```yaml
sacrifice:
  arena:
    world: ""    # Leave blank to use the player's current world
    x: 0.0
    y: 64.0
    z: 0.0
```

!!! tip "Setting Up the Arena"
    Build a dedicated PvE arena and set its coordinates under `sacrifice.arena`. Leave `world` blank to fight in place — useful for testing.

---

## Permissions

| Permission | Description | Default |
| --- | --- | --- |
| `nexusslime.events.bloodmoon.admin` | Control Blood Moon manually | OP |
