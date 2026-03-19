# NexusPrism

> **Una reimplementación integral y evolución de Slimefun4** — sistemas de tecnología, magia y calidad de vida de próxima generación para servidores de Minecraft.

NexusPrism es un plugin de Spigot modular construido sobre una arquitectura Maven de +25 módulos. Incluye ítems personalizados, máquinas, redes de energía, clanes, economía, minijuegos e integraciones profundas en un único JAR ligero.

---

## Características Principales

| Categoría | Destacados |
| --- | --- |
| **Ítems Personalizados** | +235 ítems definidos en YAML |
| **Máquinas** | Crafteo multibloques, redes de energía, almacenamiento ME |
| **Economía** | Moneda dual (dinero + créditos), /sell, /baltop |
| **Clanes** | Conquista de territorio, mejoras, cofre de clan, chat de clan |
| **Esenciales** | +40 comandos QoL — homes, warps, TPA, AFK, cárcel |
| **Seguridad** | Auth BCrypt, anti-bot CAPTCHA, anti-dupe, anti-lag |
| **Discord** | Integración con bot, vinculación de cuenta, sincronización de roles |
| **Crystal Defense** | Minijuego de defensa de Cristales Ender por oleadas |
| **Mobs Personalizados** | Jefes definidos en YAML con tablas de botín y formas de IA |
| **Votifier** | Servidor Votifier V1/V2 independiente, rachas, clasificaciones |
| **Sueños** | Sistema de cutscene de sueño con variantes de pesadilla |
| **Protecciones** | Reclamación de regiones, banderas, sistema de duelo |
| **Twitch** | Vinculación de cuenta, alertas en vivo, relay de chat, sorteos |
| **PlaceholderAPI** | +30 placeholders en todos los módulos |

---

## Resumen de Módulos

```text
NexusPrism
├── nexusprism-api          API pública para desarrolladores de addons
├── nexusprism-core         Gestores principales, registro PDC, idioma
├── nexusprism-items        Almacenamiento de ítems personalizados (+235 ítems)
├── nexusprism-machines     Definiciones de máquinas, motor de procesamiento
├── nexusprism-systems      Implementación de redes de energía
├── nexusprism-integrations PlaceholderAPI, LuckPerms, SkinsRestorer
├── nexusprism-storage      Persistencia SQLite / PostgreSQL
├── nexusprism-gui          Framework de GUI
├── nexusprism-utils        Utilidades auxiliares
├── nexusprism-web          Bridge de la tienda web, kits VIP, pagos
├── nexusprism-plugin       Punto de entrada principal (Spigot)
├── nexusprism-discord      Bot JDA, webhooks, vinculación de cuenta
├── nexusprism-chat         Sistema de chat con 4 canales
├── nexusprism-ae           Almacenamiento en red estilo ME
├── nexusprism-energy       Generación de energía y redes de cables
├── nexusprism-waila        Integración WAILA/HUD
├── nexusprism-security     Auth, anti-bot, anti-lag, anti-dupe
├── nexusprism-clanes       Clanes, territorio, mejoras
├── nexusprism-economy      Dinero, créditos, precios de venta
├── nexusprism-essentials   +40 comandos QoL
├── nexusprism-crystaldefense Minijuego Crystal Defense por oleadas
├── nexusprism-custommobs   Jefes definidos en YAML
├── nexusprism-dreams       Sistema de cutscene de sueño
├── nexusprism-protections  Protección de regiones, sistema de duelo
├── nexusprism-ss           Soporte Silk Spawner
├── nexusprism-votifier     Servidor Votifier V1/V2 independiente
└── nexusprism-twitch       Integración Twitch
```

---

## Navegación Rápida

| | |
| --- | --- |
| **[Primeros Pasos](getting-started.md)** | Instalación, requisitos y primeros pasos |
| **[Módulo Core](modules/core.md)** | Ítems, sistema PDC, registro de ítems |
| **[Todos los Módulos](modules/index.md)** | Explora los 13 módulos de funcionalidades |
| **[Referencia de Comandos](reference/commands.md)** | Todos los +40 comandos con uso y permisos |
| **[Referencia de Permisos](reference/permissions.md)** | Lista completa de nodos de permisos |
| **[PlaceholderAPI](reference/placeholders.md)** | Todos los placeholders `%nexusprism_*%` |

---

## Autor

NexusPrism es desarrollado por **O-Tiger**

- Versión de API: `1.21`
- Dependencias opcionales: `PlaceholderAPI`, `LuckPerms`, `SkinsRestorer`
