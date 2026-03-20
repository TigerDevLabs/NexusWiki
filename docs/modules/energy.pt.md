# Módulo Energy

O módulo Energy fornece uma **grade de energia baseada em Joules** para as máquinas. Geradores produzem energia, capacitores a armazenam e cabos a transportam — tudo conectado através de um grafo de rede automático.

---

## Como as Redes Funcionam

- Componentes se conectam por estarem **adjacentes** (se tocando) via cabos elétricos
- Quando qualquer componente é colocado ou removido, a rede **reescaneia automaticamente** (1 tick de delay)
- Se um componente for removido e dividir a rede, as duas metades se tornam **redes separadas**
- Máquinas consultam a rede conectada por energia; param de funcionar se a rede não tiver energia suficiente

---

## Máquinas e Taxas

| ID da Máquina | Tipo | Taxa |
| --- | --- | --- |
| `electric_cable` | Cabo (passagem) | — |
| `coal_generator` | Gerador a Carvão | 40 J/t |
| `coal_generator_2` | Gerador a Carvão Mk2 | 80 J/t |
| `solar_panel` | Painel Solar | 24 J/t *(apenas durante o dia)* |
| `small_capacitor` | Capacitor | 1.024 J máx · 128 J/t E/S |
| `medium_capacitor` | Capacitor | 8.192 J máx · 256 J/t E/S |
| `large_capacitor` | Capacitor | 65.536 J máx · 512 J/t E/S |

---

## Interações com Blocos

Toda a gestão de energia é feita com clique direito — não há comandos de jogador.

| Bloco | Ação |
| --- | --- |
| `coal_generator` / `coal_generator_2` | Abre o GUI do Gerador — adicione combustível, veja a taxa de produção |
| `solar_panel` | Abre o GUI do Gerador — veja a produção atual (0 à noite) |
| `small_capacitor` / `medium_capacitor` / `large_capacitor` | Abre o GUI do Capacitor — veja energia armazenada e taxa de E/S |

---

## Primeiros Passos

1. Coloque um gerador e uma máquina adjacentes, ou conecte-os com blocos `electric_cable`
2. Abasteca o gerador (clique direito → adicione carvão)
3. A máquina consumirá energia da rede a cada tick
4. Adicione capacitores para armazenar energia e suavizar picos de oferta/demanda

---

## API para Addons

O sistema de energia expõe uma API completa para que addons possam consultar redes e conectar componentes personalizados sem importar classes internas.

### Consultando redes

```java
import io.github.otiger.nexusprism.api.energy.EnergyRegistry;

EnergyRegistry.get().ifPresent(energy -> {
    // Rede em um bloco específico
    energy.getNetworkAt(location).ifPresent(net -> {
        long stored = net.getTotalStoredEnergy(); // FE armazenado em todos os capacitores
        long cap    = net.getTotalCapacity();     // capacidade total de armazenamento
        int  gen    = net.getGenerationRate();    // FE/t produzido
        int  con    = net.getConsumptionRate();   // FE/t consumido
        int  flow   = net.getNetFlow();           // gen - con (positivo = sobra)
    });

    // Todas as redes ativas no servidor
    energy.getAllNetworks().forEach(net -> { /* ... */ });

    int count = energy.getNetworkCount();
});
```

### Registrando um componente personalizado

Implemente `EnergyComponent` para criar geradores, consumidores ou blocos de armazenamento:

```java
// Em onEnable ou no listener de colocação de bloco:
EnergyRegistry.get().ifPresent(e -> e.registerComponent(meuComponente));

// Em onDisable ou no listener de quebra de bloco — sempre limpe:
EnergyRegistry.get().ifPresent(e -> e.unregisterComponent(meuComponente));
```

### Métodos do `EnergyNetwork` (selecionados)

| Método | Retorno | Descrição |
| --- | --- | --- |
| `getTotalStoredEnergy()` | `long` | FE total armazenado na rede |
| `getTotalCapacity()` | `long` | Capacidade total de armazenamento |
| `getGenerationRate()` | `int` | FE/t produzido pelos geradores |
| `getConsumptionRate()` | `int` | FE/t consumido pelas máquinas |
| `getNetFlow()` | `int` | `gen - con` (positivo = sobra) |
| `requestEnergy(amount, simulate)` | `long` | Retira energia; `true` para simular |
| `provideEnergy(amount, simulate)` | `long` | Injeta energia; `true` para simular |
| `getComponentAt(location)` | `Optional<EnergyComponent>` | Componente em um bloco |
| `getComponentsByType(type)` | `Collection<EnergyComponent>` | Filtrar por `GENERATOR / STORAGE / CONSUMER / CABLE` |
