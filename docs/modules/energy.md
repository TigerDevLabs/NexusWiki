# Energy Module

The Energy module provides a **Joule-based power grid** for machines. Generators produce energy, capacitors store it, and cables carry it — all connected through an automatic network graph.

---

## How Networks Work

- Components connect by being **adjacent** (touching) via electric cables
- When any component is placed or broken, the network **rescans automatically** (1-tick delay)
- If a component is removed and splits the network, the two halves become **separate networks**
- Machines query their connected network for energy; they stop working if the network has insufficient power

---

## Machines & Rates

| Machine ID | Type | Rate |
| --- | --- | --- |
| `electric_cable` | Cable (passthrough) | — |
| `coal_generator` | Coal Generator | 40 J/t |
| `coal_generator_2` | Coal Generator Mk2 | 80 J/t |
| `solar_panel` | Solar Panel | 24 J/t *(daytime only)* |
| `small_capacitor` | Capacitor | 1,024 J max · 128 J/t I/O |
| `medium_capacitor` | Capacitor | 8,192 J max · 256 J/t I/O |
| `large_capacitor` | Capacitor | 65,536 J max · 512 J/t I/O |

---

## Block Interactions

All energy management is via right-click — there are no player commands.

| Block | Action |
| --- | --- |
| `coal_generator` / `coal_generator_2` | Opens Generator GUI — add fuel, view production rate |
| `solar_panel` | Opens Generator GUI — view current output (0 at night) |
| `small_capacitor` / `medium_capacitor` / `large_capacitor` | Opens Capacitor GUI — view stored energy and I/O rate |

!!! warning
    If a component is not connected to any network, right-clicking it shows an error message instead of the GUI.

---

## Getting Started

1. Place a generator (coal or solar) and a machine adjacent to each other, or connect them with `electric_cable` blocks
2. Fuel the generator (right-click → add coal or similar)
3. The machine will draw energy from the network each tick
4. Add capacitors to buffer energy and smooth out supply/demand spikes

---

## Persistence

Generator fuel levels and capacitor charge are saved to the `energy/` data folder and survive server restarts. Components rehydrate their state automatically on chunk load.

---

## Addon API

The energy system exposes a full API so addons can query networks and plug in custom components without importing any internal classes.

### Querying networks

```java
import io.github.otiger.nexusprism.api.energy.EnergyRegistry;

EnergyRegistry.get().ifPresent(energy -> {
    // Network at a specific block
    energy.getNetworkAt(location).ifPresent(net -> {
        long stored = net.getTotalStoredEnergy(); // FE stored across all capacitors
        long cap    = net.getTotalCapacity();     // total storage capacity
        int  gen    = net.getGenerationRate();    // FE/t produced
        int  con    = net.getConsumptionRate();   // FE/t consumed
        int  flow   = net.getNetFlow();           // gen - con (positive = surplus)
    });

    // All active networks on the server
    energy.getAllNetworks().forEach(net -> { /* ... */ });

    // Quick helper
    int count = energy.getNetworkCount();
});
```

### Registering a custom component

Implement `EnergyComponent` to create custom generators, consumers, or storage blocks:

```java
import io.github.otiger.nexusprism.api.energy.EnergyComponent;
import io.github.otiger.nexusprism.api.energy.EnergyComponentType;
import io.github.otiger.nexusprism.api.energy.EnergyRegistry;

// In onEnable or a block-place listener:
EnergyRegistry.get().ifPresent(e -> e.registerComponent(myComponent));

// In onDisable or a block-break listener — always clean up:
EnergyRegistry.get().ifPresent(e -> e.unregisterComponent(myComponent));
```

### `EnergyNetwork` interface (selected methods)

| Method | Returns | Description |
| --- | --- | --- |
| `getTotalStoredEnergy()` | `long` | Total FE stored in this network |
| `getTotalCapacity()` | `long` | Total storage capacity in FE |
| `getGenerationRate()` | `int` | FE/t produced by generators |
| `getConsumptionRate()` | `int` | FE/t consumed by machines |
| `getNetFlow()` | `int` | `gen - con` (positive = surplus) |
| `requestEnergy(amount, simulate)` | `long` | Withdraw energy; pass `true` to simulate |
| `provideEnergy(amount, simulate)` | `long` | Inject energy; pass `true` to simulate |
| `getComponentAt(location)` | `Optional<EnergyComponent>` | Component at a block |
| `getComponentsByType(type)` | `Collection<EnergyComponent>` | Filter by `GENERATOR / STORAGE / CONSUMER / CABLE` |
