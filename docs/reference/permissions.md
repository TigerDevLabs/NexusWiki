# Permissions Reference

Complete list of all permission nodes registered by NexusPrism. Nodes marked **OP** default to operators only; nodes marked **true** are granted to all players by default.

---

## Core & Admin

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.*` | All permissions | OP |
| `nexusprism.command` | Use basic `/nexusprism` command | true |
| `nexusprism.admin` | General admin access | OP |
| `nexusprism.admin.*` | All admin permissions | OP |
| `nexusprism.admin.reload` | Reload plugin configs | OP |
| `nexusprism.admin.give` | Give custom items | OP |
| `nexusprism.admin.debug` | Toggle debug mode | OP |
| `nexusprism.admin.cleardata` | Clear player data | OP |
| `nexusprism.bypass.protection` | Bypass all region protections | OP |

---

## Research

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.research` | Access research system | true |
| `nexusprism.research.all` | Instantly unlock all research | OP |

---

## Backpacks

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.backpack.create` | Create backpacks | true |
| `nexusprism.backpack.upgrade` | Upgrade backpacks | true |
| `nexusprism.backpack.unlimited` | Unlimited backpack slots | OP |

---

## Waypoints

| Permission | Slots | Default |
| --- | --- | --- |
| `nexusprism.essentials.waypoints.1` | 1 waypoint | true |
| `nexusprism.essentials.waypoints.5` | 5 waypoints | — |
| `nexusprism.essentials.waypoints.25` | 25 waypoints | — |
| `nexusprism.essentials.waypoints.unlimited` | Unlimited | OP |
| `nexusprism.essentials.waypoint` | Access waypoint commands | true |

---

## Homes

| Permission | Slots | Default |
| --- | --- | --- |
| `nexusprism.essentials.homes.1` | 1 home | true |
| `nexusprism.essentials.homes.3` | 3 homes | — |
| `nexusprism.essentials.homes.10` | 10 homes | — |
| `nexusprism.essentials.homes.unlimited` | Unlimited | OP |
| `nexusprism.essentials.home` | Use /home, /sethome, /delhome | true |

---

## Essentials Commands

| Permission | Command | Default |
| --- | --- | --- |
| `nexusprism.essentials.warp.use` | `/warp` | true |
| `nexusprism.essentials.warp.admin` | `/setwarp`, `/delwarp` | OP |
| `nexusprism.essentials.back` | `/back` | true |
| `nexusprism.essentials.tpa` | `/tpa`, `/tpaccept`, `/tpdeny` | true |
| `nexusprism.essentials.spawn` | `/spawn` | true |
| `nexusprism.essentials.setspawn` | `/setspawn` | OP |
| `nexusprism.essentials.tphere` | `/tphere` | OP |
| `nexusprism.essentials.tppos` | `/tppos` | OP |
| `nexusprism.essentials.near` | `/near` | true |
| `nexusprism.essentials.fly` | `/fly` (self) | false |
| `nexusprism.essentials.fly.others` | `/fly <player>` | OP |
| `nexusprism.essentials.hat` | `/hat` | false |
| `nexusprism.essentials.god` | `/god` (self) | OP |
| `nexusprism.essentials.god.others` | `/god <player>` | OP |
| `nexusprism.essentials.heal` | `/heal` (self) | OP |
| `nexusprism.essentials.heal.others` | `/heal <player>` | OP |
| `nexusprism.essentials.feed` | `/feed` (self) | OP |
| `nexusprism.essentials.feed.others` | `/feed <player>` | OP |
| `nexusprism.essentials.nick` | `/nick` (self) | false |
| `nexusprism.essentials.nick.others` | `/nick <player>` | OP |
| `nexusprism.essentials.afk` | `/afk` | true |
| `nexusprism.essentials.workbench` | `/workbench` | true |
| `nexusprism.essentials.trash` | `/trash` | true |
| `nexusprism.essentials.anvil` | `/anvil` | OP |
| `nexusprism.essentials.grindstone` | `/grindstone` | OP |
| `nexusprism.essentials.stonecutter` | `/stonecutter` | OP |
| `nexusprism.essentials.speed` | `/speed` | OP |
| `nexusprism.essentials.seen` | `/seen` | true |
| `nexusprism.essentials.clearinventory` | `/clearinventory` (self) | OP |
| `nexusprism.essentials.clearinventory.others` | `/clearinventory <player>` | OP |
| `nexusprism.essentials.getpos` | `/getpos` | true |
| `nexusprism.essentials.playtime` | `/playtime` | true |
| `nexusprism.essentials.gamemode` | `/gamemode` | OP |
| `nexusprism.essentials.enderchest` | `/enderchest` (self) | true |
| `nexusprism.essentials.enderchest.others` | `/enderchest <player>` | OP |
| `nexusprism.essentials.repair` | `/repair` | OP |
| `nexusprism.essentials.ext` | `/ext` | OP |
| `nexusprism.essentials.exp` | `/exp` | OP |
| `nexusprism.essentials.worth` | `/worth` | true |
| `nexusprism.essentials.rules` | `/rules` | true |
| `nexusprism.essentials.skull` | `/skull` | OP |
| `nexusprism.essentials.jail.admin` | Jail management | OP |
| `nexusprism.essentials.backpack` | Backpack commands | true |

---

## Economy

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.economy.money` | View money balance | true |
| `nexusprism.economy.credits` | View credits | true |
| `nexusprism.economy.baltop` | View leaderboard | true |
| `nexusprism.economy.sell` | Use /sell | true |
| `nexusprism.economy.admin` | Admin eco commands | OP |

