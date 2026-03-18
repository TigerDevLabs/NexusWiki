# Módulo TAB

El módulo TAB personaliza la **lista de jugadores** (overlay TAB) con encabezados y pies de página formateados, prefijo de rango de LuckPerms, indicador de ping en color, marcador animado y personalización del MOTD.

---

## Funcionalidades

| Funcionalidad | Descripción |
| --- | --- |
| **Encabezado / Pie de página** | Encabezado y pie de página animados con soporte para PlaceholderAPI |
| **Formato de nombre** | Los nombres en la lista TAB muestran el prefijo y sufijo del rango de LuckPerms |
| **Indicador de ping** | Ping en color junto al nombre de cada jugador |
| **Marcador** | Marcador lateral por jugador con líneas configurables y placeholders de PAPI |
| **Personalización del MOTD** | Descripción del servidor configurable globalmente |

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/ntab reload` | Recargar configuración del TAB | `nexusslime.tab.admin` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.tab.admin` | Recargar configuración del TAB | OP |

---

## Configuración (`tab/config.yml`)

```yaml
tab:
  enabled: true

  header:
    - ""
    - "&b&lNexusSlime &8— &7Skyblock"
    - ""
  footer:
    - ""
    - "&7En línea: &f%server_online% &8/ &f%server_max_players%"
    - "&7Ping: &f%player_ping%ms"
    - ""

  name-format: "{prefix}&f{name}{suffix}"

  ping-display:
    enabled: true
    format: "&8[{ping}ms]"
    thresholds:
      good: 80
      medium: 150

scoreboard:
  enabled: true
  title: "&b&lNexusSlime"
  update-ticks: 20
  lines:
    - ""
    - "&7Jugador: &f%player_name%"
    - "&7Dinero: &a$%nexusslime_money%"
    - "&7Clan: &b%nexusslime_clan_name%"
    - ""
    - "&eplay.nexusslime.net"
    - ""

motd:
  enabled: false
  lines:
    - "&b&lNexusSlime &r&7— Skyblock MMO"
    - "&7¡Únete y explora!"
```

---

## PlaceholderAPI

El módulo TAB funciona con cualquier placeholder de PlaceholderAPI en el encabezado, pie de página y líneas del marcador. Consulta la [referencia de PlaceholderAPI](../reference/placeholders.md) para ver todos los placeholders `%nexusslime_*%` disponibles.
