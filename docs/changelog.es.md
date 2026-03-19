# Historial de Cambios

> Generado automáticamente desde los commits de [NexusPrism](https://github.com/O-Tiger).
> Traducido automáticamente — pueden esperarse pequeñas diferencias de redacción.

---

## [2.0.0-BETA] — Lanzamiento Inicial

### ✨ Añadido

- Reescritura completa como un **proyecto Maven multi-módulo con +25 módulos**
- Nuevo módulo `nexusprism-api` que proporciona una API pública para desarrolladores de addons
- Todos los sistemas de funciones ahora son módulos independientes con su propio ciclo de vida
- Migración de persistencia YAML a **SQLite / PostgreSQL** mediante `nexusprism-storage`
- `CustomItemRegistry` con etiquetado de ítems via PDC (`nexusprism:id`)
- 235+ ítems basados en datos definidos en `items.yml`
- Sistema de tier de ítems: Básico → Avanzado → Infinito
- Árbol de investigación con desbloqueos por XP
- Soporte multi-idioma: Inglés, Portugués Brasileño, Español, Chino Simplificado
- **nexusprism-essentials** — 40+ comandos QoL (homes, warps, TPA, AFK, prisión, utilidades)
- **nexusprism-economy** — Sistema de moneda dual, `/sell`, `/baltop`, precios de venta configurables
- **nexusprism-clans** — Reclamación de territorio, árbol de mejoras, cofre de clan, chat de clan
- **nexusprism-security** — Autenticación BCrypt, anti-bot CAPTCHA, detección de VPN, anti-lag, anti-dupe
- **nexusprism-discord** — Bot JDA, vinculación de cuentas, sincronización de roles, webhooks
- **nexusprism-crystaldefense** — Minijuego cooperativo por oleadas
- **nexusprism-votifier** — Servidor Votifier V1/V2 independiente con rachas y clasificación
- **nexusprism-dreams** — Sistema de cinemática al dormir (sueños y pesadillas)
- **nexusprism-protections** — Reclamación de regiones, flags, sistema de duelo 1v1
- **nexusprism-custommobs** — Jefes definidos en YAML con formas de IA y tablas de botín
- **nexusprism-twitch** — Vinculación de cuenta, alertas en vivo, relay de chat, sorteos
- **nexusprism-ae** — Almacenamiento en red ME (estilo Applied Energistics)
- **nexusprism-energy** — Generación de energía y redes de cables
- **nexusprism-chat** — Chat de 4 canales (global, local, staff, comercio) con moderación
- **nexusprism-events** — Luna de Sangre, Arco del Sacrificio y sistema de Jefe Isekai
- **nexusprism-mmo** — Estadísticas, árboles de habilidades, habilidades, profesiones y sistema de maná
- **nexusprism-tab** — Encabezado/pie de página de la lista TAB personalizado con prefijo LuckPerms
- **nexusprism-holograms** — Hologramas de texto flotante basados en YAML
- **nexusprism-traits** — Sistema de traits con cartas de Tarot e integración con economía
- **nexusprism-rng** — Ruleta diaria, bloques de suerte, gacha, niveles de investigación
- **nexusprism-crates** — Cofres de botín con apertura animada y llaves
- **nexusprism-enchantments** — 175 encantamientos personalizados (6 rarezas, 10 tipos de activación)
- **nexusprism-structures** — Inyección de botín en estructuras (11 estructuras vanilla + API de addon)
- **nexusprism-waila** — Tooltips de máquinas WAILA/HUD
- **nexusprism-web** — Bridge de tienda web, kits VIP, procesamiento de pagos, RGPD
- **PlaceholderAPI** — 14 proveedores, 30+ placeholders en todos los módulos
- **LuckPerms** — Permisos y placeholders basados en grupo
- `MachineYamlLoader` — máquinas definidas en `machines.yml`, sin necesidad de Java
- `MachineEngine` — procesamiento asíncrono de máquinas
- Estaciones de crafteo multibloques con formato de receta YAML (`infinity_recipes/`)
- Generadores de energía: Paneles Solares, Generadores de Carbón
- Transporte de energía por cables con pérdida configurable por bloque
