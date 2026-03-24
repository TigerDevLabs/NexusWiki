# Referencia de Permisos

Lista completa de todos los nodos de permisos registrados por NexusPrism. Los nodos marcados como **OP** son por defecto solo para operadores; los nodos marcados como **true** se otorgan a todos los jugadores por defecto.

---

## Core & Admin

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.*` | Todos los permisos | OP |
| `nexusprism.command` | Usar el comando básico `/nexusprism` | true |
| `nexusprism.admin` | Acceso administrativo general | OP |
| `nexusprism.admin.*` | Todos los permisos administrativos | OP |
| `nexusprism.admin.reload` | Recargar configuraciones del plugin | OP |
| `nexusprism.admin.give` | Dar ítems personalizados | OP |
| `nexusprism.admin.debug` | Alternar modo de depuración | OP |
| `nexusprism.admin.cleardata` | Limpiar datos de jugadores | OP |
| `nexusprism.bypass.protection` | Ignorar todas las protecciones de región | OP |

---

## Investigación

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.research` | Acceder al sistema de investigación | true |
| `nexusprism.research.all` | Desbloquear toda la investigación instantáneamente | OP |
| `nexusprism.research.admin` | Otorga acceso a los subcomandos de administración de `/nexusprism research` (all, tier, entry) | OP |

---

## Mochilas

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.backpack.create` | Crear mochilas | true |
| `nexusprism.backpack.upgrade` | Actualizar mochilas | true |
| `nexusprism.backpack.unlimited` | Ranuras ilimitadas de mochila | OP |

---

## Puntos de Viaje

| Permiso | Ranuras | Por defecto |
| --- | --- | --- |
| `nexusprism.essentials.waypoints.1` | 1 punto de viaje | true |
| `nexusprism.essentials.waypoints.5` | 5 puntos de viaje | — |
| `nexusprism.essentials.waypoints.25` | 25 puntos de viaje | — |
| `nexusprism.essentials.waypoints.unlimited` | Ilimitado | OP |
| `nexusprism.essentials.waypoint` | Acceder a comandos de punto de viaje | true |

---

## Homes

| Permiso | Ranuras | Por defecto |
| --- | --- | --- |
| `nexusprism.essentials.homes.1` | 1 home | true |
| `nexusprism.essentials.homes.3` | 3 homes | — |
| `nexusprism.essentials.homes.10` | 10 homes | — |
| `nexusprism.essentials.homes.unlimited` | Ilimitado | OP |
| `nexusprism.essentials.home` | Usar /home, /sethome, /delhome | true |

---

## Comandos Esenciales

| Permiso | Comando | Por defecto |
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
| `nexusprism.essentials.fly` | `/fly` (propio) | false |
| `nexusprism.essentials.fly.others` | `/fly <jugador>` | OP |
| `nexusprism.essentials.hat` | `/hat` | false |
| `nexusprism.essentials.god` | `/god` (propio) | OP |
| `nexusprism.essentials.god.others` | `/god <jugador>` | OP |
| `nexusprism.essentials.heal` | `/heal` (propio) | OP |
| `nexusprism.essentials.heal.others` | `/heal <jugador>` | OP |
| `nexusprism.essentials.feed` | `/feed` (propio) | OP |
| `nexusprism.essentials.feed.others` | `/feed <jugador>` | OP |
| `nexusprism.essentials.nick` | `/nick` (propio) | false |
| `nexusprism.essentials.nick.others` | `/nick <jugador>` | OP |
| `nexusprism.essentials.afk` | `/afk` | true |
| `nexusprism.essentials.workbench` | `/workbench` | true |
| `nexusprism.essentials.trash` | `/trash` | true |
| `nexusprism.essentials.anvil` | `/anvil` | OP |
| `nexusprism.essentials.grindstone` | `/grindstone` | OP |
| `nexusprism.essentials.stonecutter` | `/stonecutter` | OP |
| `nexusprism.essentials.speed` | `/speed` | OP |
| `nexusprism.essentials.seen` | `/seen` | true |
| `nexusprism.essentials.clearinventory` | `/clearinventory` (propio) | OP |
| `nexusprism.essentials.clearinventory.others` | `/clearinventory <jugador>` | OP |
| `nexusprism.essentials.getpos` | `/getpos` | true |
| `nexusprism.essentials.playtime` | `/playtime` | true |
| `nexusprism.essentials.gamemode` | `/gamemode` | OP |
| `nexusprism.essentials.enderchest` | `/enderchest` (propio) | true |
| `nexusprism.essentials.enderchest.others` | `/enderchest <jugador>` | OP |
| `nexusprism.essentials.repair` | `/repair` | OP |
| `nexusprism.essentials.ext` | `/ext` | OP |
| `nexusprism.essentials.exp` | `/exp` | OP |
| `nexusprism.essentials.worth` | `/worth` | true |
| `nexusprism.essentials.rules` | `/rules` | true |
| `nexusprism.essentials.skull` | `/skull` | OP |
| `nexusprism.essentials.jail.admin` | Gestión de prisión | OP |
| `nexusprism.essentials.backpack` | Comandos de mochila | true |

---

## Economía

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.economy.money` | Ver saldo de dinero | true |
| `nexusprism.economy.credits` | Ver créditos | true |
| `nexusprism.economy.baltop` | Ver tabla de clasificación | true |
| `nexusprism.economy.sell` | Usar /sell | true |
| `nexusprism.economy.admin` | Comandos administrativos de economía | OP |

