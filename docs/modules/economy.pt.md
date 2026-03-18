# Módulo Economia

O módulo Economia fornece um **sistema de moeda dupla** (dinheiro e créditos), comandos de venda, placar de riqueza e configuração de preços de venda por item.

---

## Visão Geral

| Moeda | Descrição |
| --- | --- |
| **Dinheiro** (`$`) | Moeda padrão do jogo, ganha vendendo itens, votando, etc. |
| **Créditos** | Moeda premium, normalmente obtida na webstore |

---

## Comandos

| Comando | Uso | Permissão |
| --- | --- | --- |
| `/money` | Verificar seu saldo | `nexusslime.economy.money` |
| `/money <jogador>` | Verificar saldo de outro jogador | `nexusslime.economy.money` |
| `/credits` | Verificar seus créditos | `nexusslime.economy.credits` |
| `/baltop` | Top 10 jogadores mais ricos | `nexusslime.economy.baltop` |
| `/sell hand` | Vender item na mão | `nexusslime.economy.sell` |
| `/sell all` | Vender todos os itens vendáveis | `nexusslime.economy.sell` |
| `/sell inventory` | Vender inventário completo | `nexusslime.economy.sell` |
| `/worth [item]` | Verificar valor de venda do item | `nexusslime.essentials.worth` |
| `/eco give <jogador> <quantia>` | Dar dinheiro (admin) | `nexusslime.economy.admin` |
| `/eco take <jogador> <quantia>` | Remover dinheiro (admin) | `nexusslime.economy.admin` |
| `/eco set <jogador> <quantia>` | Definir saldo (admin) | `nexusslime.economy.admin` |
| `/eco reset <jogador>` | Resetar saldo (admin) | `nexusslime.economy.admin` |

---

## Permissões

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusslime.economy.money` | Ver saldos | true |
| `nexusslime.economy.credits` | Ver créditos | true |
| `nexusslime.economy.baltop` | Ver placar | true |
| `nexusslime.economy.sell` | Usar /sell | true |
| `nexusslime.economy.admin` | Comandos de admin eco | OP |

---

## Preços de Venda (`economy/sell-prices.yml`)

Configure os preços de venda por material usados pelo `/sell` e `/worth`.

```yaml
prices:
  # ── Pedra e Terra ─────────────────────────────────────────────
  COBBLESTONE:       2.0
  STONE:             3.0
  DIRT:              1.0

  # ── Madeira e Plantas ─────────────────────────────────────────
  OAK_LOG:           6.0
  WHEAT:             4.0

  # ── Minérios e Metais ─────────────────────────────────────────
  COAL:             10.0
  IRON_INGOT:       25.0
  GOLD_INGOT:       50.0
  DIAMOND:         200.0
  NETHERITE_INGOT: 1200.0

  # ── Drops de Mob ──────────────────────────────────────────────
  BLAZE_ROD:        20.0
  ENDER_PEARL:      25.0
  SHULKER_SHELL:   150.0
