# Módulo Structures

El módulo Structures **inyecta botín personalizado** en los cofres de estructuras vanilla. Cuando el servidor genera botín para cualquier estructura soportada, el módulo añade (o reemplaza) el contenido de los cofres con ítems definidos en `structures/loot-tables.yml`.

---

## Estructuras Soportadas

| Estructura | Inyección por defecto |
| --- | --- |
| `minecraft:dungeon` | Pergamino de Investigación (Básico) |
| `minecraft:mineshaft` | Pergamino de Investigación (Básico) |
| `minecraft:desert_pyramid` | Pergamino de Investigación (Básico) |
| `minecraft:jungle_temple` | Pergamino de Investigación (Básico) |
| `minecraft:ocean_ruin` | Pergamino de Investigación (Básico) |
| `minecraft:shipwreck` | Pergamino de Investigación (Básico) |
| `minecraft:pillager_outpost` | Pergamino de Investigación (Básico) |
| `minecraft:stronghold` | Pergamino de Investigación (Avanzado) |
| `minecraft:woodland_mansion` | Pergamino de Investigación (Avanzado) |
| `minecraft:bastion_remnant` | Pergamino de Investigación (Avanzado) |
| `minecraft:end_city` | Pergamino de Investigación (Infinito) |

---

## Configuración (`structures/loot-tables.yml`)

```yaml
minecraft:dungeon:
  mode: APPEND      # APPEND | REPLACE
  rolls:
    min: 1
    max: 2
  items:
    - material: EMERALD
      weight: 40
      amount:
        min: 1
        max: 5
    - nexusslime-item: RESEARCH_PARCHMENT_BASIC
      weight: 5
      amount:
        min: 1
        max: 1
```
