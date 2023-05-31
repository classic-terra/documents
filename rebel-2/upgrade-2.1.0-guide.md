# Upgrade Guide for `rebel-2` Testnet

The `v2.1.0` upgrade happens via chain halt upgrade on May 31st 2023. All `terrad` clients are going to exit on block height `14584970` and expect upgrade name `v4` to be started as replacement. The following steps should be applied by all testnet validators: 

## Installation

After chain halt the `rebel-2` upgrade testnet binary can be installed using the following chain of cli commands:

- `git clone https://github.com/classic-terra/core core-v2.0.1`
- `cd core-v2.0.1`
- `git checkout tags/v2.0.1-rc.0`
- `make build && make install`

Check the installed `terrad` version using `terrad version`. This should show `v2.1.0-rc.0`. After installation ***DO NOT*** start the binary again. Please, perform another step before restarting the binary.

## Modify `wasm` config

The `wasm` default config needs to be tweaked. Open up `.terra/config/app.toml` with your favorite text editor and search for the following config section in:

```
[wasm]
# The maximum gas amount can be spent for contract query.
# The contract query will invoke contract execution vm,
# so we need to restrict the max usage to prevent DoS attack
contract-query-gas-limit = "3000000"

# The flag to specify whether print contract logs or not
contract-debug-mode = "false"

# The WASM VM memory cache size in MiB not bytes
contract-memory-cache-size = "100"
```

This section should be located pretty much at the bottom. Replace this snipped by the following config section:

```
###############################################################################
###                                  WASM                                   ###
###############################################################################

[wasm]
# Smart query gas limit is the max gas to be used in a smart query contract call
query_gas_limit = 3000000

# in-memory cache for Wasm contracts. Set to 0 to disable.
# The value is in MiB not bytes
memory_cache_size = 100

# Simulation gas limit is the max gas to be used in a tx simulation call.
# When not set the consensus max block gas is used instead
# simulation_gas_limit =
```

## Restart

After installation and config tweak we should now be able to restart the binary. Hit `terrad start` and wait for the network to come online again.

Happy upgrading ;)
