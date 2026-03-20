# Historial de Cambios

> Generado automáticamente desde los commits de [NexusPrism](https://github.com/O-Tiger).
> Traducido automáticamente — pueden esperarse pequeñas diferencias de redacción.

---
PH0


PH1

- PH2 Expose API de energía a través de EnergyProvider/EnergyRegistry
- Ejemplo de uso de PH3 Add EnergyRegistry

PH4

- PH5 Utilice el campo público def.id en lugar del inexistente getId() en JobProviderImpl
- PH6 Utilice la API Region.getFlag(RegionFlag) y DuelManager correcta en ProtectionsProviderImpl
- Comprobación mundial PH7 Correct HologramLine, BloodMoonManager.getWorldName y EventsProviderImpl
- PH8 Resolve errores de compilación de BackpackProviderImpl y MachineRegistrarImpl

---

PH0


PH1

- PH2 Utilice los nombres correctos de los métodos ChannelRegistry y ChatChannel en ChatProviderImpl

---

PH0


PH1

- Verificación premium basada en UUID PH2 con caché persistente
- Comando PH3 Admin /isekai con inicio forzado y selección de jefe
- Sistema dinámico de coste de maná PH4 y nueva habilidad de doble hoja
- Sistema de enlace de teclas PH5 Ability con GUI y teclas de acceso rápido en el juego
- PH6 Agregue 9 interfaces de proveedor, registros y MachineProcessingRegistry
- PH7 Cablear proveedores en constructores de módulos y paradas
- Máquina de gancho PH8 Procesamiento Registro en MachineEngine
- PH9 Agregar proyecto de plantilla pública con README y publicar flujo de trabajo
- PH10 Agregar cargador de contenido, registro de recetas infinitas e interfaces de registro de máquinas

PH11

- Cambiar el nombre de nexusslime → nexusprism en todas las capas

PH12

- Refactorización de todas las referencias desde nexusslime hasta nexusprism.
- Se corrigió el trabajo de notificación en el flujo de trabajo dependabot-discord. Causa raíz: Mis células cerebrales se olvidan de agregar los secretos del dependabot.
PH0


PH1

- Mobs nivelados PH2 y mejoras en el apilador de mobs
- Trabajos de PH3, tienda, casa de subastas y deformaciones de jugadores.
- PH4 Blood Moon, Sacrifice Arc y sistema Isekai Boss
- Estadísticas de PH5, árboles de habilidades, habilidades, profesiones y sistema de maná.

PH6

- PH7 Corregir los valores predeterminados de configuración de TAB

PH8

- Se agregó un respaldo para evitar falsos positivos al iniciar sesión/registrarse.
- Registre eventos y módulos MMO, cambie el nombre del complemento a NexusPrism
PH0


PH1

- Se agregaron marcadores y personalizaciones de MOTD al módulo TAB.
- Se agregó forge/neoforge a la lista de vigilancia, para evitar explotadores, un temporizador más alto para limpiar el mundo y un control para los jugadores. Si no se encontró ninguno, se salta la limpieza mundial.
PH0


PH1

- Se agregó soporte jitpack a la API.
- actualice jitpack.yml para forzar el uso de maven 3.9
- no sé
- corrección menor: agregue la definición de yaml al bloque de código
PH0


PH1

- Se ha mejorado el flujo de autenticación, verificando ahora el tipo de cuenta (premium o crackeada) y las IP asociadas a ella. Para acceder por primera vez, un administrador deberá otorgar confianza a la IP.
PH0


PH1

- agregue módulo de hologramas, detector de mod/mineral, antilag configurable y actualizaciones de generador.
- Referencias de crédito eliminadas (no es un servidor p2w por cierto)
PH0


PH1

- Flujo de autenticación mejorado para detectar también IP y bloquear las no reconocidas
- Nuevas correcciones cableadas para flujos de autenticación y seguridad.
PH0


PH1

- Archivos de documentación actualizados.
- Se agregó soporte para SkinsRestorer a las cuentas premium; las crackeadas deben usar comandos.
- Olvidé agregar los archivos a gitignore
PH0


PH1

- Se cambió el flujo de autenticación a basado en mapas.
PH0


PH1

- Aumentar acciones/cargar artefactos de 6 a 7 en el grupo gha-major
- Flujo de autenticación mejorado: _ Ahora se basa en sesiones, tiempo predeterminado 2 horas
PH0


PH1

- Añadido:
- registro de cambios agregado
PH0


PH1

- Actualizados algunos archivos.
- Poms.xml actualizado de cada módulo.
- Módulo de protecciones mejorado para que sea como RedProtection. También agregué algunos de mis proyectos antiguos, como Echoes boss y experiencia de ensueño.
- Elimine por completo la antigua dependencia del nuvotificador y agregue una imagen pública como avatar del flujo de trabajo.
- Se corrigió sed que causaba que la URL tuviera un formato incorrecto.
- Se agregó soporte para ejecutar acciones desde Discord.
PH0


PH1

- Se corrigió la descarga de importación de nuvotifier maven, agregándola localmente
- Crear SEGURIDAD.md
- Votificador deshabilitado por ahora. Planeando agregar nuevamente, pero como código interno, no solo como una llamada API.
- Me olvidé de la dependencia.
- Votificador desactivado en Nexus.....

PH2

- - Se agregó compatibilidad con emoji al módulo de chat; - Ahora será posible mencionar a alguien entre discord <-> minecraft, usando sus nombres actuales en cada uno. El usuario mencionado debe ser verificado en el servidor de Discord para recibir una notificación. - Se agregaron claves de idioma a los nuevos módulos.
PH0


PH1

- Bump org.postgresql:postgresql de 42.7.4 a 42.7.7
PH0


PH1

- Se agregó formateador de chat y redirecciones de canales.
- flujo de trabajo actualizado dependabot-discord
- Se agregó soporte de creación múltiple para niveles de elementos infinitos.
- Cambiado a cargas útiles jq para un uso más seguro.
- Corregir la sangría en README y deshacer los cambios de fusión del dependabot (provoca incompatibilidad)
PH0


PH1

- Bump com.sk89q.worldguard:worldguard-bukkit
PH0


PH1

- Tienda web vinculada con el módulo nexusslime-web. Mejorar aún más el módulo de discordia, permitiendo configuraciones a través de archivos yml.
PH0


PH1

- Pasar el grupo maven-major a través de 1 directorio con 2 actualizaciones
PH0


PH1

- Implementación de la API de discordia
PH0


PH1

- Pruebas de integración de Discord.
PH0


PH1

- Actualizar plantillas de problemas
- # ItemYamlLoader: admite plantillas con nombre

PH2

- Evite la descarga de ProtocolLib durante la compilación (opcional en tiempo de ejecución)
PH0


PH1

- Flujos de trabajo actualizados y agregado CONTRIBUTING.md
PH0


PH1

- Actualizado .gitignore
- Flujo de trabajo actualizado de release.yml
PH0


PH1

- Implementar máquinas de procesamiento escalonado e infraestructura de sistemas centrales.

PH2

- Creé flujos de trabajo para compilaciones y lanzamientos.
- Lanzamiento actualizado.yml
- Supera al grupo principal de gha con 3 actualizaciones
- No sé, me perdí algunos campos en la notificación Enviar discordia.
PH0


PH1

- Confirmación inicial - Marcadores de posición de elementos de trabajo

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
