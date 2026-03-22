# Referência PlaceholderAPI

O NexusPrism registra sua própria expansão PlaceholderAPI sob o identificador `nexusprism`. Todos os placeholders seguem o padrão `%nexusprism_<nome>%`.

**Requer:** [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) (dependência suave — instale separadamente)

---

## Economia

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_money%` | Saldo atual de dinheiro do jogador | `12500.00` |
| `%nexusprism_credits%` | Saldo de créditos do jogador | `350` |

---

## Essenciais

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_playtime%` | Tempo total de jogo (formatado) | `3d 12h 45m` |
| `%nexusprism_playtime_minutes%` | Tempo total de jogo em minutos | `5085` |
| `%nexusprism_homes%` | Número de homes definidos | `3` |
| `%nexusprism_afk%` | `true` se o jogador estiver AFK | `false` |
| `%nexusprism_afk_status%` | Status AFK legível por humanos | `AFK` / `Online` |

---

## Clãs

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_clan_name%` | Nome do clã do jogador | `Shadowborn` |
| `%nexusprism_clan_tag%` | Tag do clã | `SHD` |
| `%nexusprism_clan_role%` | Cargo do jogador no clã | `Owner` / `Officer` / `Member` |
| `%nexusprism_clan_level%` | Nível atual do clã | `5` |
| `%nexusprism_clan_members%` | Contagem de membros online | `8` |
| `%nexusprism_clan_bank%` | Saldo do banco do clã | `75000.00` |

Retorna string vazia se o jogador não estiver em um clã.

---

## Crystal Defense

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_crystal_wave%` | Número da onda atual | `7` |
| `%nexusprism_crystal_health%` | HP restante do cristal | `680.0` |
| `%nexusprism_crystal_points%` | Pontos de abate do jogador no jogo atual | `145` |
| `%nexusprism_crystal_arena%` | Nome da arena em que o jogador está | `arena1` |

Retorna string vazia se o jogador não estiver em um jogo de Crystal Defense.

---

## Segurança

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_authenticated%` | `true` se o jogador estiver logado | `true` |
| `%nexusprism_auth_status%` | Status de autenticação legível | `Authenticated` / `Pending` |

---

## Votifier

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_votes_total%` | Total de votos acumulados | `127` |
| `%nexusprism_vote_streak%` | Tamanho da sequência de votos atual | `12` |

---

## Estatísticas do Jogador

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_player_blocks_broken%` | Total de blocos quebrados | `48320` |
| `%nexusprism_player_machines_placed%` | Total de máquinas colocadas | `214` |
| `%nexusprism_player_items_crafted%` | Total de itens criados | `5630` |
| `%nexusprism_player_energy_generated%` | Total de energia gerada (RF) | `1200000` |
| `%nexusprism_player_items_smelted%` | Total de itens fundidos | `890` |
| `%nexusprism_player_research_unlocked%` | Entradas de pesquisa desbloqueadas | `34` |
| `%nexusprism_player_level%` | Nível NexusPrism do jogador | `15` |
| `%nexusprism_researched_<id>%` | `true` se uma pesquisa específica estiver desbloqueada | `true` |

---

## Mochilas

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_backpacks_owned%` | Número de mochilas que o jogador possui | `2` |

---

## Máquinas

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_machines_count%` | Total de máquinas colocadas pelo jogador | `42` |

---

## LuckPerms

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_lp_prefix%` | Prefixo LuckPerms do jogador | `&6[VIP]` |
| `%nexusprism_lp_suffix%` | Sufixo LuckPerms do jogador | `&7✦` |

Requerem que o LuckPerms esteja instalado.

---

## MMO

**Módulo obrigatório** (`nexusprism-mmo`).

