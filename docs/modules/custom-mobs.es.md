# Módulo Custom Mobs

El módulo Custom Mobs permite a los administradores de servidores definir **bosses basados en YAML** con salud, equipamiento, efectos de poción, formas de IA, tablas de loot y huevos de aparición personalizados — todo sin escribir código Java.

---

## Descripción General

| Funcionalidad | Descripción |
| --- | --- |
| **Definiciones en YAML** | Cada boss es un único archivo `.yml` en `custommobs/bosses/` |
| **Formas de IA** | Los bosses alternan entre estilos de combate (SWORD, DAGGER, GLADIUS…) |
| **Equipamiento** | Conjunto completo de armadura y armas |
| **Efectos de Poción** | Efectos permanentes aplicados al boss |
| **Tablas de Loot** | Drops garantizados y drops por probabilidad |
| **Huevos de Aparición** | Huevos de aparición personalizados creados o entregados con `/bossegg` |
| **Persistente** | Los bosses sobreviven a los reinicios del servidor |

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/boss spawn <id>` | Invocar un boss en tu ubicación | `nexusprism.boss.admin` |
| `/boss spawn <id> <mundo> <x> <y> <z>` | Invocar en coordenadas | `nexusprism.boss.admin` |
| `/boss list` | Listar todos los bosses registrados | `nexusprism.boss.admin` |
| `/boss info <id>` | Mostrar detalles de la definición del boss | `nexusprism.boss.admin` |
| `/boss kill <id>` | Matar todas las instancias activas de un boss | `nexusprism.boss.admin` |
| `/bossegg give <jugador> <id>` | Dar un huevo de aparición de boss | `nexusprism.boss.admin` |
| `/bossegg <id>` | Obtener tu propio huevo de aparición de boss | `nexusprism.boss.admin` |

---

## Formato YAML de Boss

Los archivos de boss se colocan en `plugins/NexusPrism/custommobs/bosses/<id>.yml`.

### Ejemplo Completo (`white_death.yml`)

```yaml
name: "§uEchoes §tof §sthe §bWhite §fDeath"
entity: WITHER_SKELETON
health: 200.0
persistent: true

equipment:
  helmet:     GOLDEN_HELMET
  chestplate: GOLDEN_CHESTPLATE
  leggings:   GOLDEN_LEGGINGS
  boots:      GOLDEN_BOOTS
  main_hand:  DIAMOND_SWORD
  off_hand:   SHIELD

potion_effects:
  - SPEED:2

ai_forms:
  - type: SWORD
    weight: 5
  - type: DAGGER
    weight: 3
  - type: GLADIUS
    weight: 2

loot:
  always:
    - SHADOW_SHARD:1
    - SNOWBALL:5
    - ENCHANTED_BOOK:1
  chance:
    - item: FROZEN_DAGGER
      chance: 0.20
    - item: GLADIUS
      chance: 0.10

form_switch_interval_ticks: 300
```

### Referencia de Campos

| Campo | Tipo | Descripción |
| --- | --- | --- |
| `name` | String | Nombre de visualización con códigos de color `&`/`§` |
| `entity` | EntityType de Bukkit | Tipo de entidad base (ej: `WITHER_SKELETON`, `ZOMBIE`) |
| `health` | Double | Salud máxima en medios corazones |
| `persistent` | Boolean | Si `true`, el boss persiste tras descarga de chunks/reinicios |
| `equipment.*` | Material | Ranuras de equipamiento: `helmet`, `chestplate`, `leggings`, `boots`, `main_hand`, `off_hand` |
| `potion_effects` | Lista | Efectos permanentes en formato `EFECTO:AMPLIFICADOR` |
| `ai_forms` | Lista | Estilos de combate entre los que alterna el boss |
| `ai_forms[].type` | String | ID de forma de IA (`SWORD`, `DAGGER`, `GLADIUS`, etc.) |
| `ai_forms[].weight` | Integer | Peso relativo para selección aleatoria |
| `loot.always` | Lista | Drops garantizados en formato `ID_ITEM:cantidad` |
| `loot.chance` | Lista | Drops por probabilidad con `item` y `chance` (0.0–1.0) |
| `form_switch_interval_ticks` | Integer | Ticks entre cambios de forma de IA (300 = 15 segundos) |

### Ítems de Loot

Tanto nombres de `Material` de Bukkit como IDs de ítems personalizados de NexusPrism pueden usarse en las tablas de loot:

```yaml
loot:
  always:
    - DIAMOND:3           # Material vanilla
    - NEXUS_SHARD:1       # ID de ítem personalizado de NexusPrism
  chance:
    - item: BOSS_TROPHY
      chance: 0.05        # 5% de probabilidad de drop
```

---

## Tipos de Forma de IA

| Forma | Descripción |
| --- | --- |
| `SWORD` | Cuerpo a cuerpo agresivo, se lanza hacia el objetivo |
| `DAGGER` | Ataques rápidos de hit-and-run |
| `GLADIUS` | Ataque equilibrado con golpes de escudo |

Las formas de IA personalizadas pueden añadirse creando módulos addon usando la `nexusprism-api`.

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.boss.admin` | Todos los comandos de boss y huevo de aparición | OP |

---

## Uso del Huevo de Aparición

Los huevos de aparición entregados con `/bossegg give <jugador> <id>` pueden usarse con clic derecho en el mundo para invocar al boss. El ítem huevo muestra el nombre del boss y una vista previa de su salud en el lore.