```

!!! tip
    Use nomes de Material (maiúsculas Bukkit). Itens não listados em `sell-prices.yml` não podem ser vendidos.

---

## PlaceholderAPI

| Placeholder | Descrição |
| --- | --- |
| `%nexusslime_money%` | Saldo de dinheiro do jogador |
| `%nexusslime_credits%` | Saldo de créditos do jogador |

---

## Empregos

Os jogadores escolhem um emprego e ganham dinheiro e XP realizando atividades relacionadas no jogo.

### Empregos Disponíveis

| Emprego | Atividades Principais |
| --- | --- |
| **Minerador** | Quebrar minérios e pedras |
| **Caçador** | Matar mobs hostis |
| **Fazendeiro** | Colher plantações |
| **Pescador** | Pescar |
| **Ferreiro** | Fundir lingotes, criar ferramentas/armaduras |
| **Encantador** | Encantar itens |
| **Alquimista** | Preparar poções |
| **Lenhador** | Cortar troncos |

Jogadores só podem ter **um emprego de cada vez**. As configurações de emprego são arquivos YAML em `economy/jobs/`.

### Fórmulas de Pagamento e XP

| Valor | Fórmula |
| --- | --- |
| **Pagamento por ação** | `base × (1 + nível × escalaPagePorNível)` |
| **XP para o próximo nível** | `xpBaseParaNível × 2^((nível-1)/10)` *(dobra a cada 10 níveis)* |

### Comandos

| Comando | Descrição | Permissão |
| --- | --- | --- |
| `/job` | Abrir GUI de empregos | `nexusslime.economy.job.use` |
| `/job join <id>` | Ingressar em um emprego | `nexusslime.economy.job.use` |
| `/job leave` | Sair do emprego atual | `nexusslime.economy.job.use` |
| `/job info [id]` | Ver estatísticas do emprego | `nexusslime.economy.job.use` |
| `/job top` | Ranking de empregos | `nexusslime.economy.job.use` |

!!! note "Bônus da Lua de Sangue"
    Durante uma Lua de Sangue, o pagamento por morte do emprego **Caçador** é multiplicado (padrão ×1,5). Veja o [módulo Events](events.md).

---

## Lojas de Baú

Os jogadores podem criar lojas no mundo colocando uma placa em (ou adjacente a) um baú.

### Criando uma Loja

1. Coloque um baú
2. Coloque uma placa na frente, em cima ou em um bloco adjacente
3. Escreva `[Shop]` na **primeira linha**
4. Escreva `BUY <preço>` na linha 2 (opcional)
5. Escreva `SELL <preço>` na linha 3 (opcional)

O plugin detecta automaticamente o baú abaixo ou adjacente à placa. O estoque é exibido automaticamente na linha 4.

### Formato da Placa

```
[Shop]
BUY 50
SELL 25
[12 no estoque]
```

### GUI da Loja

Uma GUI de 3 linhas é aberta ao clicar com botão direito na placa:

| Slot | Conteúdo |
| --- | --- |
| Centro (slot 13) | Pré-visualização do item |
| Slots 19–21 | Comprar ×1 / ×8 / ×64 |
| Slots 23–25 | Vender ×1 / ×8 / ×64 |

### Permissões

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusslime.economy.shop.create` | Criar lojas de baú | true |
| `nexusslime.economy.shop.admin` | Criar lojas admin (estoque ilimitado) | OP |

---

## Warps de Jogador

Os jogadores podem definir pontos de warp nomeados que qualquer outro jogador pode visitar.

### Comandos

| Comando | Descrição |
| --- | --- |
| `/pw set <nome>` | Criar um warp na localização atual |
| `/pw delete <nome>` | Remover um de seus warps |
| `/pw desc <nome> <texto>` | Definir uma descrição para o warp |
| `/pw icon <nome> <material>` | Definir o ícone exibido na GUI |
| `/pw list` | Navegar por todos os warps de jogadores (GUI paginada de 6 linhas) |
| `/pw visit <jogador> <nome>` | Teleportar para o warp de outro jogador |

### Limites de Warp

| Permissão | Máximo de Warps |
| --- | --- |
| `nexusslime.economy.playerwarp.unlimited` | Ilimitado |
| `nexusslime.economy.playerwarp.10` | 10 |
| `nexusslime.economy.playerwarp.3` | 3 |
| *(padrão)* | 1 |

---

## Casa de Leilões

Um quadro de listagens global onde jogadores compram e vendem itens entre si.

### Como Funciona

- Liste qualquer item da mão com `/ah sell <preço>`
- As listagens expiram após **7 dias** se não vendidas
- Itens expirados ou cancelados são devolvidos ao dono (limpeza a cada hora)
- Cada jogador pode ter até **10 listagens ativas** de cada vez

### Comandos

| Comando | Descrição | Permissão |
| --- | --- | --- |
| `/ah` | Navegar pelas listagens ativas (GUI paginada de 6 linhas) | `nexusslime.economy.ah.use` |
| `/ah sell <preço>` | Listar item na mão por um preço | `nexusslime.economy.ah.use` |
| `/ah own` | Ver suas listagens; cancelar ativas ou recuperar expiradas | `nexusslime.economy.ah.use` |
| `/ah cancel <id>` | Cancelar listagem pelo ID | `nexusslime.economy.ah.use` |