| Placeholder | Retorna | Notas |
| --- | --- | --- |
| `%nexusprism_mmo_level%` | Nível de personagem MMO | inteiro |
| `%nexusprism_mmo_mana%` | Mana atual | inteiro |
| `%nexusprism_mmo_mana_max%` | Mana máxima | inteiro |
| `%nexusprism_mmo_stat_points%` | Pontos de atributo não gastos | inteiro |
| `%nexusprism_mmo_stat_strength%` | Valor de FORÇA | inteiro |
| `%nexusprism_mmo_stat_dexterity%` | Valor de DESTREZA | inteiro |
| `%nexusprism_mmo_stat_intelligence%` | Valor de INTELIGÊNCIA | inteiro |
| `%nexusprism_mmo_stat_vitality%` | Valor de VITALIDADE | inteiro |
| `%nexusprism_mmo_stat_endurance%` | Valor de RESISTÊNCIA | inteiro |
| `%nexusprism_mmo_stat_luck%` | Valor de SORTE | inteiro |
| `%nexusprism_mmo_skill_<treeid>%` | Nível na árvore de habilidades | ex: `mmo_skill_warrior` |
| `%nexusprism_mmo_profession_<profid>%` | Nível na profissão | ex: `mmo_profession_mining` |

---

## Eventos

`bloodmoon_*` funciona mesmo sem o módulo Events (retorna `false` / `1.00`).

| Placeholder | Retorna | Notas |
| --- | --- | --- |
| `%nexusprism_bloodmoon_active%` | `true` / `false` | servidor inteiro |
| `%nexusprism_bloodmoon_multiplier%` | Multiplicador de recompensa | `1.00` quando inativo |
| `%nexusprism_sacrifice_streak%` | Sequência de sobrevivência | **Módulo obrigatório** |
| `%nexusprism_in_sacrifice%` | `true` / `false` | **Módulo obrigatório** |
| `%nexusprism_isekai_active%` | `true` / `false` | **Módulo obrigatório** |

---

## Traits & RNG

**Módulo obrigatório** (`nexusprism-traits`).

| Placeholder | Retorna | Notas |
| --- | --- | --- |
| `%nexusprism_traits_research%` | Nível de pesquisa/gacha | inteiro |
| `%nexusprism_traits_count%` | Quantidade de cartas de trait atribuídas | inteiro |
| `%nexusprism_traits_cards%` | Lista separada por vírgula das cartas | `none` se vazio |

---

## Profissões (Jobs)

**Módulo obrigatório** (`nexusprism-economy`).

| Placeholder | Retorna | Notas |
| --- | --- | --- |
| `%nexusprism_job%` | ID do emprego ativo | `none` se sem emprego |
| `%nexusprism_job_level%` | Nível no emprego ativo | `0` se sem emprego |
| `%nexusprism_job_xp%` | XP no emprego ativo | `0` se sem emprego |

---

## Discord

**Módulo obrigatório** (`nexusprism-discord`).

| Placeholder | Retorna | Notas |
| --- | --- | --- |
| `%nexusprism_discord_linked%` | `true` / `false` | — |
| `%nexusprism_discord_id%` | ID snowflake do Discord | string vazia se não vinculado |

---

## Guia

| Placeholder | Descrição |
| --- | --- |
| `%nexusprism_guide_<id>%` | Entrada dinâmica do guia para ID de item/máquina |

Esses são dinâmicos — substitua `<id>` por qualquer ID de item ou máquina registrado.

---

## Core / Diversos

| Placeholder | Descrição | Exemplo |
| --- | --- | --- |
| `%nexusprism_version%` | String da versão do plugin | `2.0.0-BETA` |
| `%nexusprism_player%` | Nome de usuário do jogador | `Steve` |
| `%nexusprism_uuid%` | UUID do jogador | `069a79f4-...` |

---

## Uso em Scoreboards / TAB

```yaml
# Exemplo com o plugin TAB
header: "&bNexusPrism &7%nexusprism_version%"
tablist-name: "%nexusprism_lp_prefix%%player_name%"
scoreboard:
  title: "&b&lSuas Estatísticas"
  lines:
    - "&7Dinheiro: &a$%nexusprism_money%"
    - "&7Créditos: &b%nexusprism_credits%"
    - "&7Votos: &e%nexusprism_votes_total% &7(sequência: %nexusprism_vote_streak%)"
    - "&7Clã: &f%nexusprism_clan_name%"
    - "&7Tempo de Jogo: &f%nexusprism_playtime%"
```
