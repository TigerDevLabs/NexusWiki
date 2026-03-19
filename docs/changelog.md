# Changelog

> Auto-generated from [NexusPrism](https://github.com/O-Tiger) commits.
> Translated automatically — minor phrasing differences are expected.

---

## [2.0.0-BETA] — Initial Release

### ✨ Added

- Complete rewrite as a **+25-module Maven multi-module project**
- New `nexusprism-api` module providing a public API for addon developers
- All feature systems are now self-contained modules with their own lifecycle
- Switched from YAML-only persistence to **SQLite / PostgreSQL** via `nexusprism-storage`
- `CustomItemRegistry` with PDC-based item tagging (`nexusprism:id`)
- 235+ data-driven items defined in `items.yml`
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
- **nexusprism-events** — Blood Moon, Sacrifice Arc, and Isekai Boss system
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
