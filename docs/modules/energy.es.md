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

---

## API para Addons

El sistema de energía expone una API completa para que los addons puedan consultar redes y conectar componentes personalizados sin importar clases internas.

### Consultando redes

```java
import io.github.otiger.nexusprism.api.energy.EnergyRegistry;

EnergyRegistry.get().ifPresent(energy -> {
    // Red en un bloque específico
    energy.getNetworkAt(location).ifPresent(net -> {
        long stored = net.getTotalStoredEnergy(); // FE almacenado en todos los capacitores
        long cap    = net.getTotalCapacity();     // capacidad total de almacenamiento
        int  gen    = net.getGenerationRate();    // FE/t producido
        int  con    = net.getConsumptionRate();   // FE/t consumido
        int  flow   = net.getNetFlow();           // gen - con (positivo = excedente)
    });

    // Todas las redes activas en el servidor
    energy.getAllNetworks().forEach(net -> { /* ... */ });

    int count = energy.getNetworkCount();
});
```

### Registrando un componente personalizado

Implementa `EnergyComponent` para crear generadores, consumidores o bloques de almacenamiento personalizados:

```java
// En onEnable o en el listener de colocar bloque:
EnergyRegistry.get().ifPresent(e -> e.registerComponent(miComponente));

// En onDisable o en el listener de romper bloque — siempre limpia:
EnergyRegistry.get().ifPresent(e -> e.unregisterComponent(miComponente));
```

### Métodos de `EnergyNetwork` (seleccionados)

| Método | Retorno | Descripción |
| --- | --- | --- |
| `getTotalStoredEnergy()` | `long` | FE total almacenado en la red |
| `getTotalCapacity()` | `long` | Capacidad total de almacenamiento |
| `getGenerationRate()` | `int` | FE/t producido por los generadores |
| `getConsumptionRate()` | `int` | FE/t consumido por las máquinas |
| `getNetFlow()` | `int` | `gen - con` (positivo = excedente) |
| `requestEnergy(amount, simulate)` | `long` | Extrae energía; `true` para simular |
| `provideEnergy(amount, simulate)` | `long` | Inyecta energía; `true` para simular |
| `getComponentAt(location)` | `Optional<EnergyComponent>` | Componente en un bloque |
| `getComponentsByType(type)` | `Collection<EnergyComponent>` | Filtrar por `GENERATOR / STORAGE / CONSUMER / CABLE` |
