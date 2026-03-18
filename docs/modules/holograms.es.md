# Módulo Holograms

El módulo Holograms crea **textos flotantes y displays de ítems** en el mundo, usando entidades `TextDisplay` e `ItemDisplay`. Todos los hologramas se definen en `holograms.yml` y sobreviven a reinicios del servidor.

---

## Tipos de Línea

| Tipo | Descripción |
| --- | --- |
| `TEXT` | Línea de texto formateado. Soporta códigos de color `&` y PlaceholderAPI. |
| `ITEM` | Ícono de ítem flotante (cualquier `Material`). |
| `HEAD` | Cabeza de jugador (skin obtenida de forma asíncrona). |

---

## Comandos

Todos los subcomandos requieren `nexusslime.holograms.admin`.

| Comando | Descripción |
| --- | --- |
| `/holo create <id>` | Crear un holograma en tu ubicación |
| `/holo delete <id>` | Eliminar un holograma |
| `/holo addline <id> text <texto…>` | Agregar una línea de texto |
| `/holo addline <id> item <MATERIAL>` | Agregar una línea de display de ítem |
| `/holo addline <id> head <jugador>` | Agregar una línea de cabeza de jugador |
| `/holo setline <id> <línea#> <texto…>` | Reemplazar una línea de texto (índice base 0) |
| `/holo removeline <id> <línea#>` | Eliminar una línea (índice base 0) |
| `/holo move <id>` | Mover el holograma a tu ubicación actual |
| `/holo list` | Listar todos los IDs de hologramas |
| `/holo info <id>` | Mostrar mundo, coordenadas, visibilidad y líneas |
| `/holo show <id> <jugador>` | Forzar a un jugador a ver un holograma en modo `PLAYERS` |
| `/holo hide <id> <jugador>` | Eliminar a un jugador de la lista de permitidos `PLAYERS` |
| `/holo reload` | Recargar todos los hologramas desde `holograms.yml` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.holograms.admin` | Todos los comandos de gestión de hologramas | OP |

---

## Configuración (`holograms.yml`)

```yaml
lobby-board:
  world: world
  x: 0.5
  y: 65.0
  z: 0.5
  visibility: GLOBAL        # GLOBAL | PERMISSION | PLAYERS
  permission: ""
  allowed-players: []
  lines:
    - type: TEXT
      content: "&b&lTop Jugadores"
    - type: HEAD
      player: "Notch"
    - type: ITEM
      material: DIAMOND
```
