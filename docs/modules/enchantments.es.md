# Módulo Enchantments

El módulo Enchantments añade **175 encantamientos personalizados** en 6 niveles de rareza y 10 tipos de disparador. Todos los encantamientos se definen en `enchants/config.yml`.

---

## Rarezas

| Rareza | Color | Costo en XP | Peso |
| --- | --- | --- | --- |
| **Común** | Blanco `§f` | 3 XP | 100 |
| **Poco común** | Verde `§a` | 8 XP | 50 |
| **Raro** | Azul `§9` | 15 XP | 20 |
| **Épico** | Morado `§5` | 25 XP | 8 |
| **Legendario** | Dorado `§6` | 40 XP | 3 |
| **Mítico** | Rojo `§c` | 60 XP | 1 |

---

## Tipos de Disparador

| Disparador | Cuándo se activa |
| --- | --- |
| `ON_HIT` | Al infligir daño cuerpo a cuerpo |
| `ON_KILL` | Al matar una entidad |
| `ON_MINE` | Al romper un bloque |
| `ON_BREAK` | Cuando el ítem está a punto de romperse |
| `ON_DEATH` | Al morir |
| `ON_DAMAGE_TAKEN` | Al recibir daño |
| `PASSIVE` | Se ejecuta continuamente en una tarea de tick |
| `ON_JUMP` | Al saltar |
| `ON_SHOOT` | Al disparar un proyectil |
| `VOID` | Al caer por debajo de Y=0 |

---

## Comandos

Todos requieren `nexusprism.enchantments.admin`.

| Comando | Descripción |
| --- | --- |
| `/enchant list` | Listar todos los encantamientos |
| `/enchant info <id>` | Ver detalles del encantamiento |
| `/enchant give <jugador> <id> [nivel]` | Dar libro de encantamiento |
| `/enchant apply <id> [nivel]` | Aplicar encantamiento al ítem en mano |
| `/enchant remove <id>` | Eliminar encantamiento del ítem en mano |
| `/enchant reload` | Recargar configuración |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.enchantments.admin` | Todos los comandos de gestión | OP |
