# Módulo Clanes

El módulo Clanes permite que los jugadores creen equipos persistentes con **conquista de territorio**, **árbol de mejoras**, un **cofre compartido** y **chat de clan**.

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/clan create <nombre> <tag>` | Crear un nuevo clan | `nexusprism.clan.use` |
| `/clan disband` | Disolver el clan | `nexusprism.clan.use` |
| `/clan invite <jugador>` | Invitar a un jugador | `nexusprism.clan.use` |
| `/clan join <nombre>` | Unirse a un clan | `nexusprism.clan.use` |
| `/clan leave` | Abandonar el clan | `nexusprism.clan.use` |
| `/clan kick <jugador>` | Expulsar a un miembro | `nexusprism.clan.use` |
| `/clan promote <jugador>` | Promover a oficial | `nexusprism.clan.use` |
| `/clan demote <jugador>` | Degradar a miembro | `nexusprism.clan.use` |
| `/clan info [nombre]` | Ver información del clan | `nexusprism.clan.use` |
| `/clan list` | Listar todos los clanes | `nexusprism.clan.use` |
| `/clan chat` | Alternar chat de clan | `nexusprism.clan.use` |
| `/clan claim` | Reclamar chunk actual | `nexusprism.clan.use` |
| `/clan unclaim` | Liberar chunk actual | `nexusprism.clan.use` |
| `/clan map` | Mostrar mapa de territorio | `nexusprism.clan.use` |
| `/clan chest` | Abrir cofre del clan | `nexusprism.clan.use` |
| `/clan upgrade` | Abrir menú de mejoras | `nexusprism.clan.use` |
| `/clan top` | Clasificación de clanes | `nexusprism.clan.use` |
| `/clan admin disband <nombre>` | Forzar disolución (admin) | `nexusprism.clan.admin` |

---

## Roles

| Rol | Permisos |
| --- | --- |
| **Líder** | Todas las acciones, disolver, mejorar |
| **Oficial** | Invitar, expulsar miembros, gestionar territorio |
| **Miembro** | Acceder al cofre, chat, usar territorio |

---

## Sistema de Territorio

Los clanes reclaman chunks como territorio. Los miembros pueden construir libremente; los no-miembros son bloqueados (cuando la protección está activada).

### Configuración (`clans/config.yml`)

```yaml
pvp-friendly-fire: false       # Los miembros no pueden atacarse entre sí

clan-name-min-length: 3
clan-name-max-length: 16
clan-tag-min-length: 2
clan-tag-max-length: 4

base-member-cap: 10            # Miembros en nivel 1
base-territory-cap: 10         # Chunks reclamables en nivel 1

neutral-chunk-protection: false

territory-worlds:
  - world
  - world_nether
```

---

## Árbol de Mejoras (`clans/upgrades.yml`)

```yaml
upgrades:
  member_cap:
    display-name: "&aExpansión de Miembros"
    description: "Aumenta el máximo de miembros en 5."
    max-level: 5
    cost-per-level:
      money: 5000
    bonus-per-level:
      members: 5

  territory_cap:
    display-name: "&aExpansión de Territorio"
    description: "Reclama 10 chunks adicionales por nivel."
    max-level: 10
    cost-per-level:
      money: 3000
    bonus-per-level:
      chunks: 10
```

---

## Permisos

| Permiso | Descripción | Predeterminado |
| --- | --- | --- |
| `nexusprism.clan.use` | Usar comandos de clan | true |
| `nexusprism.clan.admin` | Gestión admin de clanes | OP |
| `nexusprism.clan.bypass-protection` | Ignorar protección de territorio | OP |

---

## PlaceholderAPI

| Placeholder | Descripción |
| --- | --- |
| `%nexusprism_clan_name%` | Nombre del clan del jugador |
| `%nexusprism_clan_tag%` | Tag del clan |
| `%nexusprism_clan_role%` | Rol del jugador en el clan |
| `%nexusprism_clan_level%` | Nivel del clan |
| `%nexusprism_clan_members%` | Conteo de miembros en línea |
| `%nexusprism_clan_bank%` | Saldo del banco del clan |
