# v14_1 Proposal — Software Upgrade (Cosmos SDK 0.53.x)

### Release v4.0.0

A new release of the `terrad` client has been created. The release notes for this version can be viewed here:
https://github.com/classic-terra/core/releases/tag/v4.0.0

This release prepares the **Cosmos SDK 0.53 ("SDK 53")** upgrade for Terra Classic and includes the **`v14_1`** upgrade handler intended for mainnet.

Target dependency versions in this release candidate:
- Cosmos SDK `v0.53.6`
- CometBFT `v0.38.21`
- wasmd `v0.61.8`
- wasmvm `v3.0.3`

### Proposal

This proposal seeks validator and community approval to update the `terrad` client to `v4.0.0` (upgrade name `v14_1`). The chain will be halted at **28214400** which will approximately be processed on **Fri Apr 17 2026 14:30 UTC**. The actual halt time is an early estimate, can vary, and depends on the chain's block speed until the specified height is reached.

Upon passing of this proposal, an automatic chain halt will be scheduled at the specified height. Validators are asked to install the new version of the `terrad` client after the chain halt occured.

### Upgrade Instructions for Validators

As soon as the chain automatically halts at the designated upgrade block height, follow the upgrade procedure. Please **don't execute these commands before the chain has halted**:

```bash
$ git clone https://github.com/classic-terra/core core-v4.0.0
$ cd core-v4.0.0
$ git checkout v4.0.0
$ make build && make install
```

In case you already have a local copy of the repository inside the local folder `core`:

```bash
$ cd core
$ git stash
$ git fetch --all
$ git fetch --tags
$ git checkout v4.0.0
$ make build && make install
```

Check the correct installation:

```bash
$ terrad version
v4.0.0
```

After that, restart the client with `terrad start` or your system service and wait for consensus. During that period, **don't restart the client if not otherwise asked to do so**.

### Infrastructure Providers

Infrastructure providers (e.g. RPC/LCD/API providers and indexers) are advised to plan their own upgrade procedure around the same upgrade height and should rebuild any dependent services against the new `terrad` version where required.

### Testing and Rollback

- A mainnet-fork/state upgrade test was executed in collaboration with StrathCole and the upgrade completed successfully.
- Additional testnet and ecosystem testing results should be added here as they become available.

If for some unforeseen (and unlikely) reason the new release will not be able to produce new blocks on mainnet then the upgrade name `v14_1` can be applied to a patched build or a designated fallback release. In this case validators are going to be asked to roll back to a previous state and apply the corrected binary.

### Effects of Voting

- **YES** - you agree to schedule an upgrade to v4.0.0
- **NO** - you don't agree to schedule an upgrade to v4.0.0
- **ABSTAIN** - you want the proposal to reach quorum and align with the majority vote
- **VETO** - you strongly disagree and want the prop to fail with a 33,33% veto threshold
