# Módulo Traits

El módulo Traits asigna a cada jugador un conjunto de **3 Cartas del Tarot** que otorgan efectos pasivos y reactivos. Las cartas se sortean aleatoriamente en el primer acceso y pueden rerollearse con un costo en dinero.

---

## Cartas del Tarot

| Rareza | Peso | Ejemplos |
| --- | --- | --- |
| **Común** | 10 | El Loco, El Mago, La Sacerdotisa, La Emperatriz, El Carro, La Fuerza, El Ermitaño, La Rueda de la Fortuna, La Justicia, El Mundo |
| **Poco común** | 6 | El Emperador, El Hierofante, Los Amantes, La Luna, El Sol, La Templanza, La Estrella |
| **Raro** | 3 | La Torre, El Diablo, El Rey Ermitaño |
| **Legendario** | 1 | El Juicio, La Muerte |

---

## Comandos

| Comando | Permiso | Descripción |
| --- | --- | --- |
| `/traits` | *(todos los jugadores)* | Abrir el GUI de Traits del Tarot |
| `/traits info` | *(todos los jugadores)* | Listar las cartas actuales en el chat |
| `/traits admin set <jugador> <slot 1-3> <NOMBRE_CARTA>` | `nexusslime.traits.admin` | Forzar una carta (omite costo y cooldown) |
| `/traits admin reload` | `nexusslime.traits.admin` | Recargar `traits/config.yml` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.traits.admin` | Comandos administrativos de traits | OP |

---

## Configuración (`traits/config.yml`)

```yaml
reroll:
  full-cost: 5000.0
  single-cost: 2000.0
  full-cooldown-seconds: 604800     # 7 días
  single-cooldown-seconds: 86400    # 24 horas
```
