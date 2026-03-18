# Módulo Chat

El módulo Chat reemplaza el chat predeterminado de Minecraft con un **sistema de 4 canales** — local, global, staff y report — cada uno con radio, formato e integración de prefijo de LuckPerms configurables.

---

## Canales

| Canal | Activación | Audiencia | Descripción |
| --- | --- | --- | --- |
| **Local** | Por defecto (sin prefijo) | Jugadores dentro del radio | Chat por proximidad |
| **Global** | `!<mensaje>` o `/g` | Todos los jugadores en línea | Transmisión para todo el servidor |
| **Staff** | `/staffchat` o `/sc` | Solo staff | Canal privado de comunicación del equipo |
| **Report** | `/report <jugador> <motivo>` | Solo staff | Denuncias de jugadores entregadas al staff |

---

## Comandos

| Comando | Aliases | Uso | Permiso |
| --- | --- | --- | --- |
| `/globalchat <mensaje>` | `/g`, `/gc` | Enviar mensaje a todos | `nexusslime.chat.global` |
| `/staffchat <mensaje>` | `/sc` | Enviar mensaje al staff | `nexusslime.chat.staff` |
| `/report <jugador> <motivo>` | — | Denunciar un jugador | `nexusslime.chat.report` |
| `/chat reload` | — | Recargar configuración del chat | `nexusslime.chat.admin` |

---

## Permisos

| Permiso | Descripción | Por defecto |
| --- | --- | --- |
| `nexusslime.chat.global` | Usar el canal de chat global | true |
| `nexusslime.chat.staff` | Acceder al canal de staff | OP |
| `nexusslime.chat.report` | Enviar denuncias de jugadores | true |
| `nexusslime.chat.admin` | Recargar configuración del chat | OP |

---

## Configuración (`chat/config.yml`)

```yaml
chat:
  local:
    radius: 100
    format: "{prefix}&f{name}&7: &f{message}"

  global:
    format: "&8[&bGlobal&8] {prefix}&f{name}&7: &f{message}"
    trigger-prefix: "!"

  staff:
    format: "&8[&cStaff&8] &7{name}&7: &c{message}"

  report:
    format: "&8[&6Report&8] &e{reporter}&7 reportó a &c{target}&7: &f{reason}"

  luckperms-prefix:
    enabled: true
```

---

## Integración con LuckPerms

Con LuckPerms instalado y `luckperms-prefix.enabled: true`, el prefijo de rango de cada jugador se inserta automáticamente en el placeholder `{prefix}` en los formatos de chat. No se necesita configuración adicional.
