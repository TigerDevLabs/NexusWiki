# Histórico de Alterações

> Gerado automaticamente a partir dos commits do [NexusPrism](https://github.com/O-Tiger).
> Traduzido automaticamente — pequenas diferenças de fraseado são esperadas.

---
PH0


PH1

- API de energia PH2 Expose via EnergyProvider/EnergyRegistry
- Exemplo de uso do PH3 Add EnergyRegistry

PH4

- PH5 Use o campo público def.id em vez de getId() inexistente em JobProviderImpl
- PH6 Use Region.getFlag (RegionFlag) e API DuelManager corretos em ProtectionsProviderImpl
- PH7 Correta HologramLine, BloodMoonManager.getWorldName e verificação mundial EventsProviderImpl
- PH8 Resolver erros de compilação BackpackProviderImpl e MachineRegistrarImpl

---

PH0


PH1

- PH2 Use nomes corretos de métodos ChannelRegistry e ChatChannel em ChatProviderImpl

---

PH0


PH1

- Verificação premium baseada em PH2 UUID com cache persistente
- Comando PH3 Admin /isekai com início forçado e seleção de chefe
- Sistema dinâmico de custo de mana PH4 e nova capacidade de lâmina dupla
- Sistema de vinculação de teclas PH5 Ability com GUI e teclas de atalho no jogo
- PH6 Adicionar 9 interfaces de provedor, registros e MachineProcessingRegistry
- Provedores de fio PH7 em construtores de módulos e desligamentos
- PH8 Hook MachineProcessingRegistry em MachineEngine
- PH9 Adicionar projeto de modelo público com README e publicar fluxo de trabalho
- PH10 Adicionar carregador de conteúdo, registro de receita infinito e interfaces de registrador de máquina

PH11

- Renomeie nexusslime → nexusprism em todas as camadas

PH12

- Refatorando todas as referências de nexusslime para nexusprism
- Corrigido o trabalho de notificação no fluxo de trabalho do dependabot-discord. causa raiz: minhas células cerebrais se esquecem de adicionar os segredos do dependabot
PH0


PH1

- Mobs nivelados em PH2 e melhorias no empilhador de mobs
- PH3 Jobs, loja, casa de leilões e warps de jogadores
- Sistema PH4 Blood Moon, Sacrifice Arc e Isekai Boss
- Estatísticas do PH5, árvores de habilidades, habilidades, profissões e sistema de mana

PH6

- PH7 Corrija os padrões de configuração do TAB

PH8

- Adicionado um substituto para evitar falsos positivos no login/registro
- Registre eventos e módulos MMO, renomeie o plugin para NexusPrism
PH0


PH1

- Adicionados placares e personalizações MOTD ao módulo TAB
- Adicionado forge/neoforge à lista de observação, para evitar exploradores, cronômetro mais alto para mundo limpo e verificação de jogadores. Se nada for encontrado, então pula o mundo limpo
PH0


PH1

- Adicionado suporte jitpack à API
- atualize o jitpack.yml para forçar o uso do maven 3.9
- não sei
- pequena correção: adicione definição yaml ao bloco de código
PH0


PH1

- O fluxo de autenticação foi melhorado, verificando agora o tipo de conta (premium ou crackeada) e os IPs associados a ela. Para o primeiro acesso, um administrador precisará conceder confiança ao IP.
PH0


PH1

- adicionar módulo de hologramas, detector de mod/ore, antilag configurável e atualizações de spawner.
- Referências de crédito removidas (não um servidor p2w aliás)
PH0


PH1

- Fluxo de autenticação aprimorado para também detectar IP e bloquear IPs não reconhecidos
- Novas correções conectadas para fluxos de autenticação e segurança
PH0


PH1

- Arquivos de documentação atualizados
- Adicionado suporte SkinsRestorer para contas premium, as crackeadas devem usar comandos.
- Esqueci de adicionar os arquivos ao gitignore
PH0


PH1

- Fluxo de autenticação alterado para baseado em mapa
PH0


PH1

- Ações de colisão/artefato de upload de 6 para 7 no grupo gha-major
- Fluxo de autenticação aprimorado: _ Agora é baseado em sessão, tempo padrão de 2 horas
PH0


PH1

- Adicionado:
- adicionado registro de alterações
PH0


PH1

- Atualizados alguns arquivos
- Poms.xml atualizado de cada módulo
- Módulo de proteção aprimorado para ser semelhante ao RedProtection. Também adicionei alguns dos meus projetos antigos, como o chefe Echoes e a experiência de sonho
- Remova completamente a antiga dependência do nuvotifier e adicione uma imagem pública como avatar do fluxo de trabalho
- Corrigindo sed fazendo com que o URL ficasse malformado
- Adicionado suporte para executar ações do discord
PH0


PH1

- Corrigido download de importação do nuvotifier maven, adicionando-o localmente
- Crie SECURITY.md
- Votificador desativado por enquanto. Planejando adicionar novamente, mas como um código interno, não apenas uma chamada de API.
- Esqueci da dependência
- Votificador desativado no Nexus.....

PH2

- - Adicionado suporte emoji ao módulo de chat; - Agora será possível mencionar alguém entre discord <-> minecraft, usando seus nomes atuais em cada um. O usuário mencionado deve ser verificado no servidor discord para ser notificado. - Adicionadas chaves lang aos novos módulos.
PH0


PH1

- Bump org.postgresql:postgresql de 42.7.4 para 42.7.7
PH0


PH1

- Adicionado formatador de bate-papo e redirecionamentos de canal
- fluxo de trabalho atualizado do dependabot-discord
- Adicionado suporte multicrafting para níveis de itens infinitos
- Alterado para cargas úteis jq para uso mais seguro
- Corrija o recuo no README e desfaça as alterações do merge pull do dependabot (causa incompatibilidade)
PH0


PH1

- Bump com.sk89q.worldguard:worldguard-bukkit
PH0


PH1

- Loja virtual vinculada ao módulo nexusslime-web Melhore ainda mais o módulo discord, permitindo configurações através de arquivos yml.
PH0


PH1

- Coloque o grupo maven-major em 1 diretório com 2 atualizações
PH0


PH1

- Implementação da API Discord
PH0


PH1

- Testes de integração do Discord
PH0


PH1

- Atualizar modelos de problemas
- # ItemYamlLoader: suporte a modelos nomeados

PH2

- Evite o download do ProtocolLib durante a compilação (opcional em tempo de execução)
PH0


PH1

- Fluxos de trabalho atualizados e adicionado CONTRIBUTING.md
PH0


PH1

- .gitignore atualizado
- Fluxo de trabalho release.yml atualizado
PH0


PH1

- Implementar máquinas de processamento em camadas e infraestrutura de sistemas principais

PH2

- Criação de fluxos de trabalho para builds e releases
- Release.yml atualizado
- Supere o grupo gha-major com 3 atualizações
- Não sei, acabei de perder alguns campos na notificação Enviar Discord
PH0


PH1

- Confirmação inicial - Espaços reservados para itens de trabalho

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
