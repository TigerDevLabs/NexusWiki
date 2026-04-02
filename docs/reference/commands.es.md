# Referencia de Comandos

Lista completa de todos los comandos registrados por NexusPrism, organizados por módulo.

**Leyenda:**

- `<arg>` — argumento requerido
- `[arg]` — argumento opcional
- `(OP)` — solo operadores por defecto
- `(true)` — disponible para todos los jugadores por defecto

---

## Core / Plugin

| Comando | Alias | Descripción | Permiso |
| --- | --- | --- | --- |
| `/nexusprism help` | `/ns`, `/nexus`, `/slime` | Mostrar ayuda | `nexusprism.command` |
| `/nexusprism info` | | Versión y estado del plugin | `nexusprism.command` |
| `/nexusprism reload` | | Recargar todas las configuraciones | `nexusprism.admin.reload` |
| `/nexusprism give <player> <item>` | | Dar un ítem personalizado | `nexusprism.admin.give` |
| `/nexusprism guide` | | Abrir GUI de la guía de ítems | `nexusprism.command` |
| `/nexusprism modules` | | Listar todos los módulos cargados | `nexusprism.command` |
| `/nexusprism machine info <id>` | | Detalles de la máquina | `nexusprism.command` |
| `/nexusprism machine list` | | Listar todas las máquinas | `nexusprism.command` |
| `/nexusprism energy info <x,y,z>` | | Información del nodo de energía | `nexusprism.command` |
| `/nexusprism energy network` | | Ver red de energía | `nexusprism.command` |
| `/research` | | Ver progreso de investigación | `nexusprism.research` |
| `/research list [tier]` | | Listar investigaciones por tier | `nexusprism.research` |
| `/research <item-id>` | | Verificar investigación específica | `nexusprism.research` |
| `/nexusprism research all <player>` | | Desbloquear todas las investigaciones para un jugador | `nexusprism.research.admin` |
| `/nexusprism research tier <player> <tier>` | | Desbloquear todas las investigaciones de un tier | `nexusprism.research.admin` |
| `/nexusprism research entry <player> <entry-id>` | | Desbloquear una entrada de investigación específica | `nexusprism.research.admin` |
| `/recipe <item>` | | Mostrar receta(s) de crafteo | `nexusprism.recipe` |

---

## Mochilas & Puntos de Viaje

| Comando | Alias | Descripción | Permiso |
| --- | --- | --- | --- |
| `/backpack open [id]` | | Abrir tu mochila | `nexusprism.essentials.backpack` |
| `/backpack list` | | Listar todas las mochilas | `nexusprism.essentials.backpack` |
| `/waypoint create <name>` | `/wp` | Crear un punto de viaje | `nexusprism.essentials.waypoint` |
| `/waypoint delete <name>` | `/wp` | Eliminar un punto de viaje | `nexusprism.essentials.waypoint` |
| `/waypoint list` | `/wp` | Listar todos los puntos de viaje | `nexusprism.essentials.waypoint` |
| `/waypoint tp <name>` | `/wp` | Teletransportarse a punto de viaje | `nexusprism.essentials.waypoint` |
| `/waypoint info <name>` | `/wp` | Información del punto de viaje | `nexusprism.essentials.waypoint` |

---

## Esenciales — Homes

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/home [name]` | Teletransportarse a un home | `nexusprism.essentials.home` |
| `/home list` | Listar todos los homes | `nexusprism.essentials.home` |
| `/sethome <name>` | Establecer home en la ubicación actual | `nexusprism.essentials.home` |
| `/delhome <name>` | Eliminar un home | `nexusprism.essentials.home` |

---

## Esenciales — Warps

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/warp <name>` | Teletransportarse a un warp | `nexusprism.essentials.warp.use` |
| `/warp list` | Listar todos los warps | `nexusprism.essentials.warp.use` |
| `/setwarp <name>` | Crear un warp (OP) | `nexusprism.essentials.warp.admin` |
| `/delwarp <name>` | Eliminar un warp (OP) | `nexusprism.essentials.warp.admin` |

---

