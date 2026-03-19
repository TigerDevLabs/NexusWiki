# Referencia PlaceholderAPI

NexusPrism registra su propia expansión PlaceholderAPI bajo el identificador `nexusprism`. Todos los placeholders siguen el patrón `%nexusprism_<nombre>%`.

**Requiere:** [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) (dependencia suave — instálalo por separado)

---

## Economía

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_money%` | Saldo de dinero actual del jugador | `12500.00` |
| `%nexusprism_credits%` | Saldo de créditos del jugador | `350` |

---

## Esenciales

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_playtime%` | Tiempo total de juego (formateado) | `3d 12h 45m` |
| `%nexusprism_playtime_minutes%` | Tiempo total de juego en minutos | `5085` |
| `%nexusprism_homes%` | Número de homes establecidos | `3` |
| `%nexusprism_afk%` | `true` si el jugador está AFK | `false` |
| `%nexusprism_afk_status%` | Estado AFK legible por humanos | `AFK` / `Online` |

---

## Clanes

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_clan_name%` | Nombre del clan del jugador | `Shadowborn` |
| `%nexusprism_clan_tag%` | Etiqueta del clan | `SHD` |
| `%nexusprism_clan_role%` | Rol del jugador en el clan | `Owner` / `Officer` / `Member` |
| `%nexusprism_clan_level%` | Nivel actual del clan | `5` |
| `%nexusprism_clan_members%` | Conteo de miembros en línea | `8` |
| `%nexusprism_clan_bank%` | Saldo del banco del clan | `75000.00` |

Devuelve cadena vacía si el jugador no está en un clan.

---

## Crystal Defense

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_crystal_wave%` | Número de oleada actual | `7` |
| `%nexusprism_crystal_health%` | HP restante del cristal | `680.0` |
| `%nexusprism_crystal_points%` | Puntos de eliminación del jugador en el juego actual | `145` |
| `%nexusprism_crystal_arena%` | Nombre de la arena en la que se encuentra el jugador | `arena1` |

Devuelve cadena vacía si el jugador no está en un juego de Crystal Defense.

---

## Seguridad

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_authenticated%` | `true` si el jugador está autenticado | `true` |
| `%nexusprism_auth_status%` | Estado de autenticación legible | `Authenticated` / `Pending` |

---

## Votifier

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_votes_total%` | Total de votos acumulados | `127` |
| `%nexusprism_vote_streak%` | Longitud de la racha de votos actual | `12` |

---

## Estadísticas del Jugador

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_player_blocks_broken%` | Total de bloques rotos | `48320` |
| `%nexusprism_player_machines_placed%` | Total de máquinas colocadas | `214` |
| `%nexusprism_player_items_crafted%` | Total de ítems crafteados | `5630` |
| `%nexusprism_player_energy_generated%` | Total de energía generada (RF) | `1200000` |
| `%nexusprism_player_items_smelted%` | Total de ítems fundidos | `890` |
| `%nexusprism_player_research_unlocked%` | Entradas de investigación desbloqueadas | `34` |
| `%nexusprism_player_level%` | Nivel NexusPrism del jugador | `15` |
| `%nexusprism_researched_<id>%` | `true` si una investigación específica está desbloqueada | `true` |

---

## Mochilas

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_backpacks_owned%` | Número de mochilas que posee el jugador | `2` |

---

## Máquinas

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_machines_count%` | Total de máquinas colocadas por el jugador | `42` |

---

## LuckPerms

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_lp_prefix%` | Prefijo LuckPerms del jugador | `&6[VIP]` |
| `%nexusprism_lp_suffix%` | Sufijo LuckPerms del jugador | `&7✦` |

Requieren que LuckPerms esté instalado.

---

## Guía

| Placeholder | Descripción |
| --- | --- |
| `%nexusprism_guide_<id>%` | Entrada dinámica de la guía para ID de ítem/máquina |

Son dinámicos — reemplaza `<id>` con cualquier ID de ítem o máquina registrado.

---

## Core / Varios

| Placeholder | Descripción | Ejemplo |
| --- | --- | --- |
| `%nexusprism_version%` | Cadena de versión del plugin | `2.0.0-BETA` |
| `%nexusprism_player%` | Nombre de usuario del jugador | `Steve` |
| `%nexusprism_uuid%` | UUID del jugador | `069a79f4-...` |

---

## Uso en Scoreboards / TAB

```yaml
# Ejemplo con el plugin TAB
header: "&bNexusPrism &7%nexusprism_version%"
tablist-name: "%nexusprism_lp_prefix%%player_name%"
scoreboard:
  title: "&b&lTus Estadísticas"
  lines:
    - "&7Dinero: &a$%nexusprism_money%"
    - "&7Créditos: &b%nexusprism_credits%"
    - "&7Votos: &e%nexusprism_votes_total% &7(racha: %nexusprism_vote_streak%)"
    - "&7Clan: &f%nexusprism_clan_name%"
    - "&7Tiempo de Juego: &f%nexusprism_playtime%"
```
