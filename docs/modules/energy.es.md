# Módulo Energy

El módulo Energy proporciona una **red de energía basada en Julios** para las máquinas. Los generadores producen energía, los capacitores la almacenan y los cables la transportan.

---

## Máquinas y Tasas

| ID de máquina | Tipo | Tasa |
| --- | --- | --- |
| `electric_cable` | Cable (paso) | — |
| `coal_generator` | Generador de Carbón | 40 J/t |
| `coal_generator_2` | Generador de Carbón Mk2 | 80 J/t |
| `solar_panel` | Panel Solar | 24 J/t *(solo de día)* |
| `small_capacitor` | Capacitor | 1.024 J máx · 128 J/t E/S |
| `medium_capacitor` | Capacitor | 8.192 J máx · 256 J/t E/S |
| `large_capacitor` | Capacitor | 65.536 J máx · 512 J/t E/S |

---

## Interacciones con Bloques

| Bloque | Acción |
| --- | --- |
| `coal_generator` / `coal_generator_2` | Abre GUI del Generador — añade combustible, ve la tasa de producción |
| `solar_panel` | Abre GUI del Generador — ve la producción actual (0 de noche) |
| `small_capacitor` / `medium_capacitor` / `large_capacitor` | Abre GUI del Capacitor — ve energía almacenada y tasa de E/S |

---

## Primeros Pasos

1. Coloca un generador y una máquina adyacentes, o conéctalos con bloques `electric_cable`
2. Abastece el generador (clic derecho → añade carbón)
3. La máquina consumirá energía de la red cada tick
4. Añade capacitores para almacenar energía y suavizar picos de oferta/demanda
