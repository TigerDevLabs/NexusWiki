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

### Escalado de Dificultad por Racha

Rachas más altas hacen cada Luna de Sangre más difícil — más niveles de mob, más spawns y eventos de mini-jefe adicionales.

| Rango de Racha | Bonificador de Nivel | Bonificador de Tasa de Spawn | Multiplicador Elite | Eventos Extra |
| --- | --- | --- | --- | --- |
| 1–6 | Base | Base | Base | — |
| 7–13 | +4 | +500% | ×3 | — |
| 14–20 | +7 | +700% | ×5 | Spawn de jefe a mitad del evento |
| 21+ | +10 | +900% | Ilimitado | Mini-jefes cada 5 min |

---

## Arco del Sacrificio

El Arco del Sacrificio es un desafío opcional de alto riesgo activado por la racha de supervivencia. Se integra con el [módulo Dreams](dreams.md): cuando la racha califica, dormir abre una **GUI de elección** en lugar de una cutscene de sueño.

### GUI de Elección

Una GUI de 3 filas con dos opciones:

| Ranura | Ítem | Acción |
| --- | --- | --- |
| 11 | Lana Verde — **Aceptar** | Teletransporte a la arena, combate contra el Jefe Isekai |
| 15 | Lana Roja — **Rechazar** | Reiniciar racha, sin otra penalización |

Cerrar la GUI sin hacer clic cuenta como **Rechazo**.

### Juicio en la Arena

1. El jugador es teletransportado a la arena configurada (o permanece en su ubicación actual si no está configurada)
2. Un **Jefe Isekai** aleatorio es invocado — seleccionado del grupo elegible para la racha del jugador
3. Una **cuenta regresiva de 180 segundos** comienza con avisos a los 60s, 30s, 10s y 5s

### Resultados

| Resultado | Consecuencia |
| --- | --- |
| **Sobrevivir** | Recompensa otorgada por tier, transmisión al servidor, racha reiniciada |
| **Morir** | Racha reiniciada a 0 |
| **Salir/desconectarse** | Sesión limpiada, tratada como fracaso |

### Tiers de Recompensa del Sacrificio

Las recompensas escalan según cuántos Sacrificios has completado (cada 7 hitos de racha).

| Hito de Racha | Recompensas |
| --- | --- |
| **7** | Ítem MMO Tier 1 + **+5 HP Máx** permanente |
| **14** | Ítem MMO Tier 2 + **+10 HP Máx** permanente + **1 punto de atributo** |
| **21** | Ítem MMO Tier 3 + **+2 puntos de atributo** permanentes + efecto cosmético |
| **28** | Ítem MMO Tier 4 + **+3 puntos de atributo** + título + huevo de jefe |
| **35+** | Puntos de atributo multiplicadores + cosmético anime exclusivo por hito |

!!! warning "Racha Reiniciada Tras el Sacrificio"
    Completar un Sacrificio — ganar o perder — reinicia tu racha a 0. Tu **mejor racha** se registra por separado y nunca se reinicia.

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

## Códex de Jefes Isekai

Cuando se acepta un Sacrificio, se invoca un **Jefe Isekai** aleatorio en la arena. El grupo disponible depende de la racha actual del jugador. Cada jefe tiene múltiples fases, mecánicas únicas y un botín único.

Las definiciones de jefe están en `events/isekai_bosses/*.yml`. HP y daño escalan con la racha:

```
statFinal = statBase × (1 + (racha - 7) × 0,2)
```

### Grupo de Jefes

| Jefe | Racha Mín. | Entidad Base | Peso de Spawn |
| --- | --- | --- | --- |
| Rimuru Tempest | 7 | Slime Gigante | 10 |
| Kazuma Satou | 7 | Bruja | 9 |
| Subaru Natsuki | 7 | Zombie | 8 |
| Ainz Ooal Gown | 14 | Esqueleto Wither | 7 |
| Itadori Yuji | 14 | Piglin Bruto | 6 |
| Kirito | 14 | Zombie | 6 |
| Gojo Satoru | 21 | Phantom | 5 |
| Levi Ackermann | 21 | Vindicator | 4 |

---

=== "Rimuru Tempest"

    **Racha Mín.:** 7 · **Entidad Base:** Slime Gigante

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 60% | Aura Depredadora (absorbe proyectiles), División de Slime (mini-slimes al 80%/70%) |
    | 2 | 60% → 25% | Tormenta de Acero (12 flechas 360°), Drenaje Depredador (cura al golpear) — cambia a Guardian |
    | 3 | 25% → 0% | Colapso del Vacío (puxão en AoE de 8 bloques, 3 dmg/tick), Regeneración Infinita (2 HP/2 ticks) — inmune a retroceso |

    **Botín:** Fragmento de núcleo de slime · Aura brillo azul cosmética

=== "Kazuma Satou"

    **Racha Mín.:** 7 · **Entidad Base:** Bruja

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 60% | Robo (quita ítem aleatorio del hotbar cada 12s), Gatillo Suertudo (15% crit × 5 daño) |
    | 2 | 60% → 25% | Toque Drenante (drena niveles de XP), Comando de Grupo (2 "Aqua" + 1 "Darkness"), Explosión de Megumin (única en transición) |
    | 3 | 25% → 0% | Gatillo Suertudo sube al 35% con reflejo de daño; Robo Final; Llamada de Aqua (restauración de HP única) |

    **Botín:** Tarjeta de aventurero · Ítems robados devueltos al doble

