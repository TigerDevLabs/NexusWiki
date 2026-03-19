# Módulo Protections

El módulo Protections proporciona **reclamación de regiones por jugadores**, flags de protección configurables y un **sistema de duelos 1v1**.

---

## Reclamación de Regiones

Los jugadores seleccionan dos esquinas de una región cúbica con la varita de selección y la reclaman como su área protegida. Los no-miembros no pueden construir, romper ni interactuar dentro de la región por defecto.

### Cómo Reclamar una Región

1. Sostén un **Hacha Dorada** (varita por defecto)
2. Haz clic izquierdo en una esquina de tu región → haz clic derecho en la esquina opuesta
3. Ejecuta `/region claim <nombre>` para reclamar la selección

### Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/region claim <nombre>` | Reclamar área seleccionada | `nexusprism.region.use` |
| `/region delete <nombre>` | Eliminar una región | `nexusprism.region.use` |
| `/region list` | Listar tus regiones | `nexusprism.region.use` |
| `/region info [nombre]` | Ver detalles de la región | `nexusprism.region.use` |
| `/region addmember <región> <jugador>` | Añadir un miembro | `nexusprism.region.use` |
| `/region removemember <región> <jugador>` | Eliminar un miembro | `nexusprism.region.use` |
| `/region setflag <región> <flag> <valor>` | Establecer una flag | `nexusprism.region.use` |
| `/region flags <región>` | Ver todas las flags | `nexusprism.region.use` |
| `/protect <nombre>` | Protección rápida del chunk actual | `nexusprism.region.use` |
| `/region admin list [jugador]` | Admin: listar todas las regiones | `nexusprism.protect.admin` |
| `/region admin delete <nombre>` | Admin: forzar eliminación de región | `nexusprism.protect.admin` |
| `/region admin setowner <región> <jugador>` | Admin: cambiar propietario | `nexusprism.protect.admin` |

---

## Flags de Región

Las flags controlan qué está y qué no está permitido dentro de una región.

| Flag | Valores | Por defecto | Descripción |
| --- | --- | --- | --- |
| `pvp` | `true` / `false` | `false` | Permitir PvP dentro de la región |
| `build` | `true` / `false` | `false` | Permitir que no-miembros construyan |
| `interact` | `true` / `false` | `false` | Permitir que no-miembros interactúen (cofres, botones…) |
| `mob-spawning` | `true` / `false` | `true` | Permitir que aparezcan mobs |
| `explosions` | `true` / `false` | `false` | Permitir explosiones de TNT / creeper |
| `fire` | `true` / `false` | `false` | Permitir propagación de fuego |
| `greeting` | `<texto>` | — | Mensaje mostrado al entrar a la región |
| `farewell` | `<texto>` | — | Mensaje mostrado al salir de la región |

```bash
# Ejemplo: habilitar PvP en una región de arena
/region setflag my-arena pvp true
/region setflag my-arena greeting "&cYou entered a PvP zone!"
```

---

## Configuración (`protections/config.yml`)

```yaml
selection-wand: GOLDEN_AXE     # Ítem usado para seleccionar esquinas de región

max-regions-per-player: 5      # Máximo de regiones por jugador
max-region-volume: 100000      # Tamaño máximo de región en bloques

pvp-in-wilderness: true        # Permitir PvP fuera de cualquier región

duel-request-timeout-seconds: 30

economy:
  enabled: false               # Cobrar a los jugadores por reclamar regiones
  base-cost: 100.0             # Tarifa fija por reclamación
  cost-per-block: 0.01         # Costo adicional × volumen de región
  refund-percent: 50           # % reembolsado al eliminar una región
```

---

## Sistema de Duelos

El sistema de duelos permite a los jugadores desafiarse mutuamente a una pelea 1v1 en una arena de duelos segura. Las muertes durante los duelos no sueltan ítems.

### Comandos de Duelo

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/duel <jugador>` | Desafiar a un jugador a un duelo | `nexusprism.duel.use` |
| `/duel accept` | Aceptar un desafío de duelo | `nexusprism.duel.use` |
| `/duel deny` | Rechazar un desafío de duelo | `nexusprism.duel.use` |
| `/duel spectate <jugador>` | Espectador de un duelo | `nexusprism.duel.use` |
| `/duel stats` | Ver tus estadísticas de duelo | `nexusprism.duel.use` |
| `/duel setarena` | Establecer arena de duelo en tu ubicación | `nexusprism.protect.admin` |

### Reglas de Duelo

- Las solicitudes de duelo expiran después de `duel-request-timeout-seconds` (por defecto: 30)
- Los ítems se guardan y restauran al terminar el duelo
- El ganador recibe recompensas configurables (definidas en el puente de economía)
- Ambos jugadores son teletransportados a la arena de duelos al aceptar

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.region.use` | Crear y gestionar propias regiones | true |
| `nexusprism.protect.admin` | Gestión administrativa de regiones | OP |
| `nexusprism.bypass.protection` | Ignorar todas las protecciones de región | OP |
| `nexusprism.duel.use` | Desafiar y aceptar duelos | true |
