# Upgrade Guide for `rebel-2` Testnet

The `v2.2.0` upgrade happens via chain halt upgrade around 24 - 25 August, 2023. All `terrad` clients are going to exit on block height `15861000` and expect upgrade name `v5` to be started as replacement. The following steps should be applied by all testnet validators: 

## Installation

After chain halt the `rebel-2` upgrade testnet binary can be installed using the following chain of cli commands:

- `git clone --depth 1 --branch v2.2.1 https://github.com/classic-terra/core core-v2.2.1`
- `cd core-v2.2.1`
- `make build && make install`

Check the installed `terrad` version using `terrad version`. This should show `2.2.1`.

## Restart

After installation, we should now be able to restart the binary. Hit `terrad start` and wait for the network to come online again.

Happy upgrading ;)
