# Módulo Core

O módulo Core é a base do NexusPrism. Ele gerencia o registro de itens personalizados, o sistema de marcação PDC (PersistentDataContainer), o motor de máquinas, a árvore de pesquisa, mochilas e pontos de viagem.

---

## Sistema de Itens Personalizados

Todos os itens personalizados são definidos em `plugins/NexusPrism/items.yml`. O plugin já vem com **mais de 235 itens** de fábrica.

### Exemplo de `items.yml`

```yaml
COPPER_DUST:
  category: DUST
  tier: BASIC
  display-name: "&fCopper Dust"
  lore:
    - "&7A fine copper powder."
  material: PAPER
  custom-model-data: 1001
  glow: false
  stackable: true
  max-stack: 64

NEXUS_PICKAXE:
  category: TOOL
  tier: ADVANCED
  display-name: "&bNexus Pickaxe"
  lore:
    - "&7Mines at incredible speed."
    - "&8Tier: Advanced"
  material: DIAMOND_PICKAXE
  custom-model-data: 2005
  glow: true
  enchantments:
    EFFICIENCY: 5
    UNBREAKING: 3
```

### Categorias de Itens

| Categoria | Descrição |
| --- | --- |
| `DUST` | Pós de crafting (cobre, estanho, prata…) |
| `INGOT` | Lingotes de metal processados |
| `TOOL` | Ferramentas e armas personalizadas |
| `MACHINE` | Blocos de máquina posicionáveis |
| `COMPONENT` | Placas de circuito, engrenagens, etc. |
| `RESOURCE` | Recursos brutos de crafting |
| `ENERGY` | Componentes de energia |
| `BACKPACK` | Itens de mochila |

### Tiers de Itens (`NexusTier`)

| Tier | Descrição |
| --- | --- |
| `BASIC` | Tier inicial — sem pesquisa necessária |
| `ADVANCED` | Requer pesquisa básica |
| `INFINITY` | Tier final — requer pergaminhos |

---

## Sistema PDC

O NexusPrism usa o **PersistentDataContainer** do Minecraft para marcar itens personalizados, máquinas e dados de jogadores. Cada item do NexusPrism carrega uma chave PDC `nexusprism:id` que o identifica de forma única.

Classes principais:

- `CustomItemRegistry` — registra e resolve todos os itens personalizados
- `NexusItemIdResolver` — resolve IDs de itens do PDC
- `NexusItemMigrator` — migra itens legados para novos IDs

---

## Sistema de Pesquisa

Os jogadores desbloqueiam itens e máquinas gastando XP em pesquisa. A pesquisa é escalonada — **Básica → Avançada → Infinity**.

```yaml
# researches.yml
COPPER_PROCESSING:
  tier: BASIC
  xp-cost: 10
  display-name: "&fCopper Processing"
  description: "Unlock copper dust, copper ingots, and basic machines."
  unlocks:
    - COPPER_DUST
    - COPPER_INGOT
    - BASIC_CRUSHER
```

| Permissão | Descrição |
| --- | --- |
| `nexusprism.research` | Usar o sistema de pesquisa (padrão: true) |
| `nexusprism.research.all` | Desbloquear toda a pesquisa instantaneamente (OP) |

---

## Mochilas

Mochilas são recipientes de armazenamento portáteis. Os jogadores começam com uma mochila básica e podem atualizá-la.

### Comandos

| Comando | Uso | Permissão |
| --- | --- | --- |
| `/backpack open` | Abrir sua mochila | `nexusprism.essentials.backpack` |
| `/backpack open <id>` | Abrir uma mochila específica | `nexusprism.essentials.backpack` |
| `/backpack list` | Listar todas as mochilas | `nexusprism.essentials.backpack` |

### Permissões

| Permissão | Descrição |
| --- | --- |
| `nexusprism.backpack.create` | Criar mochilas (padrão: true) |
| `nexusprism.backpack.upgrade` | Atualizar mochilas (padrão: true) |
| `nexusprism.backpack.unlimited` | Slots ilimitados de mochila (OP) |

---

## Pontos de Viagem

Pontos de viagem são pontos de viagem rápida pessoais salvos pelo jogador.

### Comandos de Pontos de Viagem

| Comando | Uso | Permissão |
| --- | --- | --- |
| `/waypoint create <nome>` | Criar um ponto de viagem | `nexusprism.essentials.waypoint` |
| `/waypoint delete <nome>` | Excluir um ponto de viagem | `nexusprism.essentials.waypoint` |
| `/waypoint list` | Listar todos os pontos de viagem | `nexusprism.essentials.waypoint` |
| `/waypoint tp <nome>` | Teleportar para um ponto de viagem | `nexusprism.essentials.waypoint` |
| `/waypoint info <nome>` | Mostrar detalhes do ponto de viagem | `nexusprism.essentials.waypoint` |

Aliases: `/wp`

### Permissões de Limite de Slots

| Permissão | Slots |
| --- | --- |
| `nexusprism.essentials.waypoints.1` | 1 (padrão) |
| `nexusprism.essentials.waypoints.5` | 5 |
| `nexusprism.essentials.waypoints.25` | 25 |
| `nexusprism.essentials.waypoints.unlimited` | Ilimitado (OP) |

---

## Comandos Principais do Plugin

| Comando | Uso | Permissão |
| --- | --- | --- |
| `/nexusprism help` | Mostrar ajuda | `nexusprism.command` |
| `/nexusprism info` | Informações do plugin | `nexusprism.command` |
| `/nexusprism reload` | Recarregar todas as configurações | `nexusprism.admin.reload` |
| `/nexusprism give <jogador> <item>` | Dar um item personalizado | `nexusprism.admin.give` |
| `/nexusprism guide` | Abrir o guia de itens | `nexusprism.command` |
| `/nexusprism modules` | Listar módulos carregados | `nexusprism.command` |
| `/nexusprism machine info <id>` | Informações da máquina | `nexusprism.command` |
| `/nexusprism machine list` | Listar máquinas | `nexusprism.command` |
| `/nexusprism energy info <loc>` | Informações do nó de energia | `nexusprism.command` |
| `/nexusprism energy network` | Visualização da rede de energia | `nexusprism.command` |

Aliases: `/ns`, `/nexus`, `/slime`, `/nslime`

---

## Suporte a Idiomas

O NexusPrism vem com quatro arquivos de idioma:

| Arquivo | Idioma |
| --- | --- |
| `lang/en_US.yml` | Inglês (padrão) |
| `lang/pt_BR.yml` | Português Brasileiro |
| `lang/es_ES.yml` | Espanhol |
| `lang/zh_CN.yml` | Chinês (Simplificado) |

Defina o idioma ativo em `config.yml`:

```yaml
settings:
  language: en_US
```
