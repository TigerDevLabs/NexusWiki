# Módulo Economía


---

## Resumen

| Moneda | Descripción |
| --- | --- |
| **Dinero** (`$`) | Moneda estándar del juego, ganada vendiendo ítems, votando, etc. |
| **Créditos** | Moneda premium, normalmente obtenida en la webstore |

---

## Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/money` | Verificar tu saldo | `nexusprism.economy.money` |
| `/money <jugador>` | Verificar saldo de otro jugador | `nexusprism.economy.money` |
| `/baltop` | Top 10 jugadores más ricos | `nexusprism.economy.baltop` |
| `/sell hand` | Vender ítem en mano | `nexusprism.economy.sell` |
| `/sell all` | Vender todos los ítems vendibles | `nexusprism.economy.sell` |
| `/sell inventory` | Vender inventario completo | `nexusprism.economy.sell` |
| `/worth [ítem]` | Verificar valor de venta del ítem | `nexusprism.essentials.worth` |
| `/eco give <jugador> <cantidad>` | Dar dinero (admin) | `nexusprism.economy.admin` |
| `/eco take <jugador> <cantidad>` | Quitar dinero (admin) | `nexusprism.economy.admin` |
| `/eco set <jugador> <cantidad>` | Establecer saldo (admin) | `nexusprism.economy.admin` |
| `/eco reset <jugador>` | Resetear saldo (admin) | `nexusprism.economy.admin` |

---

## Permisos

| Permiso | Descripción | Predeterminado |
| --- | --- | --- |
| `nexusprism.economy.money` | Ver saldos | true |
| `nexusprism.economy.baltop` | Ver clasificación | true |
| `nexusprism.economy.sell` | Usar /sell | true |
| `nexusprism.economy.admin` | Comandos de admin eco | OP |

---

## Precios de Venta (`economy/sell-prices.yml`)

```yaml
prices:
  # ── Piedra y Tierra ───────────────────────────────────────────
  COBBLESTONE:       2.0
  STONE:             3.0
  DIRT:              1.0

  # ── Madera y Plantas ──────────────────────────────────────────
  OAK_LOG:           6.0
  WHEAT:             4.0

  # ── Menas y Metales ───────────────────────────────────────────
  COAL:             10.0
  IRON_INGOT:       25.0
  GOLD_INGOT:       50.0
  DIAMOND:         200.0
  NETHERITE_INGOT: 1200.0

  # ── Drops de Mob ──────────────────────────────────────────────
  BLAZE_ROD:        20.0
  ENDER_PEARL:      25.0
  SHULKER_SHELL:   150.0
```

!!! tip
    Usa nombres de Material (mayúsculas Bukkit). Los ítems no listados en `sell-prices.yml` no pueden venderse.

---

## PlaceholderAPI

| Placeholder | Descripción |
| --- | --- |
| `%nexusprism_money%` | Saldo de dinero del jugador |

---

## Empleos

Los jugadores eligen un empleo y ganan dinero y XP realizando actividades relacionadas en el juego.

### Empleos Disponibles

| Empleo | Actividades Principales |
| --- | --- |
| **Minero** | Romper menas y piedra |
| **Cazador** | Matar mobs hostiles |
| **Granjero** | Cosechar cultivos |
| **Pescador** | Pescar |
| **Herrero** | Fundir lingotes, fabricar herramientas/armaduras |
| **Encantador** | Encantar ítems |
| **Alquimista** | Preparar pociones |
| **Leñador** | Talar troncos |

Los jugadores solo pueden tener **un empleo a la vez**. Las configuraciones de empleos son archivos YAML en `economy/jobs/`.

### Fórmulas de Pago y XP

| Valor | Fórmula |
| --- | --- |
| **Pago por acción** | `base × (1 + nivel × escalaPagoPorNivel)` |
| **XP para el siguiente nivel** | `xpBaseParaNivel × 2^((nivel-1)/10)` *(se duplica cada 10 niveles)* |

