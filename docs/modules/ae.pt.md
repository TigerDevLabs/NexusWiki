# Módulo ME Storage

O módulo ME Storage é um **sistema de armazenamento em rede estilo Applied Energistics**. Coloque um ME Controller, conecte drives e terminais via cabos e gerencie milhares de itens por uma única interface unificada.

---

## Fundamentos da Rede

Uma rede requer:
1. **ME Controller** — alimenta a rede e define o orçamento de canais
2. **Cabos** — conectam componentes; diferentes níveis fornecem diferentes quantidades de canais
3. **ME Drive** — armazena células de armazenamento (o armazenamento real de itens)
4. **ME Terminal** — o GUI onde jogadores inserem e retiram itens

Componentes além do orçamento de canais são marcados como **inativos** e não funcionam.

---

## Máquinas

| ID da Máquina | Descrição | Canais |
| --- | --- | --- |
| `me_controller` | Alimenta a rede; clique direito para status | — |
| `me_cable_glass` | Cabo básico — apenas conectividade, sem canais | 0 |
| `me_cable_smart` | Cabo padrão | 8 |
| `me_cable_dense` | Cabo de alta largura de banda | 32 |
| `me_drive` | Comporta até 10 células de armazenamento | 1 |
| `me_terminal` | GUI para inserir e retirar itens | 1 |

---

## Células de Armazenamento

| Célula | ID do Item | Capacidade | Máx. Tipos |
| --- | --- | --- | --- |
| Célula 1K | `STORAGE_CELL_1K` | 1.024 itens | 63 |
| Célula 4K | `STORAGE_CELL_4K` | 4.096 itens | 63 |
| Célula 16K | `STORAGE_CELL_16K` | 16.384 itens | 63 |
| Célula 64K | `STORAGE_CELL_64K` | 65.536 itens | 63 |
| Célula 256K | `STORAGE_CELL_256K` | 262.144 itens | 63 |

!!! warning "Quebrando um Drive"
    Ao quebrar um ME Drive, as células caem como seu material base — os conteúdos armazenados **não são dropados**. Sempre retire os itens pelo terminal antes de remover um drive.

---

## Primeiros Passos

1. Obtenha um `me_controller`, cabos, um `me_drive`, um `me_terminal` e ao menos uma célula
2. Coloque o controller, depois conecte o drive e o terminal via cabos
3. Clique com botão direito no controller para verificar se a rede está online
4. Clique com botão direito no drive e insira uma célula de armazenamento
5. Clique com botão direito no terminal para começar a gerenciar itens
