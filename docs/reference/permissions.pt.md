# Referência de Permissões

Lista completa de todos os nós de permissão registrados pelo NexusPrism. Nós marcados como **OP** são padrão apenas para operadores; nós marcados como **true** são concedidos a todos os jogadores por padrão.

---

## Core & Admin

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.*` | Todas as permissões | OP |
| `nexusprism.command` | Usar o comando básico `/nexusprism` | true |
| `nexusprism.admin` | Acesso administrativo geral | OP |
| `nexusprism.admin.*` | Todas as permissões administrativas | OP |
| `nexusprism.admin.reload` | Recarregar configurações do plugin | OP |
| `nexusprism.admin.give` | Dar itens personalizados | OP |
| `nexusprism.admin.debug` | Alternar modo de depuração | OP |
| `nexusprism.admin.cleardata` | Limpar dados de jogadores | OP |
| `nexusprism.bypass.protection` | Ignorar todas as proteções de região | OP |

---

## Pesquisa

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.research` | Acessar sistema de pesquisa | true |
| `nexusprism.research.all` | Desbloquear toda pesquisa instantaneamente | OP |
| `nexusprism.research.admin` | Concede acesso aos subcomandos administrativos de `/nexusprism research` (all, tier, entry) | OP |

---

## Mochilas

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.backpack.create` | Criar mochilas | true |
| `nexusprism.backpack.upgrade` | Atualizar mochilas | true |
| `nexusprism.backpack.unlimited` | Slots ilimitados de mochila | OP |

---

## Pontos de Viagem

| Permissão | Slots | Padrão |
| --- | --- | --- |
| `nexusprism.essentials.waypoints.1` | 1 ponto de viagem | true |
| `nexusprism.essentials.waypoints.5` | 5 pontos de viagem | — |
| `nexusprism.essentials.waypoints.25` | 25 pontos de viagem | — |
| `nexusprism.essentials.waypoints.unlimited` | Ilimitado | OP |
| `nexusprism.essentials.waypoint` | Acessar comandos de ponto de viagem | true |

---

## Homes

| Permissão | Slots | Padrão |
| --- | --- | --- |
| `nexusprism.essentials.homes.1` | 1 home | true |
| `nexusprism.essentials.homes.3` | 3 homes | — |
| `nexusprism.essentials.homes.10` | 10 homes | — |
| `nexusprism.essentials.homes.unlimited` | Ilimitado | OP |
| `nexusprism.essentials.home` | Usar /home, /sethome, /delhome | true |

---

## Comandos Essenciais

| Permissão | Comando | Padrão |
| --- | --- | --- |
| `nexusprism.essentials.warp.use` | `/warp` | true |
| `nexusprism.essentials.warp.admin` | `/setwarp`, `/delwarp` | OP |
| `nexusprism.essentials.back` | `/back` | true |
| `nexusprism.essentials.tpa` | `/tpa`, `/tpaccept`, `/tpdeny` | true |
| `nexusprism.essentials.spawn` | `/spawn` | true |
| `nexusprism.essentials.setspawn` | `/setspawn` | OP |
| `nexusprism.essentials.tphere` | `/tphere` | OP |
| `nexusprism.essentials.tppos` | `/tppos` | OP |
| `nexusprism.essentials.near` | `/near` | true |
| `nexusprism.essentials.fly` | `/fly` (próprio) | false |
| `nexusprism.essentials.fly.others` | `/fly <jogador>` | OP |
| `nexusprism.essentials.hat` | `/hat` | false |
| `nexusprism.essentials.god` | `/god` (próprio) | OP |
| `nexusprism.essentials.god.others` | `/god <jogador>` | OP |
| `nexusprism.essentials.heal` | `/heal` (próprio) | OP |
| `nexusprism.essentials.heal.others` | `/heal <jogador>` | OP |
| `nexusprism.essentials.feed` | `/feed` (próprio) | OP |
| `nexusprism.essentials.feed.others` | `/feed <jogador>` | OP |
| `nexusprism.essentials.nick` | `/nick` (próprio) | false |
| `nexusprism.essentials.nick.others` | `/nick <jogador>` | OP |
| `nexusprism.essentials.afk` | `/afk` | true |
| `nexusprism.essentials.workbench` | `/workbench` | true |
| `nexusprism.essentials.trash` | `/trash` | true |
| `nexusprism.essentials.anvil` | `/anvil` | OP |
| `nexusprism.essentials.grindstone` | `/grindstone` | OP |
| `nexusprism.essentials.stonecutter` | `/stonecutter` | OP |
| `nexusprism.essentials.speed` | `/speed` | OP |
| `nexusprism.essentials.seen` | `/seen` | true |
| `nexusprism.essentials.clearinventory` | `/clearinventory` (próprio) | OP |
| `nexusprism.essentials.clearinventory.others` | `/clearinventory <jogador>` | OP |
| `nexusprism.essentials.getpos` | `/getpos` | true |
| `nexusprism.essentials.playtime` | `/playtime` | true |
| `nexusprism.essentials.gamemode` | `/gamemode` | OP |
| `nexusprism.essentials.enderchest` | `/enderchest` (próprio) | true |
| `nexusprism.essentials.enderchest.others` | `/enderchest <jogador>` | OP |
| `nexusprism.essentials.repair` | `/repair` | OP |
| `nexusprism.essentials.ext` | `/ext` | OP |
| `nexusprism.essentials.exp` | `/exp` | OP |
| `nexusprism.essentials.worth` | `/worth` | true |
| `nexusprism.essentials.rules` | `/rules` | true |
| `nexusprism.essentials.skull` | `/skull` | OP |
| `nexusprism.essentials.jail.admin` | Gerenciamento de prisão | OP |
| `nexusprism.essentials.backpack` | Comandos de mochila | true |

---

## Economia

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.economy.money` | Ver saldo de dinheiro | true |
| `nexusprism.economy.baltop` | Ver placar | true |
| `nexusprism.economy.sell` | Usar /sell | true |
| `nexusprism.economy.admin` | Comandos administrativos de economia | OP |

