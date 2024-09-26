### Release v3.1.6

A new release of the `terrad` client has been created on the 26th of September 2024. The release notes for the new version can be viewed here:

https://github.com/classic-terra/core/releases/tag/v3.1.6

This release applies an upstream wasmvm security patch. This update bumps wasmd to 1.5.5. This update also includes an improvement on gas simulation of taxable transactions which was only released to endpoint providers as it did not contain consensus-relevant changes (v3.1.5-sim.2).

### Proposal

This proposal seeks validator and community approval to update the `terrad` client to `v3.1.6` (upgrade name `v8_3`). The chain will be halted at **block height 20085000**  which will approximately be processed on **4th of October 2024 1:30pm UTC**. Upon passing of this proposal, an automatic chain halt will be scheduled at the specified height. The validators are going to be asked to install the new version of the `terrad` client after the chain halt occured.

### Upgrade Instructions for Validators

As soon as the chain automatically halts at the designated upgrade block height follow the upgrade procedure. Please **don't execute these commands before the chain has halted**:

```bash
$ git clone https://github.com/classic-terra/core core-v3.1.6
$ cd core-v3.1.6
$ git checkout v3.1.6
$ make build && make install 
```

In case you already have a local copy of the repository inside the local folder `core`:

```bash
$ cd core
$ git stash
$ git fetch --all
$ git fetch --tags
$ git checkout v3.1.6
$ make build && make install
```

Check the correct installation:

```bash
$ terrad version
v3.1.6
```

Check the correct wasmvm version is used:
```bash
$ terrad version --long | grep 'wasmvm'
github.com/CosmWasm/wasmvm@v1.5.5
```

After that, restart the client with `terrad start` or your system service and wait for consensus. During that period, **don't restart the client if not otherwise asked to do so**.

### Infrastructure Providers

Infrastructure providers who run mantlemint accelerated LCDs are asked to build and install the updated mantlemint version from source after the upgrade block height is reached:

https://github.com/classic-terra/mantlemint/releases/tag/v3.1.6

### Testing and Rollback

A rehearsal upgrade to `v3.1.6` was conducted on hellnet-1 testnet on 26th of September 2024. If for some unforeseen (and unlikely) reason the new release will not be able to produce new blocks on mainnet then the upgrade name `v8_3` can be applied to the previous release `v3.1.5`. In this case validators are going to be asked to roll back to a previous state and apply a patched `v3.1.5` release.

### Effects of Voting

- **YES** - you agree to schedule an upgrade to v3.1.6
- **NO** - you don't agree to schedule an upgrade to v3.1.6
- **ABSTAIN** - you want the proposal to reach quorum and align with the majority vote
- **VETO** - you strongly disagree and want the prop to fail with a 33,33% veto threshold