## Esenciales — Teletransporte

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/tpa <player>` | Enviar solicitud de teletransporte | `nexusprism.essentials.tpa` |
| `/tpaccept` | Aceptar solicitud de teletransporte | `nexusprism.essentials.tpa` |
| `/tpdeny` | Rechazar solicitud de teletransporte | `nexusprism.essentials.tpa` |
| `/tphere <player>` | Convocar un jugador (OP) | `nexusprism.essentials.tphere` |
| `/tppos <x> <y> <z>` | Teletransportarse a coordenadas (OP) | `nexusprism.essentials.tppos` |
| `/spawn` | Teletransportarse al spawn | `nexusprism.essentials.spawn` |
| `/setspawn` | Establecer spawn del servidor (OP) | `nexusprism.essentials.setspawn` |
| `/back` | Regresar a la ubicación anterior | `nexusprism.essentials.back` |

---

## Esenciales — Utilidades

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/afk` | Alternar AFK | `nexusprism.essentials.afk` |
| `/fly` | Alternar vuelo (propio) | `nexusprism.essentials.fly` |
| `/fly <player>` | Alternar vuelo (otro, OP) | `nexusprism.essentials.fly.others` |
| `/god` | Alternar modo dios | `nexusprism.essentials.god` |
| `/god <player>` | Alternar dios (otro, OP) | `nexusprism.essentials.god.others` |
| `/heal` | Curarse a sí mismo (OP) | `nexusprism.essentials.heal` |
| `/heal <player>` | Curar a otro (OP) | `nexusprism.essentials.heal.others` |
| `/feed` | Alimentarse a sí mismo (OP) | `nexusprism.essentials.feed` |
| `/feed <player>` | Alimentar a otro (OP) | `nexusprism.essentials.feed.others` |
| `/nick <name>` | Establecer apodo | `nexusprism.essentials.nick` |
| `/nick <player> <name>` | Establecer apodo (otro, OP) | `nexusprism.essentials.nick.others` |
| `/hat` | Usar ítem como sombrero | `nexusprism.essentials.hat` |
| `/speed <value>` | Establecer velocidad de caminar/volar (OP) | `nexusprism.essentials.speed` |
| `/workbench` | Banco de trabajo portátil | `nexusprism.essentials.workbench` |
| `/anvil` | Yunque portátil (OP) | `nexusprism.essentials.anvil` |
| `/grindstone` | Piedra de afilar portátil (OP) | `nexusprism.essentials.grindstone` |
| `/stonecutter` | Cortadora de piedra portátil (OP) | `nexusprism.essentials.stonecutter` |
| `/trash` | Papelera portátil | `nexusprism.essentials.trash` |
| `/near` | Listar jugadores cercanos | `nexusprism.essentials.near` |
| `/seen <player>` | Información de última conexión | `nexusprism.essentials.seen` |
| `/getpos` | Mostrar coordenadas | `nexusprism.essentials.getpos` |
| `/playtime` | Verificar tiempo de juego | `nexusprism.essentials.playtime` |
| `/gamemode <mode>` | Cambiar modo de juego (OP) | `nexusprism.essentials.gamemode` |
| `/enderchest` | Abrir cofre del End | `nexusprism.essentials.enderchest` |
| `/enderchest <player>` | Abrir cofre del End de otro (OP) | `nexusprism.essentials.enderchest.others` |
| `/clearinventory` | Limpiar propio inventario (OP) | `nexusprism.essentials.clearinventory` |
| `/clearinventory <player>` | Limpiar inventario de otro (OP) | `nexusprism.essentials.clearinventory.others` |
| `/repair` | Reparar ítem en mano (OP) | `nexusprism.essentials.repair` |
| `/ext` | Apagarse a sí mismo (OP) | `nexusprism.essentials.ext` |
| `/exp <amount>` | Dar XP (OP) | `nexusprism.essentials.exp` |
| `/skull [player]` | Obtener cabeza de jugador (OP) | `nexusprism.essentials.skull` |
| `/rules` | Mostrar reglas del servidor | `nexusprism.essentials.rules` |
| `/worth [item]` | Valor de venta del ítem | `nexusprism.essentials.worth` |

---

