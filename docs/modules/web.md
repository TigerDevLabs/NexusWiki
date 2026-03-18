# Web & GDPR Module

The Web module handles **webstore integration**, **VIP kit delivery**, **payment webhooks**, and **GDPR compliance** — giving players control over their personal data.

---

## GDPR Compliance

Players can export, delete, and manage consent for their stored data directly in-game.

### Commands

All GDPR commands are player-only and require no special permission (GDPR compliance requires they be accessible to all players).

| Command | Description |
| --- | --- |
| `/nexus gdpr` | Show GDPR info and current consent settings |
| `/nexus gdpr export` | Export all personal data to a JSON file in `gdpr/` |
| `/nexus gdpr delete` | Delete all personal data (right to erasure) |
| `/nexus consent <type> <accept\|deny>` | Grant or deny a specific consent type |

### Consent Types

| Consent Type | What It Covers |
| --- | --- |
| `activity_tracking` | Join/leave/playtime data |
| `purchase_history` | Transaction records |
| `discord_notifications` | Discord-linked player actions |
| `statistics` | Player stats and achievements |
| `marketing` | Server announcements and promotions |

On first join, players receive a prompt to accept or deny `activity_tracking`. Other consent types can be managed anytime via `/nexus consent`.

!!! info "Data deletion"
    Financial records newer than `gdpr.legal-retention-years` are **anonymised** rather than deleted, to comply with legal minimum retention requirements. All other data is removed immediately.

---

## Webstore Integration

The module bridges an external webstore with the plugin for **automatic kit delivery** and **payment verification**.

### VIP Kit Delivery

When a player purchases a rank or kit on the webstore, the order is queued. On the player's next join, `auto-deliver: true` delivers the kit automatically.

Kits are defined in `kits.yml`:

```yaml
kits:
  VIP:
    items:
      - material: DIAMOND
        amount: 5
      - nexusslime-item: RESEARCH_PARCHMENT_BASIC
        amount: 1
    commands:
      - "lp user {player} group set vip"
      - "tell {player} Welcome to VIP!"
  MVP:
    items:
      - material: NETHERITE_INGOT
        amount: 3
    commands:
      - "lp user {player} group set mvp"
```

---

## Configuration (`web-config.yml`)

```yaml
gdpr:
  enabled: true
  log-transactions: true
  data-retention-days: 365         # Days before inactive data is cleaned up
  legal-retention-years: 7         # Minimum legal retention for financial records
  allow-data-export: true
  allow-data-deletion: true

api:
  enabled: false
  endpoint: "https://your-website.com/api"
  key: ""
  rate-limit: 60                   # Requests per minute

payments:
  enabled: false
  provider: "custom"               # stripe | paypal | mercadopago | custom
  webhook-secret: ""

vip-kits:
  enabled: true
  auto-deliver: true               # Deliver pending kits on player join
  verify-payment: true             # Verify payment status before delivery
```

### Configuration Fields

| Field | Description |
| --- | --- |
| `gdpr.data-retention-days` | How long inactive player data is kept before automatic cleanup |
| `gdpr.legal-retention-years` | Minimum years financial records are retained (anonymised, not deleted) |
| `api.endpoint` | Your webstore's API URL for order verification |
| `payments.provider` | Payment processor: `stripe`, `paypal`, `mercadopago`, or `custom` |
| `vip-kits.auto-deliver` | Automatically deliver pending kits when the player joins |
| `vip-kits.verify-payment` | Double-check payment status via the API before delivering a kit |
