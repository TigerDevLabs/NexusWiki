# Módulo Dreams

El módulo Dreams activa una **experiencia cinematográfica al dormir** cuando un jugador se acuesta en una cama. Con una probabilidad configurable, los jugadores son transportados a una cutscene de sueño o pesadilla antes de despertar en su ubicación original.

---

## Cómo Funciona

1. Un jugador se acuesta en una cama
2. Hay una probabilidad configurable (`dream_trigger_chance`) de que se active una cutscene
3. El jugador es teletransportado al mundo de sueños o pesadillas
4. Efectos de poción, mensajes y un temporizador crean una secuencia atmosférica
5. Tras la duración, el jugador regresa a su ubicación original en la cama

---

## Sueño vs. Pesadilla

| Tipo | Probabilidad | Efectos por Defecto | Ambiente |
| --- | --- | --- | --- |
| **Sueño** | 40% (de la probabilidad de activación) | Visión Nocturna, Lentitud | Pacífico, etéreo |
| **Pesadilla** | 60% (de la probabilidad de activación) | Ceguera, Náusea, Lentitud | Oscuro, perturbador |

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/dreams reload` | Recargar configuración de sueños | `nexusslime.dreams.admin` |
| `/dreams trigger <player>` | Forzar un sueño para un jugador | `nexusslime.dreams.admin` |
| `/dreams trigger <player> nightmare` | Forzar una pesadilla | `nexusslime.dreams.admin` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.dreams.admin` | Comandos administrativos de sueños | OP |

---

## Configuración (`dreams/config.yml`)

```yaml
# Probabilidad base (%) de que dormir active la cutscene
dream_trigger_chance: 25

dimension:
  enabled: true

  nightmare:
    world: ""              # Nombre del mundo — dejar vacío para usar el mundo principal
    x: 0.0
    y: 64.0
    z: 0.0
    yaw: 0.0
    pitch: 0.0
    chance: 60             # Probabilidad (%) de pesadilla frente a sueño
    duration: 300          # Duración en ticks (300 = 15 segundos)
    effects:
      - BLINDNESS:1
      - NAUSEA:1
      - SLOWNESS:1

  dreams:
    world: ""
    x: 0.0
    y: 64.0
    z: 0.0
    yaw: 0.0
    pitch: 0.0
    duration: 300
    effects:
      - NIGHT_VISION:1
      - SLOWNESS:0

messages:
  dream:
    flashback_init:   "&9You drift off peacefully..."
    flashback_middle: "&9So peaceful..."
    end:              "&7You slowly wake up."
  nightmare:
    flashback_init:   "&8A dark memory surfaces..."
    flashback_middle: "&8You can't look away..."
    flashback_scream: "&8!"
    end:              "&7You wake up in a cold sweat."
```

### Campos de Configuración

| Campo | Descripción |
| --- | --- |
| `dream_trigger_chance` | Porcentaje de probabilidad de que un sueño active el sistema. |
| `dimension.enabled` | Activa la cutscene de teletransporte. |
| `nightmare.chance` | De las cutscenes activadas, qué % son pesadillas. |
| `duration` | Cuánto tiempo (ticks) permanece el jugador en la dimensión. 20 ticks = 1 segundo. |
| `effects` | Lista de efectos de poción en formato `EFECTO:AMPLIFICADOR` (amplificador 0 = nivel I). |
| `messages.*` | Mensajes cinematográficos mostrados durante la secuencia. Admite códigos de color `&`. |

---

## Configurar Mundos de Sueños

Para la mejor experiencia, crea mundos planos o atmosféricos dedicados para sueños y pesadillas:

1. Crea el mundo (con un plugin de gestión de mundos o Multiverse)
2. Establece las coordenadas en `dreams/config.yml` bajo `dimension.dreams.world` y `dimension.nightmare.world`
3. Construye escenarios atmosféricos en esas coordenadas
4. Recarga con `/dreams reload`

!!! tip
    Deja `world` vacío para usar el mundo principal. Los jugadores serán teletransportados a las coordenadas XYZ configuradas en el mundo por defecto.

---

## Integración con el Arco del Sacrificio

Cuando el módulo **Events** está activo, el **Arco del Sacrificio** puede suprimir por completo la cutscene normal de sueños.

Si la racha de supervivencia de Luna de Sangre de un jugador alcanza un múltiplo de 7 (7, 14, 21, 28...) y el jugador entra en una cama, el Arco del Sacrificio intercepta el evento de dormir **antes** de que se elija ningún sueño o pesadilla. En su lugar se muestra una GUI de elección.

!!! info
    Este comportamiento está controlado por `DreamsManager.SACRIFICE_HOOK` — un hook establecido por el módulo Events al cargarse y eliminado al apagarse. Si el módulo Events está desactivado, los sueños funcionan exactamente como se describe arriba, sin cambios.

Consulta el [módulo Events](events.md) para más detalles sobre el Arco del Sacrificio.
