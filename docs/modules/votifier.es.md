# Módulo Votifier

El módulo Votifier es un **servidor Votifier V1 y V2 independiente** integrado directamente en NexusPrism. Gestiona los votos recibidos de sitios de listado de servidores, distribuye recompensas configurables y rastrea las rachas de votos de los jugadores en una tabla de clasificación.

---

## Cómo Funciona

```flow
Sitio de Votación  ──► Servidor Votifier (puerto 8192)  ──► VoteManager  ──► Recompensas + Racha
                        (V1 RSA / V2 basado en token)
```

1. Registra tu servidor en sitios de votación (Minecraftservers.org, etc.)
2. Apunta cada sitio a la IP de tu servidor y al puerto de Votifier (por defecto `8192`)
3. Cuando un jugador vota, el sitio envía un payload a tu servidor Votifier
4. NexusPrism procesa el voto, ejecuta los comandos de recompensa y actualiza la racha

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/vote` | Mostrar enlaces de votación y tu racha actual | `nexusprism.vote` |
| `/votetop` | Mostrar la tabla de clasificación de votos | `nexusprism.vote.top` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.vote` | Usar `/vote` | true |
| `nexusprism.vote.top` | Usar `/votetop` | true |

---

## Configuración (`votifier/config.yml`)

```yaml
host: "0.0.0.0"       # Escuchar en todas las interfaces
port: 8192             # Puerto de Votifier (ábrelo en tu firewall)
token: "change-this-token"   # Secreto compartido para autenticación V2

vote-links:
  - "https://minecraftservers.org/vote/YOUR_SERVER_ID"
  - "https://minecraft-server-list.com/server/YOUR_SERVER_ID/vote/"

rewards:
  - type: COMMAND
    value: "eco give {player} 500"
  - type: COMMAND
    value: "crates key give {player} VOTE 1"
  - type: MESSAGE
    value: "&aThank you for voting, {player}! You received $500 and a crate key."

streak:
  enabled: true
  max-gap-hours: 36    # Votos con más de 36h de diferencia reinician la racha
  multipliers:
    5:  1.5            # Racha de 5 votos = 1.5× recompensas
    10: 2.0            # Racha de 10 votos = 2× recompensas
    30: 3.0            # Racha de 30 votos = 3× recompensas
```

### Campos de Configuración

| Campo | Descripción |
| --- | --- |
| `host` | IP para enlazar el servidor de votos. Usa `0.0.0.0` para todas las interfaces. |
| `port` | Puerto TCP. Debe estar abierto en el firewall y redireccionado si estás detrás de NAT. |
| `token` | Token secreto para autenticación V2. Cámbialo de inmediato. |
| `vote-links` | Lista de URLs mostradas por `/vote`. |
| `rewards[].type` | `COMMAND` (ejecuta un comando en consola) o `MESSAGE` (envía mensaje al jugador). |
| `rewards[].value` | Cadena de comando/mensaje. Usa `{player}` para el nombre del votante. |
| `streak.max-gap-hours` | Cuántas horas pueden pasar entre votos antes de que se reinicie la racha. |
| `streak.multipliers` | Mapa de longitud de racha → multiplicador de recompensas. |

---

## Soporte de Protocolos

| Protocolo | Descripción |
| --- | --- |
| **V1** | Protocolo Votifier legado con cifrado RSA. Compatible con la mayoría de sitios más antiguos. |
| **V2** | Protocolo moderno basado en token HMAC-SHA256. Preferido — más seguro y fiable. |

Las claves RSA para V1 se generan automáticamente en el primer inicio y se almacenan como `votifier/rsa/public.key` y `votifier/rsa/private.key`.

---

## Registro en Sitios de Votación

Al registrarte en un sitio de votación, necesitarás:

- **IP del Servidor** — la dirección IP pública de tu servidor
- **Puerto de Votifier** — `8192` (o el que hayas configurado en `config.yml`)
- **Clave Pública** — cópiala de `plugins/NexusPrism/votifier/rsa/public.key` (sitios V1)
- **Token** — el valor de `token` en `config.yml` (sitios V2)

---

## Sistema de Racha

| Racha | Multiplicador |
| --- | --- |
| 1–4 votos | 1× (base) |
| 5–9 votos | 1.5× |
| 10–29 votos | 2× |
| 30+ votos | 3× |

Cuando el multiplicador está activo, los valores `COMMAND` de recompensa se ejecutan múltiples veces según el multiplicador (redondeado al entero más cercano). También puedes implementar lógica de multiplicador personalizada usando el placeholder `%nexusprism_vote_streak%` en plugins externos.

---

## PlaceholderAPI

| Placeholder | Descripción |
| --- | --- |
| `%nexusprism_votes_total%` | Total de votos acumulados del jugador |
| `%nexusprism_vote_streak%` | Racha de votos actual del jugador |
