# Módulo Structures

O módulo Structures **injeta loot personalizado** nos baús de estruturas vanilla. Quando o servidor gera loot para qualquer estrutura suportada, o módulo adiciona (ou substitui) o conteúdo dos baús com itens definidos em `structures/loot-tables.yml` — incluindo itens personalizados do NexusPrism.

---

## Como Funciona

O módulo escuta o `LootGenerateEvent` do Paper. Quando um baú de estrutura é populado, ele:
1. Identifica a estrutura pela chave da tabela de loot
2. Procura a entrada configurada em `loot-tables.yml`
3. Rola a quantidade de itens adicionais (`min`–`max`) e injeta itens por peso

Nenhum comando é necessário — a injeção de loot é totalmente passiva.

---

## Estruturas Suportadas

| Estrutura | Injeção Padrão |
| --- | --- |
| `minecraft:dungeon` | Pergaminho de Pesquisa (Básico) |
| `minecraft:mineshaft` | Pergaminho de Pesquisa (Básico) |
| `minecraft:desert_pyramid` | Pergaminho de Pesquisa (Básico) |
| `minecraft:jungle_temple` | Pergaminho de Pesquisa (Básico) |
| `minecraft:ocean_ruin` | Pergaminho de Pesquisa (Básico) |
| `minecraft:shipwreck` | Pergaminho de Pesquisa (Básico) |
| `minecraft:pillager_outpost` | Pergaminho de Pesquisa (Básico) |
| `minecraft:stronghold` | Pergaminho de Pesquisa (Avançado) |
| `minecraft:woodland_mansion` | Pergaminho de Pesquisa (Avançado) |
| `minecraft:bastion_remnant` | Pergaminho de Pesquisa (Avançado) |
| `minecraft:end_city` | Pergaminho de Pesquisa (Infinito) |

---

## Configuração (`structures/loot-tables.yml`)

```yaml
minecraft:dungeon:
  mode: APPEND      # APPEND (adiciona ao loot vanilla) | REPLACE (substitui o loot vanilla)
  rolls:
    min: 1
    max: 2
  items:
    - material: EMERALD
      weight: 40
      amount:
        min: 1
        max: 5
    - material: ENCHANTED_BOOK
      weight: 8
      amount:
        min: 1
        max: 1
      random-enchant: true
    - nexusprism-item: RESEARCH_PARCHMENT_BASIC
      weight: 5
      amount:
        min: 1
        max: 1
```
