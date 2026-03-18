# Módulo MMO

El módulo MMO transforma NexusSlime en una experiencia ligera de RPG. Los jugadores ganan un **nivel MMO**, asignan **puntos de estadística**, suben de nivel en **seis árboles de habilidades**, desbloquean y usan **habilidades**, y progresan por **ocho profesiones** — cada una con una pasiva de maestría única.

---

## Nivel MMO y Puntos de Estadística

Los jugadores ganan XP MMO de cualquier actividad en el juego (combate, profesiones, árboles de habilidades). Subir de nivel otorga **1 punto de estadística** sin gastar para usar libremente.

### Fórmula de XP para Nivel

```
xpParaNivel(n) = 100 × 2^((n-1) / 10)
```

El requisito de XP se duplica cada 10 niveles.

### Estadísticas

| Estadística | Efecto |
| --- | --- |
| `MAX_HEALTH` | Aumenta los corazones máximos |
| `STRENGTH` | +1,5% de daño cuerpo a cuerpo por punto |
| `DEFENSE` | -0,8% de daño recibido por punto (máx. 80% de reducción) |
| `AGILITY` | +0,5% de probabilidad de esquivar por punto (golpe cancelado, "¡Esquivado!" en actionbar) |
| `INTELLIGENCE` | Aumenta el poder de las habilidades mágicas |
| `WISDOM` | Afecta la eficacia de curación y costos equivalentes a maná |
| `LUCK` | Mejora las tasas de drop y resultados aleatorios |
| `CRIT_CHANCE` | +1% de probabilidad de golpe crítico por punto (máx. 95%) |
| `CRIT_DAMAGE` | Multiplicador de crítico = `1,5 + (critDaño × 0,01)` |
| `MAGIC_POWER` | Amplifica el daño de las habilidades mágicas |
| `MINING_SPEED` | Aumenta la velocidad de romper bloques |
| `FISHING_LUCK` | Mejora la calidad del tesoro de pesca |

**Valor final de estadística** = base (asignado por el jugador) + bonificadores del árbol de habilidades + bonificadores futuros de equipamiento.

### Comandos

| Comando | Descripción |
| --- | --- |
| `/stats` | Ver tu ficha de estadísticas y puntos sin gastar |
| `/stats add <estadística>` | Gastar 1 punto de estadística (ej.: `/stats add strength`) |

---

## Árboles de Habilidades

Seis árboles de habilidades independientes, cada uno aumentado de nivel por actividades específicas. Subir de nivel otorga bonificadores pasivos de estadísticas y desbloquea habilidades en hitos.

### Resumen de Árboles

| Árbol | Estadísticas Principales | Fuente de XP | Habilidades |
| --- | --- | --- | --- |
| **Guerrero** | Fuerza, Defensa, Vida Máxima | Asesinatos cuerpo a cuerpo | Golpe de Escudo (10), Furia Berserker (25), Aura del Señor de la Guerra (50) |
| **Pícaro** | Agilidad, Probabilidad Crítica, Daño Crítico | Asesinatos | Paso Sombra (10), Apuñalamiento (25), Forma Fantasma (50) |
| **Mago** | Inteligencia, Poder Mágico, Sabiduría | Encantar ítems | Bola de Fuego (10), Escudo Arcano (25), Explosión Nova (50) |
| **Arquero** | Agilidad, Probabilidad Crítica, Suerte | Asesinatos | Lluvia de Flechas (10), Ojo de Águila (25), Disparo Perforante (50) |
| **Sanador** | Sabiduría, Vida Máxima, Defensa | Curación | Aura Sagrada (10), Revivir (25), Santuario (50) |
| **Alquimista** | Suerte, Inteligencia, Sabiduría | Elaborar pociones | Nube Tóxica (10), Oleada de Elixir (25), Toque del Filósofo (50) |

### Descripciones de Habilidades

=== "Guerrero"

    | Nivel | Habilidad | Descripción |
    | --- | --- | --- |
    | 10 | **Golpe de Escudo** | Causa daño en cono y empuje frente al jugador |
    | 25 | **Furia Berserker** | Daño cuerpo a cuerpo ×2 durante 8 segundos |
    | 50 | **Aura del Señor de la Guerra** | Pasiva: +30% de daño cuerpo a cuerpo permanentemente |

