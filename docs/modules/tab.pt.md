# Módulo TAB

O módulo TAB personaliza a **lista de jogadores** (overlay TAB) com cabeçalhos e rodapés formatados, prefixo de rank do LuckPerms, indicador de ping colorido, placar animado e personalização do MOTD.

---

## Funcionalidades

| Funcionalidade | Descrição |
| --- | --- |
| **Cabeçalho / Rodapé** | Cabeçalho e rodapé animados com suporte a PlaceholderAPI |
| **Formatação de Nome** | Nomes na lista TAB exibem o prefixo e sufixo do rank do LuckPerms |
| **Indicador de Ping** | Ping colorido ao lado do nome de cada jogador |
| **Placar** | Placar lateral por jogador com linhas configuráveis e placeholders PAPI |
| **Personalização do MOTD** | Descrição do servidor configurável globalmente |

---

## Comandos

| Comando | Uso | Permissão |
| --- | --- | --- |
| `/ntab reload` | Recarregar configuração do TAB | `nexusslime.tab.admin` |

---

## Permissões

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusslime.tab.admin` | Recarregar configuração do TAB | OP |

---

## Configuração (`tab/config.yml`)

```yaml
tab:
  enabled: true

  # Cabeçalho e rodapé exibidos na lista de jogadores
  # Suporta códigos de cor & e placeholders PlaceholderAPI
  header:
    - ""
    - "&b&lNexusSlime &8— &7Skyblock"
    - ""
  footer:
    - ""
    - "&7Online: &f%server_online% &8/ &f%server_max_players%"
    - "&7Ping: &f%player_ping%ms"
    - ""

  # Formato do nome de cada jogador na lista
  # {prefix} = prefixo LuckPerms, {name} = nome, {suffix} = sufixo
  name-format: "{prefix}&f{name}{suffix}"

  # Exibir ping como texto colorido ao lado do nome
  ping-display:
    enabled: true
    format: "&8[{ping}ms]"
    thresholds:
      good: 80        # Abaixo disso = verde
      medium: 150     # Abaixo disso = amarelo; acima = vermelho

scoreboard:
  enabled: true
  title: "&b&lNexusSlime"
  update-ticks: 20   # Taxa de atualização (20 ticks = 1 segundo)
  lines:
    - ""
    - "&7Jogador: &f%player_name%"
    - "&7Dinheiro: &a$%nexusslime_money%"
    - "&7Clã: &b%nexusslime_clan_name%"
    - ""
    - "&eplay.nexusslime.net"
    - ""

motd:
  enabled: false
  lines:
    - "&b&lNexusSlime &r&7— Skyblock MMO"
    - "&7Entre e explore!"
```

### Campos de Configuração

| Campo | Descrição |
| --- | --- |
| `tab.header` / `tab.footer` | Linhas exibidas acima/abaixo da lista. Suporta `&` e PlaceholderAPI. |
| `tab.name-format` | Formato do nome de cada jogador. Use `{prefix}`, `{name}`, `{suffix}`. |
| `ping-display.thresholds` | Valores de ping (ms) para alternar entre verde/amarelo/vermelho. |
| `scoreboard.title` | Texto no topo do placar lateral. |
| `scoreboard.lines` | Linhas do placar (de cima para baixo). Suporta PlaceholderAPI. |
| `scoreboard.update-ticks` | Frequência de atualização. 20 ticks = 1 segundo. |
| `motd.lines` | Duas linhas de descrição na lista de servidores. Suporta `&`. |

---

## PlaceholderAPI

O módulo TAB funciona com qualquer placeholder do PlaceholderAPI em cabeçalho, rodapé e linhas do placar. Veja a [referência de PlaceholderAPI](../reference/placeholders.md) para todos os placeholders `%nexusslime_*%` disponíveis.
