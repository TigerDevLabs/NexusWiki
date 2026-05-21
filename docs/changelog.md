# Changelog

> Auto-generated from [NexusPrism](https://github.com/TigerDevLabs/NexusPrism) commits.
> Translated automatically — minor phrasing differences are expected.

---

## [2026-05-21] · `69ac4f3`


### 🐛 Fixed

- **ci**: Pass changelog through env var to avoid bash syntax errors

---

## [2026-05-21] · `cf363dd`


### 🐛 Fixed

- **ci**: Fix 403 push, bad action versions, and wrong branch triggers

---

## [2026-05-21] · `e488545`


### 🔧 Maintenance

- Removed BOM on the start of file

---

## [2026-05-21] · `2f25103`


### ✨ Added

- **plugin**: Phase 2 NexusLynxReporter — push heartbeat/logs/config to Railway
- **reporter**: REDACT filter + configurable log/alert levels
- **anti-dupe**: Block-break dupe prevention across rng/mmo/traits

### 🐛 Fixed

- **reporter**: Extend REDACT filter to cover JDBC connection URLs
- **discord**: Translate server status messages to Portuguese

### ♻️ Changed

- **config**: Centralize all secrets in key_configs.yml
- **reporter**: Remove per-key filter from pushConfig — key_configs.yml is the only skipped file
- **config**: Key_configs.yml holds secrets only — non-sensitive keys moved to module files

---

## [2026-05-14] · `bab3917`


### ✨ Added

- **i18n**: Wire LanguageManager into security, protections, clans modules
- **i18n**: Wire LanguageManager into MachineManager, SilkSpawners, Twitch; add all new lang keys to 4 locales
- **i18n**: Migrate gui/mmo/web/ae/energy/essentials/protections to LanguageManager

## [2026-05-13] · `3cfce4c`


### ✨ Added

- **i18n**: Wire TagGUI/RtpWorldGUI to LanguageManager + add LanguageSelectGUI

---

## [2026-05-13] · `2201b42`


### 📚 Documentation

- **config**: Annotate key_configs.yml with source env var for each key

---

## [2026-05-13] · `191f461`


### 🔧 Maintenance

- **deps**: Bump actions/upload-artifact from 4 to 7
- Migrate org references from O-Tiger to TigerDevLabs

## [2026-05-02] · `ba0ebd5`


### 🔧 Maintenance

- **deps**: Bump org.postgresql:postgresql

---

## [2026-05-13] · `820739c`


### ✨ Added

- **logger**: Colorize module tags by prefix

### 🐛 Fixed

- **deps**: Upgrade ProtocolLib 5.1.0 → 5.4.0 (net.dmulloy2 Maven Central)
- **config**: Wire all key_configs.yml fields to module configs
- **machines**: Implement MachineEngine stale TODOs
- **integrations**: Remove unused Plugin field, log LuckPerms errors

### 📚 Documentation

- Update README, CONTRIBUTING, CREDITS, ECOSYSTEM
- Add ATTACKS.md, NEXUSPRISM_REFERENCE.md, system-wiring.html

### 🔧 Maintenance

- Simplify startup log, remove ProGuard, reduce Dependabot noise
- **deps**: Bump actions/upload-artifact from 4 to 7
- Added Staff warning on medium risk Pr's

### 🔧 Maintenance

- **dependabot**: Risk classification + auto-close low-risk PRs

## [2026-05-12] · `13f15da`


### 🔧 Maintenance

- Stripped BOM character

## [2026-05-11] · `bcdd189`


### ✨ Added

- **events**: Add 6 anime bosses, rename isekai→anime, AddonLoader, BOM fix

### 🐛 Fixed

- **tools**: Classify all 2696 items — expand CMD_MODULES, add MAGICAL/SEED/MOB category styles; regenerate all prompt batches

## [2026-04-29] · `bbac1d1`


### 📚 Documentation

- Update CONFIGURATIONS — key_configs.yml section, blacklist section, nexus-lynx/nexus-bot keys

## [2026-04-28] · `40babb7`


### ✨ Added

- **security**: Auth blacklist + KeyConfig central credentials file

### 🐛 Fixed

- **chat**: Extract finalReason for lambda capture in MuteCommand

---

## [2026-05-02] · `ba0ebd5`


### 🔧 Maintenance

- **deps**: Bump org.postgresql:postgresql

---

## [2026-05-13] · `820739c`


### 🔧 Maintenance

- Added Staff warning on medium risk Pr's

---

## [2026-05-13] · `9479dbc`


### 🔧 Maintenance

- **dependabot**: Risk classification + auto-close low-risk PRs

---

## [2026-05-13] · `f22c9c1`


### 📚 Documentation

- Add ATTACKS.md, NEXUSPRISM_REFERENCE.md, system-wiring.html

---

## [2026-05-13] · `f5aa66a`


### 🐛 Fixed

- **config**: Wire all key_configs.yml fields to module configs
- **machines**: Implement MachineEngine stale TODOs
- **integrations**: Remove unused Plugin field, log LuckPerms errors

### 📚 Documentation

- Update README, CONTRIBUTING, CREDITS, ECOSYSTEM

---

## [2026-05-13] · `552aa62`


### ✨ Added

- **logger**: Colorize module tags by prefix

---

## [2026-05-13] · `c5966c3`


### 🐛 Fixed

- **deps**: Upgrade ProtocolLib 5.1.0 → 5.4.0 (net.dmulloy2 Maven Central)

---

## [2026-05-13] · `74b3432`


### 🔧 Maintenance

- Simplify startup log, remove ProGuard, reduce Dependabot noise

---

## [2026-05-12] · `13f15da`


### 🔧 Maintenance

- Stripped BOM character

---

## [2026-05-11] · `bcdd189`


### 🐛 Fixed

- **tools**: Classify all 2696 items — expand CMD_MODULES, add MAGICAL/SEED/MOB category styles; regenerate all prompt batches

---

## [2026-05-11] · `7ac6735`


### ✨ Added

- **events**: Add 6 anime bosses, rename isekai→anime, AddonLoader, BOM fix

---

## [2026-04-29] · `bbac1d1`


### 📚 Documentation

- Update CONFIGURATIONS — key_configs.yml section, blacklist section, nexus-lynx/nexus-bot keys

## [2026-04-28] · `40babb7`


### ✨ Added

- **security**: Auth blacklist + KeyConfig central credentials file

### 🐛 Fixed

- **chat**: Extract finalReason for lambda capture in MuteCommand

---

## [2026-04-26] · `792efb0`


### ✨ Added

- **discord**: Forward moderation events to nexus-bot /api/moderation via HTTP

### 🔧 Maintenance

- Add .rtk/ to gitignore

---

## [2026-04-22] · `3782900`


### ✨ Added

- **web**: Replace inbound HTTP receiver with outbound polling

---

## [2026-04-22] · `762a968`


### 📚 Documentation

- Fix auth config path, add channels.yml section, expand checklist

---

## [2026-04-21] · `984477f`


### 🔧 Maintenance

- Add commented security channel entry to default channels.yml

---

## [2026-04-21] · `ddb3481`


### 🔒 Security

- Wire short-session Discord alert + add ops/ DDoS runbooks

---

## [2026-04-20] · `b322900`


### 🐛 Fixed

- **auth**: Bypass Java auth for Bedrock/Floodgate players

### 🔒 Security

- Bot/scanner hardening — short-session detection, IP auto-trust gate, Postgres session fix

---

## [2026-04-20] · `a998d1f`


### 📚 Documentation

- Add web/web-config.yml reference + security hardening changelog

---

## [2026-04-18] · `7f36abc`


### 🔒 Security

- AES-CBC key persistence, receiver secret auth, player name validation, session columns

---

## [2026-04-12] · `f52f78d`


### ✨ Added

- **twitch**: IRC event handling, sub/cheer/raid rewards, key raffle gate
- **web**: TwitchEventReceiver endpoint for Stream Panel integration
- **essentials**: RTP command with world selector GUI

### 🐛 Fixed

- **security**: FastLogin premium confirmation + auth hardening

### 🔧 Maintenance

- **data**: Item/machine/recipe YAML updates + plugin wiring

## [2026-03-24] · `cc57494`


### ✨ Added

- **fastlogin**: Scaffolda módulo nexusprism-fastlogin com autenticação premium via ProtocolLib

### 🐛 Fixed

- **mmo/segurança/encantamentos**: Corrige mensagens MMO, verificação premium e Auto Smelt
- **lang**: Move mmo para nível raiz do YAML (estava aninhado em economy)
- **plugin**: Qualifica ProtectionHandler como MachineManager.ProtectionHandler
- **fastlogin**: Substitui handshake RSA/AES por lookup assíncrono nome→UUID
- **fastlogin**: Injeta UUID via reflexão de campo (compatível Spigot e Paper)
- **fastlogin**: Injeta UUID via PlayerProfile no Paper, reflexão de campo no Spigot

### 🔧 Maintenance

- Moved nested mmo block message to root

---

## [2026-03-24] · `94b05a7`


### 🐛 Fixed

- **items**: Adiciona _templates.yml com item_template base para data/items/
- **data**: Corrige erros de inicialização do servidor
- **items**: Corrige conflitos de CMD dos itens comprimidos (30000-30002)

### 🔧 Maintenance

- Correção de escape inválido '\$" para "$"

---

## [2026-03-24] · `39476a5`

### ✨ Added

- **research**: Research tree system driven by `researches.yml` — entries have tier (BASIC/ADVANCED/INFINITY), parchment cost, dependencies, and unlocks
- **research**: Research progress persisted in SQLite, MySQL, and YAML
- **guide**: Infinity Table recipes now auto-registered in the in-game guide
- **machines**: VOID_COLLECTOR_BLOCK and VOID_SMELTER_BLOCK added (tier Infinity)
- **items**: SIGNALUM_INGOT and COMPRESSED_DIAMOND added to items.yml
- **discord**: ConsoleLogHandler — forwards server console output to a Discord channel
- **guide**: Category and tier icons for the guide are now YAML-driven via `gui_items.yml`; addon devs can register custom category icons without touching Java

### 🔧 Maintenance

- **config**: All data files restructured under `data/` hierarchy (`data/items/`, `data/machines/<tier>/`, `data/crafting/`, `data/smelting/`, `data/crafting/infinity_table/`)
- **config**: Root-level `items.yml`, `machines.yml`, `recipes.yml` removed — superseded by `data/` structure
- **recipes**: Machine recipes now defined inline inside the machine block under a `recipes:` key
- **recipes**: `nexus:ITEM_ID` prefix now supported in all recipe YAML files for referencing custom items

### 🐛 Fixed

- **storage**: Config keys renamed from `storage.*` to `database.*` to match `config.yml`
- **storage**: MySQL < 8 migration (`ALTER TABLE ADD COLUMN`) no longer uses `IF NOT EXISTS` — catches error code 1060 instead
- **research**: ResearchManager now reloads correctly on `/nexus reload`

### ⚖️ Legal

- License changed from MIT to proprietary All Rights Reserved

---

## [2026-03-22] · `7260628`


### 🔧 Maintenance

- **release**: Adicionar inputs version e changelist ao workflow_dispatch

---

## [2026-03-22] · `1a79a0f`


### ✨ Added

- **tab,protections,essentials**: Animações nomeadas, ordenação por grupo, GUI de flags, homes dinâmico

---

## [2026-03-22] · `5b49358`


### ✨ Added

- **discord,events**: GamePresence TYPE|text, Blood Moon chance, death/achievement embeds

### 🐛 Fixed

- **enchantments**: Add nexusprism-core dep for LanguageManager
- **tab**: Corrigido parâmetro ausente no construtor TabCommand

### 📚 Documentation

- Atualização de changelog, configurações e placeholders (2026-03-22)

### 🔧 Maintenance

- Alteração Geral: LanguageManager integrado em todos os módulos

---

## [2026-03-21] · `83b864b`


### 🔧 Maintenance

- Added server vote option to reset the MC server. Based on gnomomuitoloco ( on discord ) work

## [2026-03-20] · `e6356c5`


### ✨ Added

- **discord,integrations**: Add panel control, server vote, and PAPI providers

---

## [2026-03-19] · `bb5ecb9`


### ✨ Added

- **energy**: Expose energy API via EnergyProvider/EnergyRegistry
- **addon-example**: Add EnergyRegistry usage example

### 🐛 Fixed

- **economy**: Use public field def.id instead of nonexistent getId() in JobProviderImpl
- **protections**: Use correct Region.getFlag(RegionFlag) and DuelManager API in ProtectionsProviderImpl
- **providers**: Correct HologramLine, BloodMoonManager.getWorldName, and EventsProviderImpl world check
- **plugin**: Resolve BackpackProviderImpl and MachineRegistrarImpl compile errors

---

## [2026-03-19] · `1875bb0`


### 🐛 Fixed

- **chat**: Use correct ChannelRegistry and ChatChannel method names in ChatProviderImpl

---

## [2026-03-19] · `55c634e`


### ✨ Added

- **security**: UUID-based premium verification with persistent cache
- **events**: Admin /isekai command with force-start and boss selection
- **mmo**: Dynamic mana cost system and new dual-blade ability
- **mmo**: Ability key binding system with GUI and in-game hotkeys
- **api**: Add 9 provider interfaces, registries, and MachineProcessingRegistry
- **modules**: Wire providers into module constructors and shutdowns
- **machines**: Hook MachineProcessingRegistry into MachineEngine
- **addon-example**: Add public template project with README and publish workflow
- **api**: Add content loader, infinity recipe registry, and machine registrar interfaces

### ♻️ Changed

- Rename nexusslime → nexusprism across all layers

### 🔧 Maintenance

- Refactoring all references from nexusslime to nexusprism
- Fixed notify job on dependabot-discord workflow. root cause: My brain cells forget to  add the dependabot secrets

## [2026-03-18] · `ca5db45`


### ✨ Added

- **security**: Leveled mobs and mob stacker enhancements
- **economy**: Jobs, shop, auction house, and player warps
- **events**: Blood Moon, Sacrifice Arc, and Anime Boss system
- **mmo**: Stats, skill trees, abilities, professions, and mana system

### 🐛 Fixed

- **tab**: Correct TAB config defaults

### 🔧 Maintenance

- Added a fallback to prevent false positives on login / register
- Register Events and MMO modules, rename plugin to NexusPrism

## [2026-03-16] · `cc4853a`


### 🔧 Maintenance

- Added scoreboards and MOTD customizations  to TAB module
- Added forge/neoforge to the watchlist, to prevent exploiters, higher timer for clear world and a check for players. If none was found then skips world clean

## [2026-03-10] · `a92e2ee`


### 🔧 Maintenance

- Added jitpack support to API
- update the jitpack.yml to force use of maven 3.9
- idk
- minor fix: add yaml definition to code block

## [2026-03-09] · `e5a7a7f`


### 🔧 Maintenance

- The authentication flow has been improved, now verifying the account type (premium or cracked) and the IPs associated with it. For first-time access, an administrator will need to grant trust to the IP..

## [2026-03-08] · `6676d8d`


### 🔧 Maintenance

- add holograms module, mod/ore detector, configurable antilag, and spawner upgrades.
- Removed credit references ( not a p2w server btw )

## [2026-03-04] · `b9749a0`


### 🔧 Maintenance

- Improved Auth Flow to also detect IP and blocks unrecognized ones
- Wired new fixes for auth and security flows

## [2026-03-02] · `e5562d2`


### 🔧 Maintenance

- Updated documentation files
- Added SkinsRestorer support to premium accounts, cracked ones must use commands.
- Forgot to add the files to gitignore

## [2026-03-01] · `f5f4ee5`


### 🔧 Maintenance

- Changed auth flow to map-based

## [2026-02-28] · `bfc7f2f`


### 🔧 Maintenance

- Bump actions/upload-artifact from 6 to 7 in the gha-major group
- Improved Auth flow: _ Now it's session based, default time 2 hours

## [2026-02-27] · `4b773aa`


### 🔧 Maintenance

- Added:
- added changelog

## [2026-02-26] · `8d8020d`


### 🔧 Maintenance

- Updated some files
- Updated poms.xml of each module
- Improved Protections Module to be like RedProtection Also added some of my old projects, like Echoes boss, and dreaming experience
- Completly remove old nuvotifier dependency and add a public image as avatar of workflow
- Fixing sed causing the URL to be malformated
- Added support to running actions from discord

## [2026-02-25] · `9b39ccd`


### 🔧 Maintenance

- Fixed nuvotifier maven import download, by adding it locally
- Create SECURITY.md
- Disabled Votifier for now. Planning out on add again, but as a Internal code, not just a API call.
- Forgot about the dependency
- Votifier disabled on Nexus.....

### 🔧 Maintenance

- - Added emoji support to chat module; - Now it will be possible to mention someone between discord <-> minecraft, using their currently names on each. The mentioned user must be verified on the discord server to get notified. - Added lang keys to the new modules.

## [2026-02-24] · `6b1c020`


### 🔧 Maintenance

- Bump org.postgresql:postgresql from 42.7.4 to 42.7.7

## [2026-02-23] · `93ac56c`


### 🔧 Maintenance

- Added chat formatter and channel redirects
- updated dependabot-discord workflow
- Added multicrafting support for infinity items tiers
- Changed to jq payloads for safier use
- Correct indent on README and undo the changes of merge pull from dependabot ( causes incompability)

## [2026-02-21] · `265156e`


### 🔧 Maintenance

- Bump com.sk89q.worldguard:worldguard-bukkit

## [2026-02-11] · `7681a88`


### 🔧 Maintenance

- Linked webstore with nexusslime-web module Improve even more discord module, allowing configurations through yml files.

## [2026-02-07] · `1600a94`


### 🔧 Maintenance

- Bump the maven-major group across 1 directory with 2 updates

## [2026-02-04] · `7dc0811`


### 🔧 Maintenance

- Discord API implementation

## [2026-01-28] · `955cfc5`


### 🔧 Maintenance

- Discord integration testings

## [2026-01-20] · `fe77e92`


### 🔧 Maintenance

- Update issue templates
- ﻿# ItemYamlLoader: support named templates

### 🔧 Maintenance

- Avoid ProtocolLib download during build (optional at runtime)

## [2026-01-19] · `06bbb4b`


### 🔧 Maintenance

- Updated workflows and added CONTRIBUTING.md

## [2026-01-18] · `7d5b8ab`


### 🔧 Maintenance

- Updated .gitignore
- Updated release.yml workflow

## [2026-01-17] · `3fcae81`


### ✨ Added

- Implement tiered processing machines and Core Systems Infrastructure

### 🔧 Maintenance

- Created workflows for builds and release
- Updated release.yml
- Bump the gha-major group with 3 updates
- Idk, I just missed some fields on Send Discord notification

## [2026-01-16] · `5771bc7`


### 🔧 Maintenance

- Initial Commit - Working Items Placeholders

---

## [2.0.0-BETA] — Initial Release

### ✨ Added

- Complete rewrite as a **+25-module Maven multi-module project**
- New `nexusprism-api` module providing a public API for addon developers
- All feature systems are now self-contained modules with their own lifecycle
- Switched from YAML-only persistence to **SQLite / PostgreSQL** via `nexusprism-storage`
- `CustomItemRegistry` with PDC-based item tagging (`nexusprism:id`)
- 500+ data-driven items defined in `items.yml`
- Item tier system: Basic → Advanced → Infinity
- Research tree with XP-gated unlocks
- Multi-language support: English, Brazilian Portuguese, Spanish, Simplified Chinese
- **nexusprism-essentials** — 40+ QoL commands (homes, warps, TPA, AFK, jail, utility)
- **nexusprism-economy** — Dual-currency system, `/sell`, `/baltop`, configurable sell prices
- **nexusprism-clans** — Territory claiming, upgrade tree, clan chest, clan chat
- **nexusprism-security** — BCrypt auth, CAPTCHA anti-bot, VPN detection, anti-lag, anti-dupe
- **nexusprism-discord** — JDA bot, account linking, role sync, webhooks, GitHub Actions monitoring
- **nexusprism-crystaldefense** — Wave-based cooperative minigame
- **nexusprism-votifier** — Standalone Votifier V1/V2 server with streaks and leaderboard
- **nexusprism-dreams** — Sleep cutscene system (dreams and nightmares)
- **nexusprism-protections** — Region claiming, flags, 1v1 duel system
- **nexusprism-custommobs** — YAML-defined bosses with AI forms and loot tables
- **nexusprism-twitch** — Account linking, live alerts, chat relay, viewer giveaways
- **nexusprism-ae** — ME (Applied Energistics-style) network storage
- **nexusprism-energy** — Energy generation and cable networks
- **nexusprism-chat** — 4-channel chat (global, local, staff, trade) with moderation
- **nexusprism-events** — Blood Moon, Sacrifice Arc, and Anime Boss system
- **nexusprism-mmo** — Stats, skill trees, abilities, professions, and mana system
- **nexusprism-tab** — Custom TAB list header/footer with LuckPerms prefix
- **nexusprism-holograms** — YAML-driven floating text holograms
- **nexusprism-traits** — Tarot card trait system with economy integration
- **nexusprism-rng** — Daily spin wheel, lucky blocks, gacha, research levels
- **nexusprism-crates** — Key-based loot crates with animated openings
- **nexusprism-enchantments** — 175 custom enchants (6 rarities, 10 trigger types)
- **nexusprism-structures** — Structure loot injection (11 vanilla structures + addon API)
- **nexusprism-waila** — WAILA/HUD machine tooltips
- **nexusprism-web** — Webstore delivery bridge, VIP kits, payment handling, GDPR
- **PlaceholderAPI** — 14 providers, 30+ placeholders across all modules
- **LuckPerms** — Permissions and group-based placeholders
- `MachineYamlLoader` — machines defined in `machines.yml`, no Java required
- `MachineEngine` — async machine processing
- Multiblock crafting stations with YAML recipe format (`infinity_recipes/`)
- Energy generators: Solar Panels, Coal Generators
- Cable-based energy transport with configurable loss per block
