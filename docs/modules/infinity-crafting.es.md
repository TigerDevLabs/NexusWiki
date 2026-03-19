# Módulo Infinity Crafting

Infinity Crafting es el **sistema de crafteo multibloques** de NexusPrism. Los jugadores construyen estructuras multibloques físicas en el mundo y las usan como estaciones de crafteo avanzadas. Las recetas se definen íntegramente en YAML.

---

## Descripción General

| Funcionalidad | Descripción |
| --- | --- |
| **Estructuras multibloques** | Estaciones de crafteo construidas a partir de patrones específicos de bloques |
| **Recetas en YAML** | Sin Java necesario — define recetas en `infinity_recipes/` |
| **Interfaz GUI** | Entrada/salida de recetas con arrastrar y soltar mediante GUI de inventario |
| **Bloqueo por investigación** | Las recetas pueden requerir investigación específica para desbloquearse |
| **Integración con máquinas** | Algunas recetas infinity requieren energía o salida de máquinas como ingredientes |

---

## Configuración de Multibloques

Los multibloques son estructuras físicas colocadas en el mundo. Su diseño se define en `multiblocks.yml`.

### Construyendo un Multibloques

1. Reúne los bloques necesarios listados en la definición del multibloques
2. Construye la estructura en la forma exacta mostrada en la guía
3. Haz clic derecho en el bloque controlador para abrir la GUI de crafteo
4. Inserta los ingredientes y recoge el resultado

### Ejemplo de `multiblocks.yml`

```yaml
INFINITY_TABLE:
  display-name: "&bInfinity Crafting Table"
  description: "The core multiblock for Infinity-tier crafting."
  controller: CRAFTING_TABLE
  structure:
    # Definiciones de capas: Y=0 es la base, Y=1 es el medio, etc.
    layers:
      0:
        - "DDD"
        - "DCD"
        - "DDD"
      1:
        - "   "
        - " C "
        - "   "
    legend:
      D: DEEPSLATE_BRICKS
      C: CRAFTING_TABLE   # Bloque controlador
```

---

## Formato YAML de Recetas

Las recetas se colocan en `plugins/NexusPrism/infinity_recipes/` como archivos `.yml` individuales. El nombre del archivo sirve como ID de la receta.

### Receta Shaped (Con Forma)

```yaml
# infinity_recipes/nexus_core.yml
type: SHAPED
station: INFINITY_TABLE
output:
  item: NEXUS_CORE
  amount: 1

shape:
  - "GEG"
  - "EDE"
  - "GEG"

ingredients:
  G: GOLD_INGOT
  E: ENDER_PEARL
  D: DIAMOND

research-required: ADVANCED_METALLURGY    # Bloqueo de investigación opcional
energy-cost: 500                          # Costo de energía opcional (RF/FE)
```

### Receta Shapeless (Sin Forma)

```yaml
# infinity_recipes/star_dust.yml
type: SHAPELESS
station: INFINITY_TABLE
output:
  item: STAR_DUST
  amount: 4

ingredients:
  - GLOWSTONE_DUST
  - GLOWSTONE_DUST
  - BLAZE_POWDER
  - ENDER_PEARL
```

### Receta de Fundición (vía Máquina)

```yaml
# infinity_recipes/copper_ingot.yml
type: MACHINE_SMELT
station: ELECTRIC_FURNACE
output:
  item: COPPER_INGOT
  amount: 1

input:
  item: RAW_COPPER
  amount: 1

energy-cost: 100
processing-ticks: 200
```

### Referencia de Campos

| Campo | Descripción |
| --- | --- |
| `type` | `SHAPED`, `SHAPELESS`, `MACHINE_SMELT` |
| `station` | ID del multibloques requerido para crear esta receta |
| `output.item` | ID del ítem de salida (personalizado de NexusPrism o Material vanilla) |
| `output.amount` | Tamaño de la pila de salida |
| `shape` | Cuadrícula de 3 filas para recetas shaped (3 caracteres por fila) |
| `ingredients` | Mapa de char → ID de ítem (shaped) o lista de IDs de ítems (shapeless) |
| `research-required` | ID de investigación que debe desbloquearse antes de que aparezca esta receta |
| `energy-cost` | Energía (RF) consumida por crafteo |
| `processing-ticks` | Ticks utilizados por recetas de máquina |

---

## Guía en el Juego

Todas las recetas infinity son visibles en la guía del juego. Ábrela con `/nexusprism guide` y navega a la sección de tier **Infinity**.

La guía muestra:

- Estación multibloques requerida
- Lista de ingredientes con cantidades
- Requisito de investigación (si corresponde)
- Costo de energía (si corresponde)

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/recipe <item>` | Mostrar receta(s) de un ítem | `nexusprism.recipe` |
| `/nexusprism guide` | Abrir GUI de la guía de ítems | `nexusprism.command` |
| `/nexusprism reload` | Recargar todas las recetas y multibloques | `nexusprism.admin.reload` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.recipe` | Ver recetas con `/recipe` | true |
| `nexusprism.craft` | Usar estaciones de crafteo | true |
| `nexusprism.admin.reload` | Recargar configuraciones/recetas del plugin | OP |
