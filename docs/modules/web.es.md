# Módulo Web & GDPR

El módulo Web gestiona la **integración con la tienda virtual**, **entrega de kits VIP**, **webhooks de pago** y **cumplimiento del RGPD** — dando a los jugadores control sobre sus datos personales.

---

## Cumplimiento del RGPD

| Comando | Descripción |
| --- | --- |
| `/nexus gdpr` | Mostrar información de RGPD y configuración de consentimiento |
| `/nexus gdpr export` | Exportar todos los datos personales a un archivo JSON |
| `/nexus gdpr delete` | Eliminar todos los datos personales (derecho al olvido) |
| `/nexus consent <tipo> <accept\|deny>` | Otorgar o denegar un tipo de consentimiento |

### Tipos de Consentimiento

| Tipo | Qué cubre |
| --- | --- |
| `activity_tracking` | Datos de conexión y tiempo de juego |
| `purchase_history` | Registros de transacciones |
| `discord_notifications` | Acciones del jugador vinculadas a Discord |
| `statistics` | Estadísticas y logros del jugador |
| `marketing` | Anuncios y promociones del servidor |

---

## Configuración (`web-config.yml`)

```yaml
gdpr:
  enabled: true
  data-retention-days: 365
  legal-retention-years: 7
  allow-data-export: true
  allow-data-deletion: true

api:
  enabled: false
  endpoint: "https://tu-sitio.com/api"
  key: ""

payments:
  enabled: false
  provider: "custom"           # stripe | paypal | mercadopago | custom
  webhook-secret: ""

vip-kits:
  enabled: true
  auto-deliver: true
  verify-payment: true
```
