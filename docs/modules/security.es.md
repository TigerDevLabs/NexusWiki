# Módulo Seguridad

El módulo Seguridad proporciona **autenticación BCrypt**, protección anti-bot con CAPTCHA, gestión de sesiones, anti-duplicación y herramientas anti-lag — diseñado para **servidores offline/crackeados**.

---

## Sub-sistemas

| Sub-sistema | Descripción |
| --- | --- |
| **Auth** | Registro/inicio de sesión con contraseñas BCrypt, sesiones persistentes |
| **Anti-Bot** | Limitación de tasa por IP, CAPTCHA en mapa, lista negra de nombres, detección de VPN |
| **Anti-Dupe** | Detecta y previene exploits comunes de duplicación de ítems |
| **Anti-Lag** | Limpiador de mundo programado, apilador de entidades |

---

## Autenticación

Los jugadores en servidores crackeados deben `/register` en el primer acceso y `/login` en los accesos siguientes. Las cuentas premium son verificadas mediante la API de Mojang y omiten la autenticación.

### Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/register <contraseña> <confirmar>` | Registrar una cuenta | *(todos)* |
| `/login <contraseña>` | Iniciar sesión | *(todos)* |
| `/changepassword <antigua> <nueva>` | Cambiar contraseña | *(autenticado)* |

### Configuración Auth (`security/auth.yml`)

```yaml
storage: sqlite

session-timeout-minutes: 30      # Re-login tras 30min inactivo
persistent-session-hours: 2      # Auto-login en 2h tras última sesión

max-failed-attempts: 5           # Bloqueo tras 5 contraseñas incorrectas
lockout-minutes: 10

login-spawn:
  enabled: false
```

---

## Anti-Bot

### Configuración (`security/antibot.yml`)

```yaml
rate-limit:
  window-seconds: 10
  max-joins: 3

name-blacklist-patterns:
  - "[A-Za-z]{1,3}[0-9]{5,}"
  - "bot[0-9]+"

captcha:
  enabled: true
  timeout-seconds: 60
  session-hours: 24

premium-check:
  enabled: true

alt-detection:
  max-accounts-per-ip: 3
```

---

## Anti-Lag

### Comandos

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/cleanworld` | Ejecutar limpieza manual del mundo | `nexusprism.security.cleanworld` |

### Configuración (`security/antilag.yml`)

```yaml
cleaner:
  interval-seconds: 300
  warn-seconds: 5
  item-age-ticks: 6000
  worlds:
    - world
    - world_nether

stacker:
  radius: 5.0
  max-stack: 50
```

---

## Comandos de Staff

| Comando | Uso | Permiso |
| --- | --- | --- |
| `/vanish` | Alternar invisibilidad (OP) | `nexusprism.staff.vanish` |
| `/invsee <jugador>` | Inspeccionar inventario (OP) | `nexusprism.staff.invsee` |
| `/spy` | Alternar espionaje de chat (OP) | `nexusprism.staff.spy` |

---

## Permisos

| Permiso | Descripción | Predeterminado |
| --- | --- | --- |
| `nexusprism.security.cleanworld` | Limpieza manual del mundo | OP |
| `nexusprism.staff.vanish` | Volverse invisible | OP |
| `nexusprism.staff.invsee` | Inspeccionar inventarios | OP |
| `nexusprism.staff.spy` | Modo espía de chat | OP |

---

## Mobs con Nivel

Cada mob hostil que aparece en el mundo recibe automáticamente un **nivel** que escala según el peligro del entorno. Los mobs de mayor nivel hacen más daño, tienen más vida y dan más XP.

### Tabla de Tirada de Nivel

Los niveles se tiran al aparecer basándose en la altura Y, dimensión y bioma. Los bonificadores se acumulan.

| Condición | Rango / Bonificador |
| --- | --- |
| Y > 64 (superficie) | Nv. 1–4 |
| Y ≤ 64 | Nv. 3–6 |
| Y ≤ 30 | Nv. 5–8 |
| Y ≤ 0 (subterráneo profundo) | Nv. 8–12 |
| Dimensión Nether | +3 al resultado |
| The End | +4 al resultado |
| Bioma Deep Dark | +5 al resultado |
| Luna de Sangre activa | +2 a todos los resultados |

Todos los resultados se limitan al rango `[1, max-level]` de la configuración.

### Formato del Nombre

| Situación | Nombre mostrado |
| --- | --- |
| Apilado + con nivel | `3x [Nv.5] Zombie` |
| Individual + con nivel | `[Nv.5] Zombie` |
| Nivel 1 (cualquier pila) | `3x Zombie` *(sin etiqueta de nivel)* |

### Fórmulas de Estadísticas

| Estadística | Fórmula |
| --- | --- |
| **Daño** | `dañoBase × (1 + (nivel-1) × multiplicadorDañoPorNivel) × contadorPila` |
| **XP** | `xpBase × contadorPila × (1 + (nivel-1) × multiplicadorXPPorNivel)` |
| **Vida** | Escalada por `multiplicadorVidaPorNivel` por nivel sobre 1 |

### Configuración (`security/antilag.yml`)

```yaml
leveled-mobs:
  enabled: true
  max-level: 20
  xp-multiplier-per-level: 0.20      # +20% XP por nivel sobre 1
  damage-multiplier-per-level: 0.15  # +15% daño por nivel sobre 1
  health-multiplier-per-level: 0.10  # +10% vida por nivel sobre 1
```

!!! note "Integración con Luna de Sangre"
    Cuando la **Luna de Sangre** está activa (ver el [módulo Events](events.md)), todas las tiradas de nivel reciben un bonificador de **+2**, haciendo a los mobs de superficie significativamente más peligrosos de noche.

---

## PlaceholderAPI

| Placeholder | Descripción |
| --- | --- |
| `%nexusprism_authenticated%` | `true` si el jugador está autenticado |
| `%nexusprism_auth_status%` | Estado de auth legible (`Autenticado`, `Pendiente`) |
