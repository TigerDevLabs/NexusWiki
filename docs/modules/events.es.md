# Módulo Events

El módulo Events añade **eventos dinámicos a escala mundial** que afectan a todos los jugadores simultáneamente — comenzando con la **Luna de Sangre**, que transforma las noches en desafíos de supervivencia cada vez más peligrosos, vinculados a una racha por jugador y a un **Arco del Sacrificio**.

---

## Luna de Sangre

La Luna de Sangre se activa automáticamente cada noche cuando el tiempo del mundo supera el **tick 13000** y se desactiva al amanecer (**tick 23000**). Los operadores del servidor también pueden controlarla manualmente.

### Efectos Mientras Está Activa

| Efecto | Detalle |
| --- | --- |
| Bonificador de nivel de mob | Todas las tiradas de Mobs con Nivel reciben **+2** |
| Pago del empleo Cazador | Multiplicado por el `kill-pay-multiplier` configurado (por defecto ×1,5) |
| Lluvia de partículas | Partículas DUST rojas aparecen alrededor de cada jugador en línea cada 3 segundos |
| Oleadas de horda | Una horda de mobs aparece cada `horde-interval-ticks` (por defecto 5 min) |

Al **amanecer** (desactivación), cada jugador en línea que sobrevivió gana **+1** en su racha de supervivencia.

### Oleadas de Horda

En cada intervalo de horda, se elige un jugador en línea aleatorio como objetivo. **30 mobs** aparecen en un anillo de 18 bloques a su alrededor: Zombie, Esqueleto, Creeper, Araña, Bruja, Husk, Ahogado. Todos los mobs de la horda se llaman `[Blood Moon]` en rojo oscuro.

### Comandos

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/bloodmoon` | Mostrar estado actual de la Luna de Sangre | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon start` | Activar la Luna de Sangre manualmente | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon stop` | Desactivar la Luna de Sangre manualmente | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon status` | Salida de estado detallada | `nexusslime.events.bloodmoon.admin` |

### Configuración (`events/config.yml`)

```yaml
blood-moon:
  enabled: true
  world: world                   # El mundo donde se monitorean los cambios de tiempo
  kill-pay-multiplier: 1.5       # Multiplicador de pago del Cazador durante la Luna de Sangre
  particle-interval-ticks: 60   # Con qué frecuencia (ticks) generar partículas por jugador
  horde-interval-ticks: 6000    # Con qué frecuencia (ticks) lanzar una oleada de horda (6000 = 5 min)
  horde-size: 30                 # Número de mobs por oleada de horda
```

---

## Racha de Supervivencia

Cada jugador tiene una **racha de supervivencia a la Luna de Sangre** almacenada de forma persistente en SQLite (`events/events.db`).

| Evento | Cambio en la Racha |
| --- | --- |
| Sobrevivir una noche completa de Luna de Sangre | **+1** (otorgado al amanecer) |
| Morir durante una Luna de Sangre | **Reiniciar a 0** |

Cuando la racha alcanza un **múltiplo de 7** (7, 14, 21, 28...), el jugador recibe una **Invitación de Sacrificio** la próxima vez que duerma.

---

## Arco del Sacrificio

El Arco del Sacrificio es un desafío opcional de alto riesgo activado por la racha de supervivencia. Se integra con el [módulo Dreams](dreams.md): cuando la racha califica, dormir abre una **GUI de elección** en lugar de una cutscene de sueño.

### GUI de Elección

Una GUI de 3 filas con dos opciones:

| Ranura | Ítem | Acción |
| --- | --- | --- |
| 11 | Lana Verde — **Aceptar** | Teletransporte a la arena, juicio de supervivencia de 90 segundos |
| 15 | Lana Roja — **Rechazar** | Reiniciar racha, sin otra penalización |

Cerrar la GUI sin hacer clic cuenta como **Rechazo**.

### Juicio en la Arena

1. El jugador es teletransportado a la arena configurada (o permanece en su ubicación actual si no está configurada)
2. **5 mobs de arena** aparecen: Zombie, Esqueleto, Esqueleto Wither, Blaze, Araña de Cueva
3. Una **cuenta regresiva de 90 segundos** comienza con avisos a los 30s, 10s y 5s

### Resultados

| Resultado | Consecuencia |
| --- | --- |
| **Sobrevivir** | Recompensa otorgada (por defecto: 3 Bloques de Diamante), transmisión al servidor, racha reiniciada |
| **Morir** | Racha reiniciada a 0 |
| **Salir/desconectarse** | Sesión limpiada, tratada como fracaso |

### Configuración (`events/config.yml`)

```yaml
sacrifice:
  arena:
    world: ""    # Dejar en blanco para usar el mundo actual del jugador
    x: 0.0
    y: 64.0
    z: 0.0
```

!!! tip "Configurar la Arena"
    Construye una arena PvE dedicada y establece sus coordenadas en `sacrifice.arena`. Deja `world` en blanco para luchar en el sitio — útil para pruebas.

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.events.bloodmoon.admin` | Controlar la Luna de Sangre manualmente | OP |