## Esenciales — Prisión

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/jail <player> [duration]` | Encarcelar a un jugador (OP) | `nexusprism.essentials.jail.admin` |
| `/unjail <player>` | Liberar a un jugador (OP) | `nexusprism.essentials.jail.admin` |
| `/setjail` | Establecer ubicación de la prisión (OP) | `nexusprism.essentials.jail.admin` |

---

## Economía

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/money [player]` | Verificar saldo | `nexusprism.economy.money` |
| `/baltop` | Top 10 más ricos | `nexusprism.economy.baltop` |
| `/sell hand` | Vender ítem en mano | `nexusprism.economy.sell` |
| `/sell all` | Vender todos los ítems vendibles | `nexusprism.economy.sell` |
| `/sell inventory` | Vender inventario completo | `nexusprism.economy.sell` |
| `/worth [item]` | Verificar valor de venta | `nexusprism.essentials.worth` |
| `/eco give <player> <amount>` | Dar dinero (OP) | `nexusprism.economy.admin` |
| `/eco take <player> <amount>` | Quitar dinero (OP) | `nexusprism.economy.admin` |
| `/eco set <player> <amount>` | Establecer saldo (OP) | `nexusprism.economy.admin` |
| `/eco reset <player>` | Resetear saldo (OP) | `nexusprism.economy.admin` |

---

## Clanes

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/clan create <name> <tag>` | Crear un clan | `nexusprism.clan.use` |
| `/clan disband` | Disolver clan | `nexusprism.clan.use` |
| `/clan invite <player>` | Invitar a un jugador | `nexusprism.clan.use` |
| `/clan join <name>` | Unirse a un clan | `nexusprism.clan.use` |
| `/clan leave` | Salir del clan | `nexusprism.clan.use` |
| `/clan kick <player>` | Expulsar a un miembro | `nexusprism.clan.use` |
| `/clan promote <player>` | Ascender a oficial | `nexusprism.clan.use` |
| `/clan demote <player>` | Degradar a miembro | `nexusprism.clan.use` |
| `/clan info [name]` | Información del clan | `nexusprism.clan.use` |
| `/clan list` | Listar todos los clanes | `nexusprism.clan.use` |
| `/clan chat` | Alternar chat de clan | `nexusprism.clan.use` |
| `/clan claim` | Reclamar chunk actual | `nexusprism.clan.use` |
| `/clan unclaim` | Liberar chunk actual | `nexusprism.clan.use` |
| `/clan map` | Mostrar mapa de territorio | `nexusprism.clan.use` |
| `/clan chest` | Abrir cofre del clan | `nexusprism.clan.use` |
| `/clan upgrade` | Abrir menú de mejoras | `nexusprism.clan.use` |
| `/clan top` | Clasificación de clanes | `nexusprism.clan.use` |
| `/clan admin disband <name>` | Forzar disolución (OP) | `nexusprism.clan.admin` |
| `/clan admin unclaim <name>` | Forzar liberación (OP) | `nexusprism.clan.admin` |

---

## Seguridad & Staff

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/register <password> <confirm>` | Registrar cuenta | *(todos)* |
| `/login <password>` | Iniciar sesión | *(todos)* |
| `/changepassword <old> <new>` | Cambiar contraseña | *(autenticado)* |
| `/vanish` | Alternar invisibilidad (OP) | `nexusprism.staff.vanish` |
| `/vanish <player>` | Hacer invisible a otro (OP) | `nexusprism.staff.vanish.others` |
| `/invsee <player>` | Inspeccionar inventario (OP) | `nexusprism.staff.invsee` |
| `/spy` | Alternar espía de chat (OP) | `nexusprism.staff.spy` |
| `/cleanworld` | Ejecutar limpiador de mundo (OP) | `nexusprism.security.cleanworld` |

---

