# Módulo Crates

El módulo Crates proporciona **cofres de botín basados en llaves** con animaciones de apertura, efectos de partículas en idle y tablas de recompensas configurables por cofre.

---

## Comandos

| Comando | Permiso | Descripción |
| --- | --- | --- |
| `/crate give <jugador> <cofre> [cantidad]` | `nexusprism.crates.admin` | Dar llaves de cofre a un jugador |
| `/crate keys [jugador]` | `nexusprism.crates.use` | Ver saldo de llaves virtuales |
| `/crate setblock <cofre>` | `nexusprism.crates.admin` | Registrar el bloque apuntado como cofre |
| `/crate removeblock` | `nexusprism.crates.admin` | Desregistrar el bloque apuntado |
| `/crate preview <cofre>` | *(todos los jugadores)* | Vista previa de posibles recompensas |
| `/crate list` | *(todos los jugadores)* | Listar todos los tipos de cofres |
| `/crate reload` | `nexusprism.crates.admin` | Recargar todas las definiciones de cofres |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.crates.admin` | Crear, eliminar y dar cofres | OP |
| `nexusprism.crates.use` | Verificar saldo de llaves | true |

---

## Definición de Cofre (`crates/<id>.yml`)

```yaml
display-name: "&aCofre Común"
block-material: WHITE_SHULKER_BOX
broadcast-wins: false
preview: true

opening:
  mode: SPIN          # SPIN | INSTANT
  firework: false

rewards:
  - type: ITEM
    data: IRON_INGOT
    amount: 8
    weight: 30
    display-name: "&78x Lingote de Hierro"
  - type: MONEY
    data: "500"
    weight: 25
    display-name: "&a$500"
  - type: COMMAND
    data: "give {player} minecraft:diamond 1"
    weight: 5
    display-name: "&bDiamante Bonus"
```