---

## Clãs

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.clan.use` | Usar comandos de clã | true |
| `nexusprism.clan.admin` | Gerenciamento administrativo de clãs | OP |
| `nexusprism.clan.bypass-protection` | Ignorar território de clã | OP |

---

## Segurança

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.security.cleanworld` | Limpador de mundo manual | OP |
| `nexusprism.staff.vanish` | Tornar-se invisível | OP |
| `nexusprism.staff.vanish.others` | Tornar outro jogador invisível | OP |
| `nexusprism.staff.vanish.see` | Ver jogadores invisíveis | OP |
| `nexusprism.staff.invsee` | Inspecionar inventários | OP |
| `nexusprism.staff.spy` | Modo de espionagem de chat | OP |

---

## Chat

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.chat.staff` | Acessar canal de chat da equipe | OP |
| `nexusprism.chat.mute` | Silenciar jogadores | OP |
| `nexusprism.chat.mute.bypass` | Ignorar silenciamento | false |
| `nexusprism.chat.filter.bypass` | Ignorar filtro de palavras | OP |
| `nexusprism.chat.reload` | Recarregar configuração de chat | OP |
| `nexusprism.chat.color` | Usar códigos de cor no chat | OP |

---

## Proteções & Duelo

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.region.use` | Criar e gerenciar próprias regiões | true |
| `nexusprism.protect.admin` | Gerenciamento administrativo de regiões | OP |
| `nexusprism.duel.use` | Enviar e aceitar duelos | true |

---

## Crystal Defense

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.crystaldefense.use` | Entrar em arenas | true |
| `nexusprism.crystaldefense.admin` | Criar/gerenciar arenas | OP |

---

## Votifier

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.vote` | Usar `/vote` | true |
| `nexusprism.vote.top` | Usar `/votetop` | true |

---

## Custom Mobs

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.boss.admin` | Todos os comandos de boss/ovo de spawn | OP |

---

## Dreams

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.dreams.admin` | Comandos administrativos de sonhos | OP |

---

## Twitch

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.twitch.use` | Comandos básicos do Twitch | true |
| `nexusprism.twitch.staff` | Aprovar vinculações, realizar sorteios | OP |
| `nexusprism.twitch.admin` | Recarregar configuração do Twitch | OP |

---

## Silk Spawners

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.silkspawner.use` | Minerar spawners com Silk Touch | true |
| `nexusprism.silkspawner.admin` | Comandos administrativos de spawner | OP |

---

## Receitas & Kits

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.recipe` | Usar `/recipe` | true |
| `nexusprism.command.kit` | Usar `/kit` | true |
| `nexusprism.command.vip` | Usar `/vip` | true |
| `nexusprism.kit.*` | Acessar todos os kits VIP | OP |

---

## Nós de Nível de Permissão

Usados internamente para mapear cargos da equipe. Configure em `config.yml`:

| Permissão | Cargo |
| --- | --- |
| `nexusprism.level.user` | Jogador regular |
| `nexusprism.level.helper` | Auxiliar |
| `nexusprism.level.moderator` | Moderador |
| `nexusprism.level.admin` | Administrador |
| `nexusprism.level.owner` | Proprietário |