## Discord

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/discord` | Enlace de invitación de Discord | *(todos)* |
| `/discord link` | Iniciar vinculación de cuenta | *(todos)* |
| `/discord unlink` | Desvincular cuenta | *(todos)* |
| `/discord info` | Mostrar cuenta vinculada | *(todos)* |
| `/discordrr` | Gestionar roles de reacción (OP) | `nexusprism.admin` |

---

## Protecciones & Duelos

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/region claim <name>` | Reclamar área seleccionada | `nexusprism.region.use` |
| `/region delete <name>` | Eliminar región | `nexusprism.region.use` |
| `/region list` | Listar tus regiones | `nexusprism.region.use` |
| `/region info [name]` | Detalles de la región | `nexusprism.region.use` |
| `/region addmember <region> <player>` | Añadir miembro | `nexusprism.region.use` |
| `/region removemember <region> <player>` | Eliminar miembro | `nexusprism.region.use` |
| `/region setflag <region> <flag> <val>` | Establecer una flag | `nexusprism.region.use` |
| `/region flags <region>` | Ver flags | `nexusprism.region.use` |
| `/protect <name>` | Protección rápida de chunk | `nexusprism.region.use` |
| `/region admin list` | Admin: todas las regiones (OP) | `nexusprism.protect.admin` |
| `/region admin delete <name>` | Admin: eliminar región (OP) | `nexusprism.protect.admin` |
| `/duel <player>` | Desafiar a duelo | `nexusprism.duel.use` |
| `/duel accept` | Aceptar duelo | `nexusprism.duel.use` |
| `/duel deny` | Rechazar duelo | `nexusprism.duel.use` |
| `/duel spectate <player>` | Espectador de duelo | `nexusprism.duel.use` |
| `/duel stats` | Estadísticas de duelo | `nexusprism.duel.use` |
| `/duel setarena` | Establecer arena de duelo (OP) | `nexusprism.protect.admin` |

---

## Crystal Defense

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/crystal join <arena>` | Unirse a una arena | `nexusprism.crystaldefense.use` |
| `/crystal leave` | Salir de la arena | `nexusprism.crystaldefense.use` |
| `/crystal list` | Listar arenas | `nexusprism.crystaldefense.use` |
| `/crystal status` | Oleada y HP del cristal | `nexusprism.crystaldefense.use` |
| `/crystal create <name>` | Crear arena (OP) | `nexusprism.crystaldefense.admin` |
| `/crystal delete <name>` | Eliminar arena (OP) | `nexusprism.crystaldefense.admin` |
| `/crystal setcrystal <arena>` | Establecer ubicación del cristal (OP) | `nexusprism.crystaldefense.admin` |
| `/crystal setspawn <arena>` | Establecer spawn (OP) | `nexusprism.crystaldefense.admin` |
| `/crystal start [arena]` | Forzar inicio (OP) | `nexusprism.crystaldefense.admin` |
| `/crystal stop [arena]` | Detener juego (OP) | `nexusprism.crystaldefense.admin` |
| `/crystal reload` | Recargar configuraciones (OP) | `nexusprism.crystaldefense.admin` |

---

## Votifier

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/vote` | Mostrar enlaces de votación y racha | `nexusprism.vote` |
| `/votetop` | Clasificación de votos | `nexusprism.vote.top` |

---

## Custom Mobs

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/boss spawn <id>` | Invocar un boss | `nexusprism.boss.admin` |
| `/boss spawn <id> <w> <x> <y> <z>` | Invocar en coordenadas | `nexusprism.boss.admin` |
| `/boss list` | Listar todos los bosses | `nexusprism.boss.admin` |
| `/boss info <id>` | Definición del boss | `nexusprism.boss.admin` |
| `/boss kill <id>` | Matar todas las instancias del boss | `nexusprism.boss.admin` |
| `/bossegg give <player> <id>` | Dar huevo de aparición | `nexusprism.boss.admin` |

---

## Dreams

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/dreams reload` | Recargar configuración | `nexusprism.dreams.admin` |
| `/dreams trigger <player>` | Forzar sueño | `nexusprism.dreams.admin` |
| `/dreams trigger <player> nightmare` | Forzar pesadilla | `nexusprism.dreams.admin` |

---

## Twitch

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/twitch link <username>` | Iniciar vinculación | `nexusprism.twitch.use` |
| `/twitch unlink` | Desvincular cuenta | `nexusprism.twitch.use` |
| `/twitch status` | Estado de vinculación | `nexusprism.twitch.use` |
| `/twitch approve <player>` | Aprobar vinculación (OP) | `nexusprism.twitch.staff` |
| `/twitch reject <player>` | Rechazar vinculación (OP) | `nexusprism.twitch.staff` |
| `/twitch pending` | Solicitudes pendientes (OP) | `nexusprism.twitch.staff` |
| `/twitch giveaway <streamer>` | Realizar sorteo (OP) | `nexusprism.twitch.staff` |
| `/twitch reload` | Recargar configuración (OP) | `nexusprism.twitch.admin` |
