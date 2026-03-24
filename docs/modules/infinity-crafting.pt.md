# Módulo Infinity Crafting

Infinity Crafting é o **sistema de crafting multiblocos** do NexusPrism. Os jogadores constroem estruturas multiblocos físicas no mundo e as usam como estações de crafting avançadas. As receitas são definidas inteiramente em YAML.

---

## Visão Geral

| Funcionalidade | Descrição |
| --- | --- |
| **Estruturas multiblocos** | Estações de crafting construídas a partir de padrões específicos de blocos |
| **Receitas em YAML** | Sem Java necessário — defina receitas em `data/crafting/infinity_table/` |
| **Interface GUI** | Entrada/saída de receitas por arrastar e soltar via GUI de inventário |
| **Bloqueio por pesquisa** | Receitas podem exigir pesquisa específica para ser desbloqueadas |
| **Integração com máquinas** | Algumas receitas infinity requerem energia ou saída de máquinas como ingredientes |

---

## Configuração de Multiblocos

Os multiblocos são estruturas físicas colocadas no mundo. Seu layout é definido em `multiblocks.yml`.

### Construindo um Multiblocos

1. Reúna os blocos necessários listados na definição do multiblocos
2. Construa a estrutura na forma exata mostrada no guia
3. Clique com o botão direito no bloco controlador para abrir a GUI de crafting
4. Insira os ingredientes e colete o resultado

### Exemplo de `multiblocks.yml`

```yaml
INFINITY_TABLE:
  display-name: "&bInfinity Crafting Table"
  description: "The core multiblock for Infinity-tier crafting."
  controller: CRAFTING_TABLE
  structure:
    # Definições de camadas: Y=0 é a base, Y=1 é o meio, etc.
    layers:
      0:
        - "DDD"
        - "DCD"
        - "DDD"
      1:
        - "   "
        - " C "
        - "   "
    legend:
      D: DEEPSLATE_BRICKS
      C: CRAFTING_TABLE   # Bloco controlador
```

---

## Formato YAML de Receitas

As receitas são colocadas em `plugins/NexusPrism/data/crafting/infinity_table/` como arquivos `.yml` individuais. O nome do arquivo serve como ID da receita.

### Receita Shapeed (Com Formato)

```yaml
# data/crafting/infinity_table/nexus_core.yml
type: SHAPED
station: INFINITY_TABLE
output:
  item: NEXUS_CORE
  amount: 1

shape:
  - "GEG"
  - "EDE"
  - "GEG"

ingredients:
  G: GOLD_INGOT
  E: ENDER_PEARL
  D: DIAMOND

research-required: ADVANCED_METALLURGY    # Bloqueio de pesquisa opcional
energy-cost: 500                          # Custo de energia opcional (RF/FE)
```

### Receita Shapeless (Sem Formato)

```yaml
# data/crafting/infinity_table/star_dust.yml
type: SHAPELESS
station: INFINITY_TABLE
output:
  item: STAR_DUST
  amount: 4

ingredients:
  - GLOWSTONE_DUST
  - GLOWSTONE_DUST
  - BLAZE_POWDER
  - ENDER_PEARL
```

### Receita de Fundição (via Máquina)

```yaml
# data/crafting/infinity_table/copper_ingot.yml
type: MACHINE_SMELT
station: ELECTRIC_FURNACE
output:
  item: COPPER_INGOT
  amount: 1

input:
  item: RAW_COPPER
  amount: 1

energy-cost: 100
processing-ticks: 200
```

### Referência de Campos

| Campo | Descrição |
| --- | --- |
| `type` | `SHAPED`, `SHAPELESS`, `MACHINE_SMELT` |
| `station` | ID do multiblocos necessário para criar esta receita |
| `output.item` | ID do item de saída (personalizado do NexusPrism ou Material vanilla) |
| `output.amount` | Tamanho da pilha de saída |
| `shape` | Grade de 3 linhas para receitas shaped (3 caracteres por linha) |
| `ingredients` | Mapa de char → ID de item (shaped) ou lista de IDs de itens (shapeless) |
| `research-required` | ID da pesquisa que deve ser desbloqueada antes de esta receita aparecer |
| `energy-cost` | Energia (RF) consumida por crafting |
| `processing-ticks` | Ticks usados por receitas de máquina |

---

## Guia no Jogo

Todas as receitas infinity são visíveis no guia do jogo. Abra-o com `/nexusprism guide` e navegue até a seção do tier **Infinity**.

O guia mostra:

- Estação multiblocos necessária
- Lista de ingredientes com quantidades
- Requisito de pesquisa (se houver)
- Custo de energia (se houver)

---

## Comandos

| Comando | Uso | Permissão |
| --- | --- | --- |
| `/recipe <item>` | Mostrar receita(s) de um item | `nexusprism.recipe` |
| `/nexusprism guide` | Abrir GUI do guia de itens | `nexusprism.command` |
| `/nexusprism reload` | Recarregar todas as receitas e multiblocos | `nexusprism.admin.reload` |

---

## Permissões

| Permissão | Descrição | Padrão |
| --- | --- | --- |
| `nexusprism.recipe` | Ver receitas com `/recipe` | true |
| `nexusprism.craft` | Usar estações de crafting | true |
| `nexusprism.admin.reload` | Recarregar configurações/receitas do plugin | OP |
