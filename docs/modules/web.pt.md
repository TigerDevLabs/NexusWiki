# Módulo Web & GDPR

O módulo Web gerencia a **integração com a loja virtual**, **entrega de kits VIP**, **webhooks de pagamento** e **conformidade com a LGPD/GDPR** — dando aos jogadores controle sobre seus dados pessoais.

---

## Conformidade com LGPD/GDPR

Os jogadores podem exportar, deletar e gerenciar o consentimento de seus dados armazenados diretamente no jogo.

### Comandos

Todos os comandos GDPR são exclusivos para jogadores e não requerem permissão especial.

| Comando | Descrição |
| --- | --- |
| `/nexus gdpr` | Mostrar informações de GDPR e configurações de consentimento atuais |
| `/nexus gdpr export` | Exportar todos os dados pessoais para um arquivo JSON em `gdpr/` |
| `/nexus gdpr delete` | Deletar todos os dados pessoais (direito ao esquecimento) |
| `/nexus consent <tipo> <accept\|deny>` | Conceder ou negar um tipo específico de consentimento |

### Tipos de Consentimento

| Tipo | O que Cobre |
| --- | --- |
| `activity_tracking` | Dados de entrada/saída e tempo de jogo |
| `purchase_history` | Registros de transações |
| `discord_notifications` | Ações do jogador vinculadas ao Discord |
| `statistics` | Estatísticas e conquistas do jogador |
| `marketing` | Anúncios e promoções do servidor |

!!! info "Exclusão de dados"
    Registros financeiros mais recentes que `gdpr.legal-retention-years` são **anonimizados** em vez de deletados, para cumprir os requisitos legais mínimos de retenção. Todos os outros dados são removidos imediatamente.

---

## Integração com Loja Virtual

### Entrega de Kits VIP

Quando um jogador compra um rank ou kit na loja virtual, o pedido é colocado em fila. No próximo acesso do jogador, `auto-deliver: true` entrega o kit automaticamente.

```yaml
kits:
  VIP:
    items:
      - material: DIAMOND
        amount: 5
    commands:
      - "lp user {player} group set vip"
      - "tell {player} Bem-vindo ao VIP!"
```

---

## Configuração (`web-config.yml`)

```yaml
gdpr:
  enabled: true
  data-retention-days: 365
  legal-retention-years: 7
  allow-data-export: true
  allow-data-deletion: true

api:
  enabled: false
  endpoint: "https://seu-site.com/api"
  key: ""
  rate-limit: 60

payments:
  enabled: false
  provider: "custom"           # stripe | paypal | mercadopago | custom
  webhook-secret: ""

vip-kits:
  enabled: true
  auto-deliver: true
  verify-payment: true
```
