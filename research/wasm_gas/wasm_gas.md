# Wasm Gas

## I. Gas strategy

https://github.com/CosmWasm/cosmwasm/blob/main/docs/GAS.md

- Gas calculation is based on **CPU time** and **storage cost**.
- Gas consumption is deterministic. Gas is charged for each Wasm operation. 
- CosmWasm team will have a target for adjustments, e.g. when the Wasm runtime becomes faster or slower. The target for adjustment is 1 Terragas (10^12 gas) per millisecond.

## II. GasMultiplier (The lower this is, the higher SDK gas will be charged)

### First iteration
**SUMMARY**: benchmark gas cost for a smart contract

1. Calculation
- 96837752 gas and took 15ms (6,455,850.13333 per millisecond) (calculate gas for instantiating and executing a smart contract)
    - https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/benches/main.rs#L90
- multiplier rate (gas/wasm ops) to make it reach target:
    - 10^12/6,455,850.13333 = 154,898 → 150,000 gas/wasm ops
    - 150_000 gas multiplier is considered too low which leads to overcharging of SDK gas

### Second iteration 
**SUMMARY**: benchmark gas cost for secp256k1 sig verification as CPU time

- For SDK Gas, secp256k1 sig verification call cost 1000 gas

1. Calculation
- for reproducibility, please download this branch: https://github.com/classic-terra/core/tree/wasm-upgrade
- running "go test -benchmem -run=^$ -bench ^BenchmarkGasNormalization$ github.com/terra-money/core/x/wasm/keeper"
- benchmark result of BenchmarkGasNormalization on M1 pro: 201235 ns/call
- calculate SDK gas per millisecond:
    - convert 201235 (ns/call) to ms/call: 201235 / 10^6
    - calculate sdk gas/ms: 1000 (gas/call) / (201235 (ns/call) / 10^6) = 4969.31448307 gas/ms
- calculate multiplier rate
    - 10^12/4969.31448307 = 201235000 (gas/wasm ops)
    - 200_000_000 gas multiplier

### Third iteration
**SUMMARY**: benchmark gas cost for writing 1000000 keys into goleveldb as Storage usage

- Storage usage: secp256k1 is charged 2x compared to storage operations. Ethan Frey has done benchmarking on both storing keys into **goleveldb** and secp256k1 sig verification to derive gas difference here: https://github.com/CosmWasm/wasmd/pull/634#issuecomment-938053734
    - CPU usage/2 = storage usage

1. Calculation
- 200_000_000 is updated to 100_000_000 gas multiplier for Storage usage 
- Why change from CPU usage to Storage usage?

Can dynamic gas multiplier be realized? It will help a chain to compete on gas price.

## III. CompileCost

### First iteration
**SUMMARY**: benchmark gas cost for secp256k1 sig verification as CPU time

1. Calculation
- for reproducibility, please download this branch: https://github.com/classic-terra/core/tree/wasm-upgrade
- running "go test -benchmem -run=^$ -bench ^BenchmarkCompilation$ github.com/terra-money/core/x/wasm/keeper"
- gas benchmark for compiling burner wasm contract: 16395133 ns / 125239 bytes = 130.91 (ns/bytes)
- gas benchmark for compiling hackatom wasm contract: 31091749 ns / 214650 bytes = 144.85 (ns/bytes)
- gas benchmark for compiling maker wasm contract: 35596363 ns / 222488 bytes = 160 (ns/bytes)
- average: 145.25 (ns/bytes)
- ns per SDK gas (taken from secp256k1 calculation): 201235 / 1000 = 201.235 (ns/gas)
- 145.25/201.35 = 0.7 (gas/bytes) (CPU usage) ~ 1 (gas/bytes)

### Second iteration
**SUMMARY**: benchmark gas cost for secp256k1 sig verification as CPU time

1. Calculation
- When converted to Storage usage: 0.7*2 = 1.4 (gas/bytes) ~ 2 (gas/bytes)

## IV. InstantiateCost

Not yet