=== "Pícaro"

    | Nivel | Habilidad | Descripción |
    | --- | --- | --- |
    | 10 | **Paso Sombra** | Teletransportarse 6 bloques en la dirección en que miras |
    | 25 | **Apuñalamiento** | Causa 4× de daño al golpear un objetivo por la espalda |
    | 50 | **Forma Fantasma** | 5 segundos de invisibilidad + +200% de daño |

=== "Mago"

    | Nivel | Habilidad | Descripción |
    | --- | --- | --- |
    | 10 | **Bola de Fuego** | Lanza un proyectil explosivo con rastro de partículas de llama |
    | 25 | **Escudo Arcano** | 3 orbes orbitando, cada uno absorbiendo 1 golpe recibido |
    | 50 | **Explosión Nova** | Explosión arcana en área centrada en el jugador |

=== "Arquero"

    | Nivel | Habilidad | Descripción |
    | --- | --- | --- |
    | 10 | **Lluvia de Flechas** | Disparar 9 flechas críticas en arco radial |
    | 25 | **Ojo de Águila** | Disparar una única flecha perforante que atraviesa mobs |
    | 50 | **Disparo Perforante** | Flecha con 5× de daño que ignora toda la defensa |

=== "Sanador"

    | Nivel | Habilidad | Descripción |
    | --- | --- | --- |
    | 10 | **Aura Sagrada** | Restaurar 6 corazones a todos los aliados cercanos |
    | 25 | **Revivir** | Previene el siguiente golpe fatal (escudo único) |
    | 50 | **Santuario** | Crear una zona de curación de 10 bloques durante 15 segundos |

=== "Alquimista"

    | Nivel | Habilidad | Descripción |
    | --- | --- | --- |
    | 10 | **Nube Tóxica** | Desplegar una nube de veneno persistente |
    | 25 | **Oleada de Elixir** | Compartir todas tus pociones activas con aliados cercanos |
    | 50 | **Toque del Filósofo** | Probabilidad pasiva de duplicar cualquier poción elaborada |

### Usar Habilidades

```
/skill use <idHabilidad>
```

O abre `/skill`, haz clic en un árbol y luego en el ícono de la habilidad. Los tiempos de recarga se rastrean por jugador por habilidad.

### Comandos

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/skill` | Abrir GUI del Navegador de Árboles de Habilidades | `nexusslime.mmo.use` |
| `/skill use <id>` | Activar una habilidad desbloqueada | `nexusslime.mmo.use` |

---

## Profesiones

Ocho profesiones suben de nivel independientemente de los árboles de habilidades. Cada una tiene una **pasiva de maestría** que se fortalece con el nivel de la profesión.

### Fórmula de XP

```
xpParaNivel(n) = xpBase × 1,8^(nivel / 10)
```

### Tabla de Profesiones

| Profesión | Fuente de XP | Pasiva de Maestría | Bono Máx. |
| --- | --- | --- | --- |
| **Minería** | Romper menas | Minero de Veta — duplicar probabilidad de drop de mena | 50% |
| **Agricultura** | Romper cultivos | Cosecha Abundante — duplicar drop de cosecha | 60% |
| **Pesca** | Pescar | Lanzamiento Afortunado — probabilidad extra de tesoro | 40% |
| **Leñador** | Romper troncos | Partidor de Madera — duplicar drop de tronco | 50% |
| **Herrería** | Fabricar/fundir herramientas y armaduras | Artesano Maestro — duplicar herramienta/armadura fabricada | 30% |
| **Alquimia** | Elaborar pociones | Duplicación de Pociones — duplicar pociones elaboradas | 50% |
| **Encantamiento** | Encantar ítems | Eficiencia Arcana — ahorrar niveles de XP al encantar | 40% |
| **Cocina** | Fabricar/cocinar alimentos | Gourmet — duplicar alimentos cocinados | 70% |

---

## Almacenamiento y Permisos

| Detalle | Valor |
| --- | --- |
| Base de datos | SQLite — `mmo/mmo.db` |
| Tablas | `player_mmo`, `player_skills`, `player_professions` |
| Permiso | `nexusslime.mmo.use` (por defecto: **true**) |