=== "Subaru Natsuki"

    **Racha Mín.:** 7 · **Entidad Base:** Zombie

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 50% | Golpe de Tierra, Llamada Desesperada (invoca "Rem" al 60%) |
    | **Retorno por la Muerte** | Al llegar a 0 HP (una vez) | Se restablece al 100% HP, HP del jugador restaurado, título: `⟳ RETURN BY DEATH` |
    | Post-RBD | 100% → 0% | Factor Bruja (Wither I + Hambre II cada 20s), Último Recurso (por debajo del 25%: +velocidad, +daño) |

    !!! danger "Retorno por la Muerte"
        Subaru no puede ser matado la primera vez. La mecánica se activa exactamente **una vez por combate**.

    **Botín:** Moneda de plata cosmética · Aura "Olor de la Bruja"

=== "Ainz Ooal Gown"

    **Racha Mín.:** 14 · **Entidad Base:** Esqueleto Wither

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 70% | Convocar Guardianes del Piso (3 zombies cada 30s), Estallido Negativo (cráneo wither → Wither II + Debilidad) |
    | 2 | 70% → 30% | Garra de la Muerte (10 daño verdadero retrasado 4s), Sabiduría Oscura (15s de inmunidad al tipo de daño repetido) |
    | 3 | 30% → 0% | Toque de Ainz (quieto 3s = muerte instantánea), Devorador de Almas (cura 5 HP por entidad muerta) |

    !!! warning "No puede ser matado por debajo de 1 HP mientras las entidades convocadas estén vivas."

    **Botín:** Corona No-Muerta cosmética · Fragmento de título `§8Overlord`

=== "Itadori Yuji"

    **Racha Mín.:** 14 · **Entidad Base:** Piglin Bruto

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 50% | Puño Divergente (8% proc Flash Negro = 10× daño), Embestida (combo de 3 golpes telegráfico) |
    | 2 — **Sukuna Despierta** | 50% → 0% | Desmantelar (3 proyectiles en V + sangrado), Tajo (AoE cuerpo a cuerpo de 5 bloques), Santuario Malévolo (por debajo del 20%: 20 tajos en 3s), Flash Negro sube al 15% |

    **Botín:** Cristal de energía maldita · Título `§4Maldito` · Cosmético de tatuaje

=== "Kirito"

    **Racha Mín.:** 14 · **Entidad Base:** Zombie

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 40% | Skill Vorpal (carga de 5 golpes en línea recta), Parada (20% de negar golpe recibido) |
    | 2 — **Doble Espada** | 40% → 0% | VELOCIDAD III permanente, Starburst Stream (16 golpes consecutivos en 4s — rompe con 8+ daño en un golpe), Golpe Final (por debajo del 15%: carga crit garantizada) |

    **Botín:** Cosmético de élitra abrigo negro · Título `§7Solo Player` · Set de espadas dobles CMD

=== "Gojo Satoru"

    **Racha Mín.:** 21 · **Entidad Base:** Phantom

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 60% | Infinito (70% de los ataques causan 1 daño), Cambio de Fase (invisible cada 8s por 4s) |
    | 2 | 60% → 25% | Tirón Azul (atrae al jugador), Vacío Púrpura (AoE en línea recta — 1s de aviso, 15 daño + Levitación) |
    | 3 — **Expansión de Dominio** | 25% → 0% | Oscuridad cada 2s, Desorientación en ráfagas, Golpe de Dominio (+50%), Infinito TOTALMENTE activo |

    !!! tip "Las habilidades de mago y el daño de fuego evitan el Infinito."

    **Botín:** Cosmético de venda · Título `§b∞ Limitless`

=== "Levi Ackermann"

    **Racha Mín.:** 21 · **Entidad Base:** Vindicator

    | Fase | Rango de HP | Habilidades Clave |
    | --- | --- | --- |
    | 1 | 100% → 50% | Carga ODM (teletransporte a pared → arremete hacia el jugador), Corte Limpio (ignora 50% de la defensa), Maniobra Vertical (VELOCIDAD IV en círculos por 3s) |
    | 2 | 50% → 0% | Pared a Pared (4 cargas encadenadas con telegrafía decreciente), Forma Matador de Titanes (por debajo del 25%: postura de 5s — un golpe a 0,5 corazones, contorno blanco telegráfico) |

    !!! danger "No puede ser aturdido, golpeado hacia atrás ni ralentizado — jamás."

    **Botín:** Cosmético de élitra ODM · Título `§8Survey Corps` · Espada mata-titanes CMD

---

### Grupo de Jefes Futuros (Racha 28+)

Jefes planificados para lanzamientos futuros: Goku, Naruto Uzumaki, Aizen Sosuke, Natsu Dragneel, Sung Jin-Woo, Giorno Giovanna.

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.events.bloodmoon.admin` | Controlar la Luna de Sangre manualmente | OP |
