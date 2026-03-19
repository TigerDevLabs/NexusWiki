# Tienda / Webstore

NexusPrism incluye un bridge de tienda web integrado que entrega los paquetes comprados a los jugadores automáticamente, incluso cuando están desconectados.

!!! warning "Cumplimiento del EULA"
    Todos los paquetes de la tienda deben cumplir con las [Directrices de Uso Comercial de Minecraft](https://www.minecraft.net/en-us/eula). La venta de ventajas de juego que no puedan obtenerse normalmente **no está permitida** en servidores accesibles al público.

---

## Funcionalidades Conformes al EULA

| Funcionalidad | Notas |
| --- | --- |
| **Apodos cosméticos** | `/nick` — solo visual, sin ventaja |
| **Sombreros cosméticos** | `/hat` — solo visual |
| **Homes adicionales** | Slots extra de home (comodidad) |
| **Volar fuera de zonas PvP** | Comodidad cosmética; deshabilitado en regiones PvP |
| **Acceso al resource pack** | Resource pack del servidor (cosmético) |
| **Slots extra de mochila** | Comodidad de almacenamiento |
| **Kit VIP (cosmético)** | Ítems cosméticos, equipamiento de vanidad |
| **Llaves de crate** | Siempre que todas las recompensas también puedan obtenerse en el juego |
| **Etiquetas de nombre con color** | Solo visual |
| **Cargo en Discord** | Acceso a un canal especial de Discord |
| **Mensajes de entrada personalizados** | Visual/cosmético |

---

## Sistema de Entrega

El bridge de webstore de NexusPrism usa una cola de entrega. Cuando un jugador compra un paquete:

1. La tienda envía una solicitud de entrega al plugin mediante el bridge
2. La entrega se pone en cola en `delivery.yml` (persistente)
3. En el próximo inicio de sesión del jugador, todas las entregas pendientes se procesan
4. Los comandos se ejecutan automáticamente en su nombre

Esto significa que la **entrega offline está soportada** — el jugador no necesita estar conectado en el momento de la compra.

### Configuración (`delivery.yml`)

```yaml
enabled: true

endpoint:
  host: "0.0.0.0"
  port: 9090
  token: "cambia-este-token-de-entrega"

file-fallback: "pending_deliveries.jsonl"
```

---

## Kits VIP (`kits.yml`)

```yaml
kits:
  vip:
    display-name: "&6Kit VIP"
    permission: "nexusprism.kit.vip"
    cooldown-hours: 24
    items:
      - material: GOLDEN_APPLE
        amount: 5
      - nexusprism-id: SERVER_KEY
        amount: 1
    commands:
      - "eco give {player} 1000"

  mvp:
    display-name: "&bKit MVP"
    permission: "nexusprism.kit.mvp"
    cooldown-hours: 24
    items:
      - material: GOLDEN_APPLE
        amount: 16
      - nexusprism-id: SERVER_KEY
        amount: 2
    commands:
      - "eco give {player} 2500"
```

---

## Plataformas de Tienda Recomendadas

- **Tebex** (antes Buycraft) — certificado por el EULA
- **CraftingStore** — certificado por el EULA
- **Panel personalizado** — usa el endpoint HTTP de entrega
