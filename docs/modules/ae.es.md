# Módulo ME Storage

El módulo ME Storage es un **sistema de almacenamiento en red estilo Applied Energistics**. Coloca un ME Controller, conecta drives y terminales mediante cables y gestiona miles de ítems a través de una única interfaz unificada.

---

## Máquinas

| ID de máquina | Descripción | Canales |
| --- | --- | --- |
| `me_controller` | Alimenta la red; clic derecho para ver estado | — |
| `me_cable_glass` | Cable básico — solo conectividad | 0 |
| `me_cable_smart` | Cable estándar | 8 |
| `me_cable_dense` | Cable de alto ancho de banda | 32 |
| `me_drive` | Hasta 10 celdas de almacenamiento | 1 |
| `me_terminal` | GUI para insertar y extraer ítems | 1 |

---

## Celdas de Almacenamiento

| Celda | ID del ítem | Capacidad | Máx. tipos |
| --- | --- | --- | --- |
| Celda 1K | `STORAGE_CELL_1K` | 1.024 ítems | 63 |
| Celda 4K | `STORAGE_CELL_4K` | 4.096 ítems | 63 |
| Celda 16K | `STORAGE_CELL_16K` | 16.384 ítems | 63 |
| Celda 64K | `STORAGE_CELL_64K` | 65.536 ítems | 63 |
| Celda 256K | `STORAGE_CELL_256K` | 262.144 ítems | 63 |

!!! warning "Romper un drive"
    Al romper un ME Drive, las celdas caen como su material base — el contenido almacenado **no se dropea**. Siempre extrae los ítems desde el terminal antes de remover un drive.

---

## Primeros Pasos

1. Obtén un `me_controller`, cables, un `me_drive`, un `me_terminal` y al menos una celda
2. Coloca el controller y conecta el drive y el terminal mediante cables
3. Clic derecho en el controller para verificar que la red está en línea
4. Clic derecho en el drive e inserta una celda de almacenamiento
5. Clic derecho en el terminal para comenzar a gestionar ítems
