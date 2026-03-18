# Módulo RNG

El módulo RNG proporciona **giros de recompensas diarios**, **bloques de suerte**, **pulls de gacha** mediante Pergaminos de Investigación y **eventos automáticos de servidor**.

---

## Comandos

| Comando | Permiso | Descripción |
| --- | --- | --- |
| `/spin` | `nexusslime.rng.spin` | Abrir el GUI de giro diario |
| `/rng event start <id>` | `nexusslime.rng.admin` | Forzar inicio de un evento |
| `/rng event stop` | `nexusslime.rng.admin` | Detener el evento activo |
| `/rng event list` | `nexusslime.rng.admin` | Listar todos los eventos definidos |
| `/rng giveblock <jugador> [pool] [cantidad]` | `nexusslime.rng.admin` | Dar bloques de suerte |
| `/rng giveparchment <jugador> <BASIC\|ADVANCED\|INFINITY>` | `nexusslime.rng.admin` | Dar un Pergamino de Investigación |
| `/rng research get <jugador>` | `nexusslime.rng.admin` | Ver nivel de investigación |
| `/rng research set <jugador> <nivel>` | `nexusslime.rng.admin` | Establecer nivel de investigación |
| `/rng reload` | `nexusslime.rng.admin` | Recargar config, eventos y pools |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.rng.spin` | Usar el giro diario | true |
| `nexusslime.rng.admin` | Todos los comandos admin de RNG | OP |

---

## Tipos de Eventos de Servidor

| Tipo | Efecto |
| --- | --- |
| `DOUBLE_DROPS` | Todos los drops se duplican |
| `DOUBLE_XP` | Todo el XP obtenido se duplica |
| `MOB_RUSH` | Mayor tasa de aparición de mobs |
| `MINING_RUSH` | Drops adicionales al minar minerales |
| `TRADING_BOOST` | Mejores precios de comercio con aldeanos |
| `HAPPY_HOUR` | Bono combinado (drops + XP) |
| `CUSTOM` | Solo ejecuta un comando/anuncio personalizado |

---

## Gacha (Pergaminos de Investigación)

| Nivel | Pool | Nivel de Investigación Mínimo |
| --- | --- | --- |
| `BASIC` | `gacha_basic` | 0 |
| `ADVANCED` | `gacha_advanced` | 5 |
| `INFINITY` | `gacha_infinity` | 10 |