---

## Clans

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.clan.use` | Use clan commands | true |
| `nexusprism.clan.admin` | Admin clan management | OP |
| `nexusprism.clan.bypass-protection` | Bypass clan territory | OP |

---

## Security

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.security.cleanworld` | Manual world cleaner | OP |
| `nexusprism.staff.vanish` | Vanish yourself | OP |
| `nexusprism.staff.vanish.others` | Vanish another player | OP |
| `nexusprism.staff.vanish.see` | See vanished players | OP |
| `nexusprism.staff.invsee` | Inspect inventories | OP |
| `nexusprism.staff.spy` | Chat spy mode | OP |

---

## Chat

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.chat.staff` | Access staff chat channel | OP |
| `nexusprism.chat.mute` | Mute players | OP |
| `nexusprism.chat.mute.bypass` | Bypass mute | false |
| `nexusprism.chat.filter.bypass` | Bypass word filter | OP |
| `nexusprism.chat.reload` | Reload chat config | OP |
| `nexusprism.chat.color` | Use color codes in chat | OP |

---

## Protections & Duel

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.region.use` | Create and manage own regions | true |
| `nexusprism.protect.admin` | Admin region management | OP |
| `nexusprism.duel.use` | Send and accept duels | true |

---

## Crystal Defense

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.crystaldefense.use` | Join arenas | true |
| `nexusprism.crystaldefense.admin` | Create/manage arenas | OP |

---

## Votifier

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.vote` | Use `/vote` | true |
| `nexusprism.vote.top` | Use `/votetop` | true |

---

## Custom Mobs

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.boss.admin` | All boss/spawn-egg commands | OP |

---

## Dreams

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.dreams.admin` | Admin dreams commands | OP |

---

## Twitch

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.twitch.use` | Basic Twitch commands | true |
| `nexusprism.twitch.staff` | Approve links, run giveaways | OP |
| `nexusprism.twitch.admin` | Reload Twitch config | OP |

---

## Silk Spawners

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.silkspawner.use` | Mine spawners with Silk Touch | true |
| `nexusprism.silkspawner.admin` | Admin spawner commands | OP |

---

## Recipes & Kits

| Permission | Description | Default |
| --- | --- | --- |
| `nexusprism.recipe` | Use `/recipe` | true |
| `nexusprism.command.kit` | Use `/kit` | true |
| `nexusprism.command.vip` | Use `/vip` | true |
| `nexusprism.kit.*` | Access all VIP kits | OP |

---

## Permission Level Nodes

Used internally to map staff ranks. Configure in `config.yml`:

| Permission | Rank |
| --- | --- |
| `nexusprism.level.user` | Regular player |
| `nexusprism.level.helper` | Helper |
| `nexusprism.level.moderator` | Moderator |
| `nexusprism.level.admin` | Admin |
| `nexusprism.level.owner` | Owner |
