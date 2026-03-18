# ME Storage Module

The ME Storage module is an **Applied Energistics-style network storage system**. Place an ME Controller, connect drives and terminals via cables, and manage thousands of items through a single unified inventory.

---

## Network Basics

A network requires:
1. **ME Controller** — powers the network and defines the channel budget
2. **Cables** — connect components; different tiers provide different channel counts
3. **ME Drive** — holds storage cells (actual item storage)
4. **ME Terminal** — the GUI where players insert and retrieve items

Components beyond the channel budget are marked **inactive** and do not function. The network rescans automatically 1 tick after any AE block is placed or broken.

---

## Machines

| Machine ID | Description | Channels |
| --- | --- | --- |
| `me_controller` | Powers the network; right-click for network status | — |
| `me_cable_glass` | Basic cable — connectivity only, no channels | 0 |
| `me_cable_smart` | Standard cable | 8 |
| `me_cable_dense` | High-bandwidth cable | 32 |
| `me_drive` | Holds up to 10 storage cells | 1 |
| `me_terminal` | GUI for inserting and retrieving items | 1 |

Channel budget = sum of channel capacities of cables **directly adjacent** to the controller. Drives and terminals each cost 1 channel. The BFS scan limit is 512 blocks.

---

## Storage Cells

Storage cells are items inserted into ME Drives to provide inventory capacity.

| Cell | Item ID | Capacity | Max Item Types |
| --- | --- | --- | --- |
| 1K Cell | `STORAGE_CELL_1K` | 1,024 items | 63 |
| 4K Cell | `STORAGE_CELL_4K` | 4,096 items | 63 |
| 16K Cell | `STORAGE_CELL_16K` | 16,384 items | 63 |
| 64K Cell | `STORAGE_CELL_64K` | 65,536 items | 63 |
| 256K Cell | `STORAGE_CELL_256K` | 262,144 items | 63 |

!!! warning "Breaking a drive"
    When an ME Drive is broken, the cell **items** drop as their base material — the stored contents are **not** dropped. Always extract items via the terminal before removing a drive.

---

## Block Interactions

There are no commands — all ME interaction is via right-click:

| Block | Action |
| --- | --- |
| `me_controller` | Prints network status: online/offline, channels used/total, component count |
| `me_drive` | Opens the Drive GUI — manage the 10 cell slots |
| `me_terminal` | Opens the Terminal GUI — view, insert, and extract items from all drives (requires powered network + available channels) |

---

## Persistence

Drive states (which cells are installed and their contents) are saved to `ae/drives/{world}_{x}_{y}_{z}.yml` files. Data survives server restarts.

---

## Getting Started

1. Craft or obtain an `me_controller`, some cables, an `me_drive`, an `me_terminal`, and at least one storage cell
2. Place the controller, then connect the drive and terminal via cables
3. Right-click the controller to verify the network is online
4. Right-click the drive and insert a storage cell
5. Right-click the terminal to start managing items
