# Historial de Cambios

> Generado automáticamente desde los commits de [NexusPrism](https://github.com/O-Tiger).
> Traducido automáticamente — pueden esperarse pequeñas diferencias de redacción.

---
## [2026-05-13] · `9479dbc`


### 🔧Mantenimiento

- **dependabot**: Clasificación de riesgo + cierre automático de relaciones públicas de bajo riesgo

---

## [2026-05-13] · `f22c9c1`


### 📚 Documentación

- Agregue ATTACKS.md, NEXUSPRISM_REFERENCE.md, system-wiring.html

---

## [2026-05-13] · `f5aa66a`


### 🐛 Corregido See More

- **config**: Conecte todos los campos key_configs.yml a las configuraciones del módulo
- **machines**: Implementar TODOs obsoletos de MachineEngine
- **integrations**: Elimina el campo de complemento no utilizado y registra errores de LuckPerms

### 📚 Documentación

- Actualización README, CONTRIBUCIONES, CRÉDITOS, ECOSISTEMA

---

## [2026-05-13] · `552aa62`


### ✨Añadido See More

- **logger**: Colorea las etiquetas del módulo por prefijo

---

## [2026-05-13] · `c5966c3`


### 🐛 Corregido See More

- Protocolo de actualización **deps**:Lib 5.1.0 → 5.4.0 (net.dmulloy2 Maven Central)

---

## [2026-05-13] · `74b3432`


### 🔧Mantenimiento

- Simplifique el registro de inicio, elimine ProGuard, reduzca el ruido del Dependabot

---

## [2026-05-12] · `13f15da`


### 🔧Mantenimiento

- Carácter BOM despojado

---

## [2026-05-11] · `bcdd189`


### 🐛 Corregido See More

- **tools**: Clasifique los 2696 elementos: expanda CMD_MODULES, agregue estilos de categoría MÁGICO/SEED/MOB; regenerar todos los lotes rápidos

---

## [2026-05-11] · `7ac6735`


### ✨Añadido See More

- **events**: Agregue 6 jefes de anime, cambie el nombre de isekai → anime, AddonLoader, corrección de BOM

---

## [2026-04-29] · `bbac1d1`


### 📚 Documentación

- Actualizar CONFIGURACIONES: sección key_configs.yml, sección de lista negra, claves nexus-lynx/nexus-bot
## [2026-04-28] · `40babb7`


### ✨Añadido See More

- **security**: Lista negra de autenticación + archivo de credenciales central KeyConfig

### 🐛 Corregido See More

- **chat**: Extracto finalReason para la captura lambda en MuteCommand

---

## [2026-04-26] · `792efb0`


### ✨Añadido See More

- **discord**: Reenviar eventos de moderación a nexus-bot /api/moderation a través de HTTP

### 🔧Mantenimiento

- Agrega .rtk/ a gitignore

---

## [22/04/2026] · `3782900`


### ✨Añadido See More

- **web**: Reemplazar el receptor HTTP entrante con sondeo saliente

---

## [22/04/2026] · `762a968`


### 📚 Documentación

- Corregir la ruta de configuración de autenticación, agregar la sección canales.yml, expandir la lista de verificación

---

## [2026-04-21] · `984477f`


### 🔧 Mantenimiento

- Agregue la entrada del canal de seguridad comentada a los canales predeterminados.yml

---

## [2026-04-21] · `ddb3481`


### 🔒Seguridad

- Alerta de Discord de sesión corta por cable + agregar runbooks de operaciones/DDoS

---

## [2026-04-20] · `b322900`


### 🐛 Corregido See More

- **auth**: Omitir la autenticación de Java para reproductores Bedrock/Floodgate

### 🔒Seguridad

- Refuerzo de bot/escáner: detección de sesiones cortas, puerta de confianza automática de IP, corrección de sesión de Postgres

---

## [2026-04-20] · `a998d1f`


### 📚 Documentación

- Agregar referencia web/web-config.yml + registro de cambios de refuerzo de seguridad

---

## [2026-04-18] · `7f36abc`


### 🔒Seguridad

- Persistencia de clave AES-CBC, autenticación secreta del receptor, validación del nombre del jugador, columnas de sesión

---

## [2026-04-12] · `f52f78d`


### ✨Añadido See More

- Manejo de eventos IRC **twitch**:, recompensas de sub/animación/incursión, puerta de rifa clave
- Punto final **web**: TwitchEventReceiver para la integración del Stream Panel
- Comando **essentials**: RTP con GUI de selector mundial

### 🐛 Corregido See More

- **security**: Confirmación premium FastLogin + refuerzo de autenticación

### 🔧Mantenimiento

- **data**: Actualizaciones YAML de artículo/máquina/receta + cableado de complementos
## [2026-03-24] · `cc57494`


### ✨Añadido See More

- **fastlogin**: Scaffolda módulo nexusprism-fastlogin con autenticación premium a través de ProtocolLib

### 🐛 Corregido See More

- **mmo/segurança/encantamentos**: Corrige mensajes MMO, verificación premium y Auto Smelt
- **lang**: Mover mmo para nivel raíz de YAML (estava aninhado em economía)
- **plugin**: califica ProtectionHandler como MachineManager.ProtectionHandler
- **fastlogin**: Sustituye el protocolo de enlace RSA/AES por búsqueda en el nombre sincronizado→UUID
- **fastlogin**: Injeta UUID vía reflexão de campo (compatível Spigot e Paper)
- **fastlogin**: Injeta UUID a través de PlayerProfile en Paper, reflejo de campo en Spigot

### 🔧Mantenimiento

- Se movió el mensaje de bloqueo mmo anidado a la raíz.

---

## [2026-03-24] · `94b05a7`


### 🐛 Corregido See More

- **items**: Adiciona _templates.yml con item_template base para data/items/
- **data**: Corrección de errores de inicialización del servidor
- **items**: Corrige conflictos de CMD dos artículos comprimidos (30000-30002)

### 🔧Mantenimiento

- Corrección de escape inválido '\$" para "$"

---

## [2026-03-24] · `39476a5`

### ✨ Añadido

- **research**: Sistema de árbol de investigación basado en `researches.yml` — las entradas tienen tier (BASIC/ADVANCED/INFINITY), costo en pergaminos, dependencias y desbloqueos
- **research**: Progreso de investigación persistido en SQLite, MySQL y YAML
- **guide**: Las recetas de la Infinity Table ahora se registran automáticamente en la guía del juego
- **machines**: VOID_COLLECTOR_BLOCK y VOID_SMELTER_BLOCK añadidos (tier Infinity)
- **items**: SIGNALUM_INGOT y COMPRESSED_DIAMOND añadidos a items.yml
- **discord**: ConsoleLogHandler — reenvía la salida de la consola del servidor a un canal de Discord
- **guide**: Los íconos de categoría y tier de la guía ahora son configurables mediante `gui_items.yml`; los desarrolladores de addons pueden registrar íconos de categoría personalizados sin modificar Java

### 🔧 Mantenimiento

- **config**: Todos los archivos de datos reestructurados bajo la jerarquía `data/` (`data/items/`, `data/machines/<tier>/`, `data/crafting/`, `data/smelting/`, `data/crafting/infinity_table/`)
- **config**: Archivos `items.yml`, `machines.yml` y `recipes.yml` en la raíz eliminados — reemplazados por la estructura `data/`
- **recipes**: Las recetas de máquinas ahora se definen en línea dentro del bloque de la máquina bajo la clave `recipes:`
- **recipes**: El prefijo `nexus:ITEM_ID` ahora está soportado en todos los archivos YAML de recetas para referenciar ítems personalizados

### 🐛 Corregido

- **storage**: Claves de configuración renombradas de `storage.*` a `database.*` para coincidir con `config.yml`
- **storage**: La migración de MySQL < 8 (`ALTER TABLE ADD COLUMN`) ya no usa `IF NOT EXISTS` — captura el código de error 1060
- **research**: ResearchManager ahora se recarga correctamente con `/nexus reload`

### ⚖️ Legal

- Licencia cambiada de MIT a propietaria — Todos los derechos reservados

---

## [22/03/2026] · `7260628`


### 🔧Mantenimiento

- **release**: Agregar versión de entradas y lista de cambios a flujo de trabajo_dispatch

---

## [22/03/2026] · `1a79a0f`


### ✨Añadido See More

- **tab,protections,essentials**: Animações nomeadas, ordenação por grupo, GUI de banderas, casas dinámicas

---

## [2026-03-22] · `5b49358`


### ✨ Añadido

- **discord,events**: GamePresence TYPE|texto, probabilidad de Blood Moon, incrustaciones de muerte/logro

### 🐛 Corregido

- **enchantments**: Agregar dependencia nexusprism-core para LanguageManager
- **tab**: Parámetro corregido ausente en el constructor TabCommand

### 📚 Documentación

- Actualización del registro de cambios, configuraciones y marcadores de posición (22/03/2026)

### 🔧 Mantenimiento

- Modificación general: LanguageManager integrado en todos los módulos

---

## [2026-03-21] · `83b864b`


### 🔧 Mantenimiento

- Se agregó la opción de votación del servidor para restablecer el servidor MC. Basado en el trabajo de gnomomuitoloco (en Discord)

## [2026-03-20] · `e6356c5`


### ✨ Añadido

- **discord,integrations**: Agregar control de panel, votación de servidor y proveedores PAPI

---

## [2026-03-19] · `bb5ecb9`


### ✨ Añadido

- **energy**: Exponer API de energía mediante EnergyProvider/EnergyRegistry
- **addon-example**: Agregar ejemplo de uso de EnergyRegistry

### 🐛 Corregido

- **economy**: Usar campo público def.id en lugar del inexistente getId() en JobProviderImpl
- **protections**: Usar Region.getFlag(RegionFlag) y API DuelManager correctos en ProtectionsProviderImpl
- **providers**: Corregir HologramLine, BloodMoonManager.getWorldName y verificación de mundo en EventsProviderImpl
- **plugin**: Resolver errores de compilación en BackpackProviderImpl y MachineRegistrarImpl

---

## [2026-03-19] · `1875bb0`


### 🐛 Corregido

- **chat**: Usar los nombres correctos de métodos ChannelRegistry y ChatChannel en ChatProviderImpl

---

## [2026-03-19] · `55c634e`


### ✨ Añadido

- **security**: Verificación premium basada en UUID con caché persistente
- **events**: Comando admin /isekai con inicio forzado y selección de jefe
- **mmo**: Sistema dinámico de coste de maná y nueva habilidad de doble hoja
- **mmo**: Sistema de asignación de teclas de habilidades con GUI y atajos en el juego
- **api**: Agregar 9 interfaces de proveedor, registros y MachineProcessingRegistry
- **modules**: Cablear proveedores en constructores de módulos y paradas
- **machines**: Conectar MachineProcessingRegistry al MachineEngine
- **addon-example**: Agregar proyecto de plantilla pública con README y flujo de publicación
- **api**: Agregar cargador de contenido, registro de recetas infinitas e interfaces de registro de máquinas

### ♻️ Modificado

- Renombrar nexusslime → nexusprism en todas las capas

### 🔧 Mantenimiento

- Refactorizando todas las referencias de nexusslime a nexusprism
- Se corrigió el job de notificación en el flujo de trabajo dependabot-discord. Causa raíz: mis células cerebrales olvidaron agregar los secretos del dependabot

## [2026-03-18] · `ca5db45`


### ✨ Añadido

- **security**: Mobs nivelados y mejoras en el apilador de mobs
- **economy**: Jobs, tienda, casa de subastas y warps de jugadores
- **events**: Blood Moon, Arco del Sacrificio y sistema de Jefe Isekai
- **mmo**: Estadísticas, árboles de habilidades, habilidades, profesiones y sistema de maná

### 🐛 Corregido

- **tab**: Corregir los valores predeterminados de configuración del TAB

### 🔧 Mantenimiento

- Se agregó un respaldo para evitar falsos positivos al iniciar sesión/registrarse
- Registrar módulos Events y MMO, renombrar el plugin a NexusPrism

## [2026-03-16] · `cc4853a`


### 🔧 Mantenimiento

- Se agregaron marcadores y personalizaciones de MOTD al módulo TAB
- Se agregó forge/neoforge a la lista de vigilancia para evitar explotadores, mayor tiempo para limpiar el mundo y verificación de jugadores. Si no se encontró ninguno, se omite la limpieza

## [2026-03-10] · `a92e2ee`


### 🔧 Mantenimiento

- Se agregó soporte jitpack a la API
- Actualizado jitpack.yml para forzar el uso de maven 3.9
- no sé
- Corrección menor: agregar definición yaml al bloque de código

## [2026-03-09] · `e5a7a7f`


### 🔧 Mantenimiento

- Se ha mejorado el flujo de autenticación, verificando ahora el tipo de cuenta (premium o crackeada) y las IP asociadas. Para el primer acceso, un administrador deberá otorgar confianza a la IP.

## [2026-03-08] · `6676d8d`


### 🔧 Mantenimiento

- Agregar módulo de hologramas, detector de mod/mineral, antilag configurable y mejoras de spawner.
- Referencias de crédito eliminadas (no es un servidor p2w)

## [2026-03-04] · `b9749a0`


### 🔧 Mantenimiento

- Flujo de autenticación mejorado para detectar también IP y bloquear las no reconocidas
- Nuevas correcciones conectadas para flujos de autenticación y seguridad

## [2026-03-02] · `e5562d2`


### 🔧 Mantenimiento

- Archivos de documentación actualizados
- Se agregó soporte para SkinsRestorer a las cuentas premium; las crackeadas deben usar comandos.
- Olvidé agregar los archivos al .gitignore

## [2026-03-01] · `f5f4ee5`


### 🔧 Mantenimiento

- Se cambió el flujo de autenticación a basado en mapas

## [2026-02-28] · `bfc7f2f`


### 🔧 Mantenimiento

- Bump actions/upload-artifact de 6 a 7 en el grupo gha-major
- Flujo de autenticación mejorado: ahora se basa en sesiones, tiempo predeterminado 2 horas

## [2026-02-27] · `4b773aa`


### 🔧 Mantenimiento

- Añadido:
- registro de cambios agregado

## [2026-02-26] · `8d8020d`


### 🔧 Mantenimiento

- Actualizados algunos archivos
- Poms.xml actualizado de cada módulo
- Módulo de protecciones mejorado para ser como RedProtection. También agregué algunos de mis proyectos antiguos, como el boss Echoes y la experiencia de ensueño
- Eliminada completamente la antigua dependencia del nuvotifier y agregada una imagen pública como avatar del flujo de trabajo
- Se corrigió sed que causaba que la URL tuviera un formato incorrecto
- Se agregó soporte para ejecutar acciones desde Discord

## [2026-02-25] · `9b39ccd`


### 🔧 Mantenimiento

- Se corrigió la descarga de importación de nuvotifier maven, agregándola localmente
- Crear SECURITY.md
- Votificador deshabilitado por ahora. Planificando agregar nuevamente, pero como código interno, no solo como una llamada API.
- Me olvidé de la dependencia
- Votificador desactivado en Nexus.....

### 🔧 Mantenimiento

- Se agregó compatibilidad con emoji al módulo de chat; ahora será posible mencionar a alguien entre discord <-> minecraft, usando sus nombres actuales en cada plataforma. El usuario mencionado debe estar verificado en el servidor de Discord para recibir una notificación. Se agregaron claves de idioma a los nuevos módulos.

## [2026-02-24] · `6b1c020`


### 🔧 Mantenimiento

- Bump org.postgresql:postgresql de 42.7.4 a 42.7.7

## [2026-02-23] · `93ac56c`


### 🔧 Mantenimiento

- Se agregó formateador de chat y redirecciones de canales
- Flujo de trabajo dependabot-discord actualizado
- Se agregó soporte de crafteo múltiple para tiers de ítems infinitos
- Cambiado a payloads jq para un uso más seguro
- Corregir la sangría en README y deshacer los cambios de merge pull del dependabot (provoca incompatibilidad)

## [2026-02-21] · `265156e`


### 🔧 Mantenimiento

- Bump com.sk89q.worldguard:worldguard-bukkit

## [2026-02-11] · `7681a88`


### 🔧 Mantenimiento

- Tienda web vinculada con el módulo nexusslime-web. Mejorado aún más el módulo discord, permitiendo configuraciones a través de archivos yml.

## [2026-02-07] · `1600a94`


### 🔧 Mantenimiento

- Bump del grupo maven-major en 1 directorio con 2 actualizaciones

## [2026-02-04] · `7dc0811`


### 🔧 Mantenimiento

- Implementación de la API de Discord

## [2026-01-28] · `955cfc5`


### 🔧 Mantenimiento

- Pruebas de integración de Discord

## [2026-01-20] · `fe77e92`


### 🔧 Mantenimiento

- Actualizar plantillas de issues
- ItemYamlLoader: admite plantillas con nombre

### 🔧 Mantenimiento

- Evitar la descarga de ProtocolLib durante la compilación (opcional en tiempo de ejecución)

## [2026-01-19] · `06bbb4b`


### 🔧 Mantenimiento

- Flujos de trabajo actualizados y agregado CONTRIBUTING.md

## [2026-01-18] · `7d5b8ab`


### 🔧 Mantenimiento

- .gitignore actualizado
- Flujo de trabajo release.yml actualizado

## [2026-01-17] · `3fcae81`


### ✨ Añadido

- Implementar máquinas de procesamiento escalonado e infraestructura de sistemas principales

### 🔧 Mantenimiento

- Creados flujos de trabajo para compilaciones y lanzamientos
- release.yml actualizado
- Bump del grupo gha-major con 3 actualizaciones
- No sé, me perdí algunos campos en la notificación de Discord

## [2026-01-16] · `5771bc7`


### 🔧 Mantenimiento

- Confirmación inicial — Marcadores de posición de ítems funcionando

---

## [2.0.0-BETA] — Lanzamiento Inicial

### ✨ Añadido

- Reescritura completa como un **proyecto Maven multi-módulo con +25 módulos**
- Nuevo módulo `nexusprism-api` que proporciona una API pública para desarrolladores de addons
- Todos los sistemas de funciones ahora son módulos independientes con su propio ciclo de vida
- Migración de persistencia YAML a **SQLite / PostgreSQL** mediante `nexusprism-storage`
- `CustomItemRegistry` con etiquetado de ítems via PDC (`nexusprism:id`)
- 500+ ítems basados en datos definidos en `items.yml`
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
