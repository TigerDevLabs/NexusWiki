# Histórico de Alterações

> Gerado automaticamente a partir dos commits do [NexusPrism](https://github.com/O-Tiger).
> Traduzido automaticamente — pequenas diferenças de fraseado são esperadas.

---

## [2.0.0-BETA] — Lançamento Inicial

### ✨ Adicionado

- Reescrita completa como um **projeto Maven multi-módulo com +25 módulos**
- Novo módulo `nexusprism-api` fornecendo uma API pública para desenvolvedores de addons
- Todos os sistemas de recursos agora são módulos independentes com ciclo de vida próprio
- Migração de persistência YAML para **SQLite / PostgreSQL** via `nexusprism-storage`
- `CustomItemRegistry` com marcação de itens via PDC (`nexusprism:id`)
- 235+ itens baseados em dados definidos em `items.yml`
- Sistema de tier de itens: Básico → Avançado → Infinito
- Árvore de pesquisa com desbloqueios por XP
- Suporte a múltiplos idiomas: Inglês, Português Brasileiro, Espanhol, Chinês Simplificado
- **nexusprism-essentials** — 40+ comandos QoL (homes, warps, TPA, AFK, prisão, utilitários)
- **nexusprism-economy** — Sistema de moeda dupla, `/sell`, `/baltop`, preços de venda configuráveis
- **nexusprism-clans** — Reivindicação de território, árvore de upgrades, baú de clã, chat de clã
- **nexusprism-security** — Autenticação BCrypt, anti-bot CAPTCHA, detecção de VPN, anti-lag, anti-dupe
- **nexusprism-discord** — Bot JDA, vinculação de contas, sincronização de cargos, webhooks
- **nexusprism-crystaldefense** — Minijogo cooperativo por ondas
- **nexusprism-votifier** — Servidor Votifier V1/V2 independente com sequências e placar
- **nexusprism-dreams** — Sistema de cutscene ao dormir (sonhos e pesadelos)
- **nexusprism-protections** — Reivindicação de regiões, flags, sistema de duelo 1v1
- **nexusprism-custommobs** — Bosses definidos em YAML com formas de IA e tabelas de loot
- **nexusprism-twitch** — Vinculação de conta, alertas ao vivo, relay de chat, sorteios
- **nexusprism-ae** — Armazenamento em rede ME (estilo Applied Energistics)
- **nexusprism-energy** — Geração de energia e redes de cabos
- **nexusprism-chat** — Chat de 4 canais (global, local, staff, comércio) com moderação
- **nexusprism-events** — Lua de Sangue, Arco do Sacrifício e sistema de Boss Isekai
- **nexusprism-mmo** — Estatísticas, árvores de habilidades, habilidades, profissões e sistema de mana
- **nexusprism-tab** — Cabeçalho/rodapé da lista TAB personalizado com prefixo LuckPerms
- **nexusprism-holograms** — Hologramas de texto flutuante baseados em YAML
- **nexusprism-traits** — Sistema de traits com cartas de Tarot e integração com economia
- **nexusprism-rng** — Roleta diária, blocos da sorte, gacha, níveis de pesquisa
- **nexusprism-crates** — Caixas de loot com abertura animada e chaves
- **nexusprism-enchantments** — 175 encantamentos personalizados (6 raridades, 10 tipos de gatilho)
- **nexusprism-structures** — Injeção de loot em estruturas (11 estruturas vanilla + API de addon)
- **nexusprism-waila** — Tooltips de máquinas WAILA/HUD
- **nexusprism-web** — Bridge de loja web, kits VIP, processamento de pagamentos, LGPD
- **PlaceholderAPI** — 14 provedores, 30+ placeholders em todos os módulos
- **LuckPerms** — Permissões e placeholders baseados em grupo
- `MachineYamlLoader` — máquinas definidas em `machines.yml`, sem necessidade de Java
- `MachineEngine` — processamento assíncrono de máquinas
- Estações de crafting multibloco com formato de receita YAML (`infinity_recipes/`)
- Geradores de energia: Painéis Solares, Geradores de Carvão
- Transporte de energia via cabos com perda configurável por bloco
