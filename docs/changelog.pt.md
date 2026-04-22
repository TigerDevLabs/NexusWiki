# Histórico de Alterações

> Gerado automaticamente a partir dos commits do [NexusPrism](https://github.com/O-Tiger).
> Traduzido automaticamente — pequenas diferenças de fraseado são esperadas.

---
## [2026-04-22] · `3782900`


### ✨ Adicionado

- **web**: Substitua o receptor HTTP de entrada por pesquisa de saída

---

## [2026-04-22] · `762a968`


### 📚 Documentação

- Corrija o caminho de configuração de autenticação, adicione a seção Channels.yml, expanda a lista de verificação

---

## [2026-04-21] · `984477f`


### 🔧 Manutenção

- Adicionar entrada de canal de segurança comentada ao canal padrão.yml

---

## [2026-04-21] · `ddb3481`


### 🔒 Segurança

- Alerta Discord de sessão curta + adição de runbooks de operações/DDoS

---

## [2026-04-20] · `b322900`


### 🐛 Corrigido

- **auth**: Ignorar autenticação Java para jogadores Bedrock/Floodgate

### 🔒 Segurança

- Proteção de bot/scanner — detecção de sessões curtas, porta de confiança automática de IP, correção de sessão Postgres

---

## [2026-04-20] · `a998d1f`


### 📚 Documentação

- Adicionar referência web/web-config.yml + changelog de reforço de segurança

---

## [2026-04-18] · `7f36abc`


### 🔒 Segurança

- Persistência de chave AES-CBC, autenticação secreta do receptor, validação de nome de jogador, colunas de sessão

---

## [2026-04-12] · `f52f78d`


### ✨ Adicionado

- **twitch**: Tratamento de eventos IRC, recompensas de sub/cheer/raid, sorteio de chaves
- Endpoint **web**: TwitchEventReceiver para integração com Stream Panel
- Comando **essentials**: RTP com GUI do seletor mundial

### 🐛 Corrigido

- **security**: Confirmação premium FastLogin + proteção de autenticação

### 🔧Manutenção

- **data**: Atualizações YAML de item/máquina/receita + fiação de plugin
## [2026-03-24] · `cc57494`


### ✨ Adicionado

- **fastlogin**: Scaffolda módulo nexusprism-fastlogin com autenticação premium via ProtocolLib

### 🐛 Corrigido

- **mmo/segurança/encantamentos**: Corrige mensagens MMO, seleção premium e Auto Smelt
- **lang**: Move mmo para nível raiz do YAML (estava aninhado em economia)
- **plugin**: Qualifica ProtectionHandler como MachineManager.ProtectionHandler
- **fastlogin**: Substitui handshake RSA/AES por lookup assíncrono nome→UUID
- **fastlogin**: Injeta UUID via reflexão de campo (compatível com Spigot e Paper)
- **fastlogin**: Insira UUID via PlayerProfile no Paper, reflexão de campo no Spigot

### 🔧Manutenção

- Mensagem de bloco MMO aninhada movida para root

---

## [2026-03-24] · `94b05a7`


### 🐛 Corrigido

- **items**: Adiciona _templates.yml com item_template base para data/items/
- **data**: Corrige erros de inicialização do servidor
- **items**: Corrige conflitos de CMD dos itens comprimidos (30000-30002)

### 🔧Manutenção

- Correção de escape inválido '\$" para "$"

---

## [2026-03-24] · `39476a5`

### ✨ Adicionado

- **research**: Sistema de árvore de pesquisa baseado em `researches.yml` — entradas têm tier (BASIC/ADVANCED/INFINITY), custo em pergaminhos, dependências e desbloqueios
- **research**: Progresso de pesquisa persistido em SQLite, MySQL e YAML
- **guide**: Receitas da Infinity Table agora são registradas automaticamente no guia do jogo
- **machines**: VOID_COLLECTOR_BLOCK e VOID_SMELTER_BLOCK adicionados (tier Infinity)
- **items**: SIGNALUM_INGOT e COMPRESSED_DIAMOND adicionados ao items.yml
- **discord**: ConsoleLogHandler — encaminha a saída do console do servidor para um canal do Discord
- **guide**: Ícones de categoria e tier do guia agora são configuráveis via `gui_items.yml`; desenvolvedores de addons podem registrar ícones de categoria personalizados sem alterar Java

### 🔧 Manutenção

- **config**: Todos os arquivos de dados reestruturados sob a hierarquia `data/` (`data/items/`, `data/machines/<tier>/`, `data/crafting/`, `data/smelting/`, `data/crafting/infinity_table/`)
- **config**: Arquivos `items.yml`, `machines.yml` e `recipes.yml` na raiz removidos — substituídos pela estrutura `data/`
- **recipes**: Receitas de máquinas agora definidas inline dentro do bloco da máquina sob a chave `recipes:`
- **recipes**: Prefixo `nexus:ITEM_ID` agora suportado em todos os arquivos YAML de receitas para referenciar itens personalizados

### 🐛 Corrigido

- **storage**: Chaves de configuração renomeadas de `storage.*` para `database.*` para corresponder ao `config.yml`
- **storage**: Migração do MySQL < 8 (`ALTER TABLE ADD COLUMN`) não usa mais `IF NOT EXISTS` — captura o código de erro 1060
- **research**: ResearchManager agora recarrega corretamente no `/nexus reload`

### ⚖️ Legal

- Licença alterada de MIT para proprietária — Todos os Direitos Reservados

---

## [2026-03-22] · `7260628`


### 🔧Manutenção

- **release**: Adicionar inputs version e changelist ao workflow_dispatch

---

## [2026-03-22] · `1a79a0f`


### ✨ Adicionado

- **tab,protections,essentials**: Animações nomeadas, ordenação por grupo, GUI de bandeiras, casas dinâmicas

---

## [2026-03-22] · `5b49358`


### ✨ Adicionado

- **discord,events**: GamePresence TYPE | texto, chance de Blood Moon, incorporações de morte/conquista

### 🐛 Corrigido

- **enchantments**: Adicionar dependência nexusprism-core para LanguageManager
- **tab**: Corrigido parâmetro ausente no construtor TabCommand

### 📚 Documentação

- Atualização de changelog, configurações e placeholders (22/03/2026)

### 🔧 Manutenção

- Alteração Geral: LanguageManager integrado em todos os módulos

---

## [2026-03-21] · `83b864b`


### 🔧 Manutenção

- Adicionada opção de votação no servidor para redefinir o servidor MC. Baseado no trabalho do gnomomuitoloco (no discord)

## [2026-03-20] · `e6356c5`


### ✨ Adicionado

- **discord,integrations**: Adicionar controle de painel, votação de servidor e provedores PAPI

---

## [2026-03-19] · `bb5ecb9`


### ✨ Adicionado

- **energy**: Expor API de energia via EnergyProvider/EnergyRegistry
- **addon-example**: Adicionar exemplo de uso do EnergyRegistry

### 🐛 Corrigido

- **economy**: Usar campo público def.id em vez de getId() inexistente em JobProviderImpl
- **protections**: Usar Region.getFlag(RegionFlag) correto e API DuelManager em ProtectionsProviderImpl
- **providers**: Corrigir HologramLine, BloodMoonManager.getWorldName e verificação de mundo em EventsProviderImpl
- **plugin**: Resolver erros de compilação em BackpackProviderImpl e MachineRegistrarImpl

---

## [2026-03-19] · `1875bb0`


### 🐛 Corrigido

- **chat**: Usar nomes corretos de métodos ChannelRegistry e ChatChannel em ChatProviderImpl

---

## [2026-03-19] · `55c634e`


### ✨ Adicionado

- **security**: Verificação premium baseada em UUID com cache persistente
- **events**: Comando admin /isekai com início forçado e seleção de boss
- **mmo**: Sistema dinâmico de custo de mana e nova habilidade de lâmina dupla
- **mmo**: Sistema de vinculação de teclas de habilidades com GUI e atalhos no jogo
- **api**: Adicionar 9 interfaces de provedor, registros e MachineProcessingRegistry
- **modules**: Conectar provedores nos construtores de módulos e desligamentos
- **machines**: Conectar MachineProcessingRegistry ao MachineEngine
- **addon-example**: Adicionar projeto de template público com README e fluxo de publicação
- **api**: Adicionar carregador de conteúdo, registro de receita infinita e interfaces de registrador de máquina

### ♻️ Alterado

- Renomear nexusslime → nexusprism em todas as camadas

### 🔧 Manutenção

- Refatorando todas as referências de nexusslime para nexusprism
- Corrigido o job de notificação no workflow do dependabot-discord. Causa raiz: minhas células cerebrais se esquecem de adicionar os segredos do dependabot

## [2026-03-18] · `ca5db45`


### ✨ Adicionado

- **security**: Mobs nivelados e melhorias no empilhador de mobs
- **economy**: Jobs, loja, casa de leilões e warps de jogadores
- **events**: Blood Moon, Arco do Sacrifício e sistema de Boss Isekai
- **mmo**: Estatísticas, árvores de habilidades, habilidades, profissões e sistema de mana

### 🐛 Corrigido

- **tab**: Corrigir padrões de configuração do TAB

### 🔧 Manutenção

- Adicionado um substituto para evitar falsos positivos no login/registro
- Registrar módulos Events e MMO, renomear o plugin para NexusPrism

## [2026-03-16] · `cc4853a`


### 🔧 Manutenção

- Adicionados placares e personalizações de MOTD ao módulo TAB
- Adicionado forge/neoforge à lista de observação para evitar exploradores, maior timer para limpeza de mundo e verificação de jogadores. Se nenhum for encontrado, pula a limpeza

## [2026-03-10] · `a92e2ee`


### 🔧 Manutenção

- Adicionado suporte jitpack à API
- Atualizado o jitpack.yml para forçar o uso do maven 3.9
- não sei
- pequena correção: adicionar definição yaml ao bloco de código

## [2026-03-09] · `e5a7a7f`


### 🔧 Manutenção

- O fluxo de autenticação foi melhorado, verificando agora o tipo de conta (premium ou crackeada) e os IPs associados a ela. Para o primeiro acesso, um administrador precisará conceder confiança ao IP.

## [2026-03-08] · `6676d8d`


### 🔧 Manutenção

- Adicionar módulo de hologramas, detector de mod/minério, antilag configurável e atualizações de spawner.
- Referências de crédito removidas (não é um servidor p2w)

## [2026-03-04] · `b9749a0`


### 🔧 Manutenção

- Fluxo de autenticação aprimorado para também detectar IP e bloquear IPs não reconhecidos
- Novas correções conectadas para fluxos de autenticação e segurança

## [2026-03-02] · `e5562d2`


### 🔧 Manutenção

- Arquivos de documentação atualizados
- Adicionado suporte SkinsRestorer para contas premium; as crackeadas devem usar comandos.
- Esqueci de adicionar os arquivos ao .gitignore

## [2026-03-01] · `f5f4ee5`


### 🔧 Manutenção

- Fluxo de autenticação alterado para baseado em mapa

## [2026-02-28] · `bfc7f2f`


### 🔧 Manutenção

- Bump actions/upload-artifact de 6 para 7 no grupo gha-major
- Fluxo de autenticação aprimorado: agora é baseado em sessão, tempo padrão de 2 horas

## [2026-02-27] · `4b773aa`


### 🔧 Manutenção

- Adicionado:
- adicionado registro de alterações

## [2026-02-26] · `8d8020d`


### 🔧 Manutenção

- Atualizados alguns arquivos
- Atualizado o poms.xml de cada módulo
- Módulo de proteções aprimorado para ser semelhante ao RedProtection. Também adicionei alguns dos meus projetos antigos, como o boss Echoes e a experiência de sonho
- Removida completamente a antiga dependência do nuvotifier e adicionada uma imagem pública como avatar do workflow
- Corrigido sed que causava URL malformada
- Adicionado suporte para executar ações a partir do discord

## [2026-02-25] · `9b39ccd`


### 🔧 Manutenção

- Corrigido o download de importação do nuvotifier maven, adicionando-o localmente
- Criar SECURITY.md
- Votificador desativado por enquanto. Planejando adicionar novamente, mas como código interno, não apenas uma chamada de API.
- Esqueci da dependência
- Votificador desativado no Nexus.....

### 🔧 Manutenção

- Adicionado suporte a emoji ao módulo de chat; agora será possível mencionar alguém entre discord <-> minecraft, usando seus nomes atuais em cada plataforma. O usuário mencionado deve ser verificado no servidor discord para ser notificado. Adicionadas chaves de idioma aos novos módulos.

## [2026-02-24] · `6b1c020`


### 🔧 Manutenção

- Bump org.postgresql:postgresql de 42.7.4 para 42.7.7

## [2026-02-23] · `93ac56c`


### 🔧 Manutenção

- Adicionado formatador de chat e redirecionamentos de canal
- Workflow do dependabot-discord atualizado
- Adicionado suporte de multicrafting para tiers de itens infinitos
- Alterado para payloads jq para uso mais seguro
- Corrigir recuo no README e desfazer as alterações do merge pull do dependabot (causa incompatibilidade)

## [2026-02-21] · `265156e`


### 🔧 Manutenção

- Bump com.sk89q.worldguard:worldguard-bukkit

## [2026-02-11] · `7681a88`


### 🔧 Manutenção

- Loja virtual vinculada ao módulo nexusslime-web. Melhorado ainda mais o módulo discord, permitindo configurações através de arquivos yml.

## [2026-02-07] · `1600a94`


### 🔧 Manutenção

- Bump do grupo maven-major em 1 diretório com 2 atualizações

## [2026-02-04] · `7dc0811`


### 🔧 Manutenção

- Implementação da API do Discord

## [2026-01-28] · `955cfc5`


### 🔧 Manutenção

- Testes de integração do Discord

## [2026-01-20] · `fe77e92`


### 🔧 Manutenção

- Atualizar templates de issues
- ItemYamlLoader: suporte a templates nomeados

### 🔧 Manutenção

- Evitar download do ProtocolLib durante a compilação (opcional em tempo de execução)

## [2026-01-19] · `06bbb4b`


### 🔧 Manutenção

- Workflows atualizados e adicionado CONTRIBUTING.md

## [2026-01-18] · `7d5b8ab`


### 🔧 Manutenção

- .gitignore atualizado
- Workflow release.yml atualizado

## [2026-01-17] · `3fcae81`


### ✨ Adicionado

- Implementar máquinas de processamento em camadas e infraestrutura dos sistemas principais

### 🔧 Manutenção

- Criados workflows para builds e releases
- release.yml atualizado
- Bump do grupo gha-major com 3 atualizações
- Não sei, acabei de perder alguns campos na notificação Enviar Discord

## [2026-01-16] · `5771bc7`


### 🔧 Manutenção

- Commit inicial — Placeholders de itens funcionando

---

## [2.0.0-BETA] — Lançamento Inicial

### ✨ Adicionado

- Reescrita completa como um **projeto Maven multi-módulo com +25 módulos**
- Novo módulo `nexusprism-api` fornecendo uma API pública para desenvolvedores de addons
- Todos os sistemas de recursos agora são módulos independentes com ciclo de vida próprio
- Migração de persistência YAML para **SQLite / PostgreSQL** via `nexusprism-storage`
- `CustomItemRegistry` com marcação de itens via PDC (`nexusprism:id`)
- 500+ itens baseados em dados definidos em `items.yml`
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
