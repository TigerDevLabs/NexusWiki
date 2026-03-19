# Módulo Esenciales

El módulo Esenciales proporciona **+40 comandos de calidad de vida** que cubren homes, warps, waypoints, teletransporte, detección de AFK, cárcel y comandos utilitarios del día a día.

---

## Homes

Los jugadores pueden establecer homes con nombre y teletransportarse a ellas.

### Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/home [nombre]` | Teletransportarse a una home | `nexusprism.essentials.home` |
| `/home list` | Listar todas las homes | `nexusprism.essentials.home` |
| `/sethome <nombre>` | Establecer home en la posición actual | `nexusprism.essentials.home` |
| `/delhome <nombre>` | Eliminar una home | `nexusprism.essentials.home` |

### Permisos de Slots de Home

| Permiso | Slots |
| --- | --- |
| `nexusprism.essentials.homes.1` | 1 (predeterminado) |
| `nexusprism.essentials.homes.3` | 3 |
| `nexusprism.essentials.homes.10` | 10 |
| `nexusprism.essentials.homes.unlimited` | Ilimitado (OP) |

---

## Warps

Destinos de teletransporte públicos en todo el servidor gestionados por admins.

### Comandos de Warps

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/warp <nombre>` | Teletransportarse a un warp | `nexusprism.essentials.warp.use` |
| `/warp list` | Listar todos los warps | `nexusprism.essentials.warp.use` |
| `/setwarp <nombre>` | Crear un warp (OP) | `nexusprism.essentials.warp.admin` |
| `/delwarp <nombre>` | Eliminar un warp (OP) | `nexusprism.essentials.warp.admin` |

---

## TPA (Solicitudes de Teletransporte)

### Comandos TPA

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/tpa <jugador>` | Enviar solicitud de teletransporte | `nexusprism.essentials.tpa` |
| `/tpaccept` | Aceptar solicitud de teletransporte | `nexusprism.essentials.tpa` |
| `/tpdeny` | Rechazar solicitud de teletransporte | `nexusprism.essentials.tpa` |
| `/tphere <jugador>` | Teletransportar jugador hasta ti (OP) | `nexusprism.essentials.tphere` |
| `/tppos <x> <y> <z>` | Teletransportarse a coordenadas (OP) | `nexusprism.essentials.tppos` |
| `/spawn` | Teletransportarse al spawn | `nexusprism.essentials.spawn` |
| `/setspawn` | Establecer el spawn del servidor (OP) | `nexusprism.essentials.setspawn` |
| `/back` | Volver a la ubicación anterior | `nexusprism.essentials.back` |

### Configuración (`essentials/config.yml`)

```yaml
tpa:
  expiry-seconds: 60       # La solicitud expira tras este tiempo

back:
  save-on-death: true      # Guardar ubicación de muerte para /back
  save-on-any-teleport: false

spawn:
  respawn-at-spawn: false  # Forzar respawn en el spawn (vs. cama)
```

---

## Sistema AFK

### Comandos AFK

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/afk` | Alternar estado AFK | `nexusprism.essentials.afk` |

### Configuración AFK

```yaml
afk:
  idle-seconds: 300        # AFK automático tras 5 minutos inactivo
  broadcast: true          # Anunciar cuando un jugador entra en AFK
```

---

## Cárcel

Los admins pueden enviar jugadores a una ubicación de cárcel predefinida.

### Comandos de Cárcel

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/jail <jugador> [duración]` | Encarcelar a un jugador (OP) | `nexusprism.essentials.jail.admin` |
| `/unjail <jugador>` | Liberar a un jugador (OP) | `nexusprism.essentials.jail.admin` |
| `/setjail` | Establecer ubicación de la cárcel (OP) | `nexusprism.essentials.jail.admin` |

---

## Comandos Utilitarios

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/fly` | Alternar modo vuelo | `nexusprism.essentials.fly` |
| `/fly <jugador>` | Alternar vuelo para otro jugador (OP) | `nexusprism.essentials.fly.others` |
| `/god` | Alternar modo dios | `nexusprism.essentials.god` |
| `/heal` | Curarte a ti mismo (OP) | `nexusprism.essentials.heal` |
| `/feed` | Alimentarte a ti mismo (OP) | `nexusprism.essentials.feed` |
| `/nick <nombre>` | Establecer apodo | `nexusprism.essentials.nick` |
| `/workbench` | Mesa de trabajo portátil | `nexusprism.essentials.workbench` |
| `/trash` | Papelera portátil | `nexusprism.essentials.trash` |
| `/anvil` | Yunque portátil (OP) | `nexusprism.essentials.anvil` |
| `/speed <valor>` | Establecer velocidad de movimiento (OP) | `nexusprism.essentials.speed` |
| `/near` | Listar jugadores cercanos | `nexusprism.essentials.near` |
| `/seen <jugador>` | Última vez visto | `nexusprism.essentials.seen` |
| `/getpos` | Mostrar tus coordenadas | `nexusprism.essentials.getpos` |
| `/playtime` | Verificar tiempo de juego | `nexusprism.essentials.playtime` |
| `/gamemode <modo>` | Cambiar modo de juego (OP) | `nexusprism.essentials.gamemode` |
| `/enderchest` | Abrir tu cofre de ender | `nexusprism.essentials.enderchest` |
| `/repair` | Reparar el ítem sostenido (OP) | `nexusprism.essentials.repair` |
| `/ext` | Apagarte a ti mismo (OP) | `nexusprism.essentials.ext` |
| `/hat` | Usar ítem como sombrero | `nexusprism.essentials.hat` |
| `/rules` | Mostrar reglas del servidor | `nexusprism.essentials.rules` |
| `/worth [ítem]` | Verificar valor de venta | `nexusprism.essentials.worth` |
