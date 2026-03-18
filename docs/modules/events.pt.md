# Módulo Events

O módulo Events adiciona **eventos dinâmicos em escala mundial** que afetam todos os jogadores simultaneamente — começando com a **Lua de Sangue**, que transforma as noites em desafios de sobrevivência cada vez mais perigosos, vinculados a uma sequência por jogador e a um **Arco do Sacrifício**.

---

## Lua de Sangue

A Lua de Sangue é ativada automaticamente toda noite quando o tempo do mundo ultrapassa o **tick 13000** e é desativada ao amanhecer (**tick 23000**). Operadores do servidor também podem controlá-la manualmente.

### Efeitos Enquanto Ativa

| Efeito | Detalhe |
| --- | --- |
| Bônus de nível de mob | Todas as rolagens de Mobs com Nível recebem **+2** |
| Pagamento do emprego Caçador | Multiplicado pelo `kill-pay-multiplier` configurado (padrão ×1,5) |
| Chuva de partículas | Partículas DUST vermelhas aparecem ao redor de cada jogador online a cada 3 segundos |
| Ondas de horda | Uma horda de mobs aparece a cada `horde-interval-ticks` (padrão 5 min) |

Ao **amanhecer** (desativação), todo jogador online que sobreviveu ganha **+1** em sua sequência de sobrevivência.

### Ondas de Horda

A cada intervalo de horda, um jogador online aleatório é escolhido como alvo. **30 mobs** aparecem em um anel de 18 blocos ao redor dele: Zumbi, Esqueleto, Creeper, Aranha, Bruxa, Husk, Afogado. Todos os mobs da horda são nomeados `[Blood Moon]` em vermelho escuro.

### Comandos

| Comando | Descrição | Permissão |
| --- | --- | --- |
| `/bloodmoon` | Exibir status atual da Lua de Sangue | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon start` | Ativar a Lua de Sangue manualmente | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon stop` | Desativar a Lua de Sangue manualmente | `nexusslime.events.bloodmoon.admin` |
| `/bloodmoon status` | Saída de status detalhada | `nexusslime.events.bloodmoon.admin` |

### Configuração (`events/config.yml`)

```yaml
blood-moon:
  enabled: true
  world: world                   # O mundo onde as mudanças de tempo são monitoradas
  kill-pay-multiplier: 1.5       # Multiplicador de pagamento do Caçador durante a Lua de Sangue
  particle-interval-ticks: 60   # Com que frequência (ticks) gerar partículas por jogador
  horde-interval-ticks: 6000    # Com que frequência (ticks) disparar uma onda de horda (6000 = 5 min)
  horde-size: 30                 # Número de mobs por onda de horda
```

---

## Sequência de Sobrevivência

Cada jogador tem uma **sequência de sobrevivência à Lua de Sangue** armazenada persistentemente em SQLite (`events/events.db`).

| Evento | Mudança na Sequência |
| --- | --- |
| Sobreviver a uma noite completa de Lua de Sangue | **+1** (concedido ao amanhecer) |
| Morrer durante uma Lua de Sangue | **Resetar para 0** |

Quando a sequência atinge um **múltiplo de 7** (7, 14, 21, 28...), o jogador recebe um **Convite de Sacrifício** na próxima vez que dormir.

---

## Arco do Sacrifício

O Arco do Sacrifício é um desafio opcional de alto risco acionado pela sequência de sobrevivência. Ele se integra ao [módulo Dreams](dreams.md): quando a sequência se qualifica, dormir abre uma **GUI de escolha** em vez de uma cutscene de sonho.

### GUI de Escolha

Uma GUI de 3 linhas com duas opções:

| Slot | Item | Ação |
| --- | --- | --- |
| 11 | Lã Verde — **Aceitar** | Teleportar para a arena, julgamento de sobrevivência de 90 segundos |
| 15 | Lã Vermelha — **Recusar** | Resetar sequência, sem outra penalidade |

Fechar a GUI sem clicar conta como **Recusa**.

### Julgamento na Arena

1. O jogador é teleportado para a arena configurada (ou permanece na localização atual se não configurada)
2. **5 mobs de arena** aparecem: Zumbi, Esqueleto, Esqueleto Wither, Blaze, Aranha das Cavernas
3. Uma **contagem regressiva de 90 segundos** começa com avisos em 30s, 10s e 5s

### Resultados

| Resultado | Consequência |
| --- | --- |
| **Sobreviver** | Recompensa concedida (padrão: 3 Blocos de Diamante), transmissão para o servidor, sequência resetada |
| **Morrer** | Sequência resetada para 0 |
| **Sair/desconectar** | Sessão encerrada, tratada como falha |

### Configuração (`events/config.yml`)

```yaml
sacrifice:
  arena:
    world: ""    # Deixe em branco para usar o mundo atual do jogador
    x: 0.0
    y: 64.0
    z: 0.0
```

!!! tip "Configurando a Arena"
    Construa uma arena PvE dedicada e defina suas coordenadas em `sacrifice.arena`. Deixe `world` em branco para lutar no lugar — útil para testes.

---

## Permissões

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusslime.events.bloodmoon.admin` | Controlar a Lua de Sangue manualmente | OP |
