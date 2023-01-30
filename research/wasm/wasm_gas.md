# Wasm Gas

## I. Gas strategy

1. Reference
- https://github.com/CosmWasm/cosmwasm/blob/main/docs/GAS.md
- https://github.com/CosmWasm/wasmd/pull/634

2. Main points
- Gas calculation is based on **CPU time** and **storage cost**.
- Gas consumption is deterministic. Gas is charged for each Wasm operation. 
- CosmWasm team will have a target for gas adjustments, e.g. when the Wasm runtime becomes faster or slower. The target for adjustment is 1 Terragas (10^12 gas) per millisecond.

3. Gas calculation
- There are these following actions that will cost gas:
    * db_read
    * db_write
    * db_remove
    * addr_validate
    * addr_canonicalize
    * addr_humanize
    * secp256k1_verify
    * secp256k1_recover_pubkey
    * ed25519_verify
    * ed25519_batch_verify
    * query_chain
    * db_scan
    * db_next
- The function that handle gas change is [process_gas_info()](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/environment.rs#L336). Each of the above actions calls process_gas_info().
- Step 1: Every time you invoke execute, instantiate, query, ... in a smart contract, the request will be routed to corresponding smart contract for handling. It will use some actions above which results in several gas change. CosmWasm VM Instance will [create_gas_report()](https://github.com/CosmWasm/cosmwasm/blob/main/packages/vm/src/instance.rs#L293) to get final Wasm gas usage after all invocation is done.
- Step 2: Wasm gas usage will be returned to x/wasm module where it will be modified by GasMultiplier to get SDK gas.
- Step 3: SDK gas is deducted from caller balances

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
**SUMMARY**: benchmark gas cost based on secp256k1 sig verification as CPU time

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
**SUMMARY**: benchmark gas cost based on writing 1000000 keys into goleveldb as Storage usage

- Storage usage: secp256k1 is charged 2x compared to storage operations. Ethan Frey has done benchmarking on both storing keys into **goleveldb** and secp256k1 sig verification to derive gas difference here: https://github.com/CosmWasm/wasmd/pull/634#issuecomment-938053734
    - CPU usage/2 = storage usage

1. Calculation
- 200_000_000 is updated to 100_000_000 gas multiplier for Storage usage 
- Why change from CPU usage to Storage usage?

Can dynamic gas multiplier be realized? It will help a chain to compete on gas price.

## III. CompileCost

### First iteration
**SUMMARY**: benchmark gas cost based on secp256k1 sig verification as CPU time

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
**SUMMARY**: benchmark gas cost based on writing 1000000 keys into goleveldb as Storage usage

1. Calculation
- When converted to Storage usage: 0.7*2 = 1.4 (gas/bytes) ~ 2 (gas/bytes)

## IV. InstantiateCost

### First iteration
**SUMMARY**: 
* benchmark instantiation overhead between get instance from file_system cache and get instance from pinned_memory cache
* benchmark gas cost based on secp256k1 sig verification as CPU time

READ MORE ABOUT file_system_cache AND pinned_memory cache [here](./wasm_cache.md)

1. Calculation
- for reproducibility, please download this branch: https://github.com/classic-terra/core/tree/wasm-upgrade
- running "go test -benchmem -run=^$ -bench ^BenchmarkInstantiationOverhead$ github.com/terra-money/core/x/wasm/keeper"
- gas benchmark for querying contracts from unpinned memory (file_system cache): 14839385 ns/op
- gas benchmark for querying contracts from pinned memory (pinned_memory cache): 103717 ns/op
- overhead: 14839385 - 103717 = 14735668 ns
- ns per SDK gas (taken from secp256k1 calculation): 201235 / 1000 = 201.235 (ns/gas)
- gas per operation = 14735668 (ns/op) / 201.235 (ns/gas) = 73226.1684101 (gas/op) ~ 70_000

### Second iteration
**SUMMARY**: 
* benchmark instantiation overhead between get instance from file_system cache and get instance from pinned_memory cache
* benchmark gas cost based on writing 1000000 keys into goleveldb as Storage usage

1. Calculation
- When converted to Storage usage: 73226.1684101*2 = 146452.33682 ~ 140_000