---

## Clanes

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.clan.use` | Usar comandos de clan | true |
| `nexusprism.clan.admin` | Gestión administrativa de clanes | OP |
| `nexusprism.clan.bypass-protection` | Ignorar territorio de clan | OP |

---

## Seguridad

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.security.cleanworld` | Limpiador de mundo manual | OP |
| `nexusprism.staff.vanish` | Hacerse invisible | OP |
| `nexusprism.staff.vanish.others` | Hacer invisible a otro jugador | OP |
| `nexusprism.staff.vanish.see` | Ver jugadores invisibles | OP |
| `nexusprism.staff.invsee` | Inspeccionar inventarios | OP |
| `nexusprism.staff.spy` | Modo espía de chat | OP |

---

## Chat

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.chat.staff` | Acceder al canal de chat del staff | OP |
| `nexusprism.chat.mute` | Silenciar jugadores | OP |
| `nexusprism.chat.mute.bypass` | Ignorar silenciamiento | false |
| `nexusprism.chat.filter.bypass` | Ignorar filtro de palabras | OP |
| `nexusprism.chat.reload` | Recargar configuración de chat | OP |
| `nexusprism.chat.color` | Usar códigos de color en el chat | OP |

---

## Protecciones & Duelos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.region.use` | Crear y gestionar propias regiones | true |
| `nexusprism.protect.admin` | Gestión administrativa de regiones | OP |
| `nexusprism.duel.use` | Enviar y aceptar duelos | true |

---

## Crystal Defense

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.crystaldefense.use` | Unirse a arenas | true |
| `nexusprism.crystaldefense.admin` | Crear/gestionar arenas | OP |

---

## Votifier

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.vote` | Usar `/vote` | true |
| `nexusprism.vote.top` | Usar `/votetop` | true |

---

## Custom Mobs

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.boss.admin` | Todos los comandos de boss/huevo de aparición | OP |

---

## Dreams

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.dreams.admin` | Comandos administrativos de sueños | OP |

---

## Twitch

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.twitch.use` | Comandos básicos de Twitch | true |
| `nexusprism.twitch.staff` | Aprobar vinculaciones, realizar sorteos | OP |
| `nexusprism.twitch.admin` | Recargar configuración de Twitch | OP |

---

## Silk Spawners

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.silkspawner.use` | Minar spawners con Silk Touch | true |
| `nexusprism.silkspawner.admin` | Comandos administrativos de spawner | OP |

---

## Recetas & Kits

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.recipe` | Usar `/recipe` | true |
| `nexusprism.command.kit` | Usar `/kit` | true |
| `nexusprism.command.vip` | Usar `/vip` | true |
| `nexusprism.kit.*` | Acceder a todos los kits VIP | OP |

---

## Nodos de Nivel de Permiso

Usados internamente para mapear rangos del staff. Configura en `config.yml`:

| Permiso | Rango |
| --- | --- |
| `nexusprism.level.user` | Jugador regular |
| `nexusprism.level.helper` | Asistente |
| `nexusprism.level.moderator` | Moderador |
| `nexusprism.level.admin` | Administrador |
| `nexusprism.level.owner` | Propietario |