### Comandos

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/job` | Abrir GUI de empleos | `nexusprism.economy.job.use` |
| `/job join <id>` | Unirse a un empleo | `nexusprism.economy.job.use` |
| `/job leave` | Abandonar el empleo actual | `nexusprism.economy.job.use` |
| `/job info [id]` | Ver estadísticas del empleo | `nexusprism.economy.job.use` |
| `/job top` | Clasificación de empleos | `nexusprism.economy.job.use` |

!!! note "Bonificación de Luna de Sangre"
    Durante una Luna de Sangre, el pago por matar del empleo **Cazador** se multiplica (por defecto ×1,5). Ver el [módulo Events](events.md).

---

## Tiendas de Cofre

Los jugadores pueden crear tiendas en el mundo colocando un letrero en (o adyacente a) un cofre.

### Creando una Tienda

1. Coloca un cofre
2. Coloca un letrero en la cara frontal, superior o en un bloque adyacente
3. Escribe `[Shop]` en la **primera línea**
4. Escribe `BUY <precio>` en la línea 2 (opcional)
5. Escribe `SELL <precio>` en la línea 3 (opcional)

El plugin detecta automáticamente el cofre debajo o adyacente al letrero. El stock se muestra automáticamente en la línea 4.

### Formato del Letrero

```
[Shop]
BUY 50
SELL 25
[12 en stock]
```

### GUI de la Tienda

Se abre una GUI de 3 filas al hacer clic derecho en el letrero:

| Ranura | Contenido |
| --- | --- |
| Centro (ranura 13) | Vista previa del ítem |
| Ranuras 19–21 | Comprar ×1 / ×8 / ×64 |
| Ranuras 23–25 | Vender ×1 / ×8 / ×64 |

### Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusprism.economy.shop.create` | Crear tiendas de cofre | true |
| `nexusprism.economy.shop.admin` | Crear tiendas admin (stock ilimitado) | OP |

---

## Teletransportes de Jugador

Los jugadores pueden establecer puntos de teletransporte con nombre que cualquier otro jugador puede visitar.

### Comandos

| Comando | Descripción |
| --- | --- |
| `/pw set <nombre>` | Crear un punto en tu ubicación actual |
| `/pw delete <nombre>` | Eliminar uno de tus puntos |
| `/pw desc <nombre> <texto>` | Establecer una descripción para el punto |
| `/pw icon <nombre> <material>` | Establecer el ícono mostrado en la GUI |
| `/pw list` | Explorar todos los puntos de jugadores (GUI paginada de 6 filas) |
| `/pw visit <jugador> <nombre>` | Teletransportarse al punto de otro jugador |

### Límites de Puntos

| Permiso | Máximo de Puntos |
| --- | --- |
| `nexusprism.economy.playerwarp.unlimited` | Ilimitado |
| `nexusprism.economy.playerwarp.10` | 10 |
| `nexusprism.economy.playerwarp.3` | 3 |
| *(por defecto)* | 1 |

---

## Casa de Subastas

Un tablón de listados global donde los jugadores compran y venden ítems entre sí.

### Cómo Funciona

- Lista cualquier ítem de tu mano con `/ah sell <precio>`
- Los listados expiran tras **7 días** si no se venden
- Los ítems expirados o cancelados se devuelven al dueño (limpieza horaria)
- Cada jugador puede tener hasta **10 listados activos** a la vez

### Comandos

| Comando | Descripción | Permiso |
| --- | --- | --- |
| `/ah` | Explorar listados activos (GUI paginada de 6 filas) | `nexusprism.economy.ah.use` |
| `/ah sell <precio>` | Listar ítem en mano a un precio | `nexusprism.economy.ah.use` |
| `/ah own` | Ver tus listados; cancelar activos o reclamar expirados | `nexusprism.economy.ah.use` |
| `/ah cancel <id>` | Cancelar un listado por su ID | `nexusprism.economy.ah.use` |
